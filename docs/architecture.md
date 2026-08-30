# Architecture — Precision GNSS Receiver

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- GNSS RF chain
- 50-ohm routing
- LNA/filter
- quiet supplies

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## GNSS receiver selection and what it already integrates

- Module or bare receiver IC, and what makes that the right split for this board?
- Which constellations and bands does the chosen part cover, and does that match what "GNSS" is being asked to do here?
- Does the chosen part already contain an LNA, a SAW filter, a DC block or a bias path on its RF input, and what does its datasheet say about required external front-end parts?
- What RF input impedance and maximum input level does the part specify at its antenna pin?
- What does the part require on its backup-supply pin — voltage window, current draw, and what state it actually retains?
- Which of the required outputs (USB, UART, timing/status) does the part provide natively, and which must be built around it?

## Antenna port: connector, ESD and bias feed

- Which connector family and mount style, and what does that choice imply for the antenna cable and for board edge geometry?
- Where in the chain does the ESD device sit relative to the bias injection point and the first filter or amplifier stage?
- What is the ESD device's shunt capacitance, and what insertion loss and return-loss penalty does it add at the GNSS band?
- What bias voltage and current must the feed deliver, and against which class of active antenna is that number justified?
- By what route does DC reach the antenna — over the RF conductor, on a separate conductor, or from a bias path the chosen part already provides — and how is the bias network built (choke, ferrite, integrated bias-tee)?
- For whichever bias element is chosen, is its behaviour at the GNSS band — impedance, self-resonance, insertion loss — acceptable in the receive path?
- Does DC have to be blocked from the receiver's RF input, and if so is that block a discrete part in the path or already inside the chosen receiver?
- What happens to the bias source with a shorted or absent antenna, and is any protection or bias-current sensing warranted here?

## Receive chain budget: filtering and low-noise amplification

- What is the cascaded noise figure from the connector to the receiver input, computed stage by stage with real datasheet numbers?
- The antenna is active, so gain already sits ahead of the connector: what do that and the chosen part's own integrated front end imply about whether a further discrete LNA belongs here, and what does each answer cost — in noise figure if omitted, in compression on out-of-band interferers if added?
- Which out-of-band threats does the filter have to reject, and what rejection does the chosen filter actually provide at those frequencies?
- What is the total insertion loss ahead of the first gain stage — connector, ESD device, any bias-network or DC-blocking components, trace — and how much does it cost in noise figure?
- What is the total chain gain, and does it stay inside the receiver's specified input range?
- How is each active stage in the RF path supplied and decoupled, and where does its supply come from?

## Controlled-impedance RF routing and stackup

- The stressor list names 50-ohm routing: is 50 ohm the target at both ends of this path, and what tolerance do the parts on either end actually require?
- Which stackup — dielectric heights, copper weights, layer assignment — produces that impedance, and from whose published stack is it computed?
- Which layer carries the RF trace, and which plane is its reference, unbroken end to end?
- Is the trace coplanar-waveguide-with-ground, microstrip, or something else, and what gap and stitching pitch does that require?
- What is the actual physical length of the antenna-to-receiver path, and what argument makes it "short" for this board?
- How are the connector launch and every component pad transition handled so the impedance is continuous through them?
- Is there a via in the RF path, and if so how is its transition compensated and stitched?

## Isolation from digital clocks and switching regulators

- Where does every clock source and every switching node sit relative to the RF section on the floorplan?
- What separation, keep-out, guarding or shielding enforces that isolation, and how will it be demonstrated rather than asserted?
- Which switching frequencies and their harmonics land in or near the GNSS band, and how is that avoided or attenuated?
- Do any return currents from digital or switching sections cross under the RF trace or its reference plane?
- Are the RF ground and the digital ground treated as one plane or partitioned, and what is the justification for whichever is chosen?
- Do the USB-C data lines, the UART, or the timing output route anywhere near the antenna port or the front-end stages?

## Power architecture and supply quietness

- What are the input source(s) and the resulting rail list, and which blocks does each rail feed?
- Which rails feeding the RF front end are LDO-supplied versus switcher-supplied, and what noise and PSRR numbers back that decision?
- What is the residual ripple at the receiver's and any RF amplifier's supply pins in the GNSS band, and against what limit is that judged?
- Is any switching converter placed such that its inductor field couples to the RF section, and how is that bounded?
- What sequencing or inrush behaviour does the receiver require at power-up?
- How are the antenna bias supply and the receiver supply related — shared rail or separated, and why?

## Backup supply and state retention

- What holds the backup energy, and what retention duration is the target?
- What is the receiver's backup-current draw, and what leakage does the isolation/charging path add?
- Does the backup element get charged from the board, and if so what limits the charge current and voltage?
- How is backup current prevented from flowing backwards into the main rail when it is down?
- What happens at the crossover between main and backup power — is retained state guaranteed through the transition?
- Does the chosen element impose storage, temperature or shipping constraints on the assembled board?

## Host interfaces: USB-C and UART

- How is USB-C output produced — natively by the receiver or through a bridge — and what does that dictate about port role and CC termination?
- If USB carries data, is it the receiver's native USB or a bridge, and what does that add to the BOM and to the noise environment?
- Which USB-C port role does the board take, what CC termination does that role require, and what current does it advertise or draw?
- Are the USB pair's impedance and length matching handled by the same stackup that carries the RF trace?
- What are the UART's electrical level, connector, pinout and default rate, and what consumes it?
- Is there ESD protection on the USB-C and UART pins that reach the outside world, and where does it sit?

## Status and timing output

- What signal does the timing output actually carry, and which receiver pin sources it?
- Is it buffered, level-translated or terminated, and for what load?
- Does it leave the board on a connector or header, drive an indicator, or both?
- What edge quality or jitter matters for its intended use, and does the routing preserve it?
- Does routing this output near the RF section compromise the isolation requirement?
- Is there any separate status indication distinct from the timing output, and is that in scope?

## Floorplan and mechanical

- What board outline and dimensions follow from the connector set and the short-RF-path requirement?
- Where does the antenna connector sit on the outline, and what does that force about the receiver's placement?
- What mounting and enclosure assumptions are being made, and are they documented as assumptions rather than requirements?
- Is the RF section on one side of the board only, and what is on the other side beneath it?
- Do the USB-C, UART and timing connectors end up on edges that keep their traces away from the front end?

## Manufacture, assembly and test

- Does the chosen stackup and impedance target fit the intended fabricator's published capability for this layer count?
- Which parts drive the tightest process requirement, and is that acceptable?
- What test points exist for the rails, the antenna bias, and the receiver's outputs?
- How is the RF path's impedance verified — coupon, TDR, or vendor impedance report?
- How is a bare-board or first-article unit brought up and shown to acquire a fix?
- What is the programming or configuration step, if the chosen receiver needs one?

## Answers still owed

All of them. See [status.md](status.md).
