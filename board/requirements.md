# Requirements — Precision GNSS Receiver

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `72965c43b536d3ab1db18566af96177416b5d1071563a091fe58c896983c146d`.

## Fixed by the brief

### REQ-01 — The board is a GNSS receiver.

Brief text:

> Create a GNSS receiver board with an external active-antenna connector

### REQ-02 — Provide a connector for an external active antenna (the antenna is off-board and, being active, needs DC power from this board).

Brief text:

> Create a GNSS receiver board with an external active-antenna connector

### REQ-03 — Provide ESD protection on the antenna port.

Brief text:

> an external active-antenna connector, ESD protection, bias feed

### REQ-04 — Provide a bias feed that powers the external active antenna. How the bias is injected and routed to the antenna is not fixed by the brief (see OPEN-06).

Brief text:

> external active-antenna connector, ESD protection, bias feed, SAW/filtering

### REQ-05 — Provide SAW/filtering and low-noise amplification in the receive chain, scoped and justified against what the selected GNSS module/IC actually requires.

Brief text:

> SAW/filtering and low-noise amplification as appropriate to the selected GNSS module/IC

### REQ-06 — Provide USB-C output. The brief lists USB-C alongside UART as output, so USB-C carries data rather than power alone; it names no USB speed class, port role or CC arrangement.

Brief text:

> Provide USB-C and UART output, backup supply for ephemeris/RTC retention

### REQ-07 — Provide a UART output.

Brief text:

> Provide USB-C and UART output, backup supply for ephemeris/RTC retention

### REQ-08 — Provide a backup supply that retains ephemeris/RTC state when the main supply is removed.

Brief text:

> Provide USB-C and UART output, backup supply for ephemeris/RTC retention, and status timing output.

### REQ-09 — Provide a status timing output.

Brief text:

> backup supply for ephemeris/RTC retention, and status timing output.

### REQ-10 — Keep the RF path from the antenna connector to the receiver short.

Brief text:

> The RF path from antenna to receiver must be short, impedance controlled

### REQ-11 — Make the antenna-to-receiver RF path impedance controlled; the source material names 50-ohm routing as the impedance in play, while stating no tolerance or geometry.

Brief text:

> **Primary stressors:** GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies

### REQ-12 — Isolate the antenna-to-receiver RF path from digital clocks and from switching regulators.

Brief text:

> must be short, impedance controlled, and isolated from digital clocks and switching regulators

### REQ-13 — Where the brief leaves a choice open, make and document a reasonable engineering decision rather than inventing an unstated user requirement.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements

### REQ-14 — Keep this repository a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Which GNSS receiver to use — a pre-certified module versus a bare receiver IC — and which specific part.

The brief refers only to "the selected GNSS module/IC" and never names or constrains a part; it explicitly defers the choice to the designer.

*Decision:* **not yet made.**

### OPEN-02 — Which constellations, frequency bands and single- versus multi-band operation the receiver must support.

The brief calls the board "GNSS" without naming constellations or bands, and states no accuracy, fix-time or sensitivity target.

*Decision:* **not yet made.**

### OPEN-03 — Whether a discrete external LNA and/or SAW filter is actually required, how many stages, and their order relative to each other and to the ESD device.

The brief affirmatively lists "SAW/filtering and low-noise amplification" but qualifies them "as appropriate to the selected GNSS module/IC", so the topology is contingent on a part not yet chosen — the module may already integrate some or all of it, or may require all of it externally.

*Decision:* **not yet made.**

### OPEN-04 — Antenna connector family, gender, mount style and orientation (edge versus vertical).

The brief requires "an external active-antenna connector" but names no connector type or mechanical arrangement.

*Decision:* **not yet made.**

### OPEN-05 — ESD protection device class, capacitance budget and its placement in the RF path.

The brief names ESD protection as something to handle and says nothing about the device, its capacitance, or the ESD level to survive.

*Decision:* **not yet made.**

### OPEN-06 — Bias-feed topology — how DC reaches the antenna (over the RF conductor via a choke/ferrite/integrated bias-tee, on a separate conductor, or from a bias pin the chosen part provides), whether a DC block is needed ahead of the receiver input, the bias voltage and current, and whether short-circuit/over-current protection or bias sensing is included.

The brief requires a "bias feed" only, with no injection method, no blocking arrangement and no protection named; the antenna's bias voltage and current draw are properties of an antenna the brief does not specify.

*Decision:* **not yet made.**

### OPEN-07 — How the required USB-C output is realised — native receiver USB, or a USB-to-serial bridge — which USB-C port role the board therefore takes, the CC termination that role requires, and any USB data-rate class.

The brief requires "USB-C and UART output" but does not say how the USB data path is produced, and names no USB speed, port role or CC arrangement.

*Decision:* **not yet made.**

### OPEN-08 — UART electrical level and physical presentation: logic-level versus transceiver-driven, connector or header type, pinout, default baud rate and message format.

The brief requires "UART output" and fixes no level, connector, pin order or rate.

*Decision:* **not yet made.**

### OPEN-09 — Backup supply element (primary cell, rechargeable cell, supercapacitor, or host-supplied rail), its charge/isolation circuit, and the retention duration to design for.

The brief requires a "backup supply for ephemeris/RTC retention" but names no element, no retention time, and no charging behaviour.

*Decision:* **not yet made.**

### OPEN-10 — Electrical form of the status timing output: what signal it carries, whether it is buffered or level-translated, and whether it lands on an LED, a header, or a connector.

The brief requires a "status timing output" and defines neither the signal nor the physical interface.

*Decision:* **not yet made.**

### OPEN-11 — Power architecture: input source(s), rail voltages and count, LDO versus switching regulator per rail, sequencing, and how "quiet supply" is achieved and measured for the RF section.

The brief is silent on power topology, input sources and voltages; it constrains only that switching regulators must be isolated from the RF path.

*Decision:* **not yet made.**

### OPEN-12 — Stackup and geometry that realise the controlled impedance: dielectric materials and heights, copper weights, which layer carries the RF trace, reference-plane assignment, trace/gap geometry, and the impedance tolerance to hold.

The brief body says only "impedance controlled" and states no tolerance; the header's stressor list names 50-ohm routing, so the impedance in play is identified, but no stackup, dielectric height, copper weight, trace geometry or tolerance is given anywhere, and metadata supplies only a likely layer count of 4.

*Decision:* **not yet made.**

### OPEN-13 — Board outline, dimensions, mounting-hole pattern, connector edge placement and any enclosure or keep-out constraints.

Neither the brief nor the metadata states any mechanical dimension or mounting requirement.

*Decision:* **not yet made.**

### OPEN-14 — Whether any local MCU, configuration storage, or host processing exists on the board at all, versus a receiver that talks straight out over USB-C/UART.

The brief describes interfaces and an RF chain but never mentions a controller or firmware.

*Decision:* **not yet made.**

### OPEN-15 — Shielding strategy: shield can or fence over the RF section, ground-stitch pitch, guard structures, and RF keep-out extent.

The brief demands isolation from clocks and switchers but prescribes no mechanism for achieving it.

*Decision:* **not yet made.**

### OPEN-16 — Test, bring-up and RF verification provisions: test points, RF measurement access, programming/debug interface, and how the impedance and isolation claims will be checked.

The brief says nothing about test access or verification method.

*Decision:* **not yet made.**

### OPEN-17 — Operating environment: temperature range, supply-input range, and any EMC/regulatory regime the board must meet.

The brief states no environmental, supply or compliance conditions.

*Decision:* **not yet made.**

### OPEN-18 — Assembly process constraints: single- versus double-sided placement, minimum package sizes, and any hand-assembly or panelisation requirements.

The brief imposes no process or DFM constraints.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Stating a sensitivity, noise figure or time-to-first-fix number without a stage-by-stage cascade computed from actual datasheet gain, NF and insertion-loss values.
- Bolting on a discrete LNA and SAW filter reflexively — or omitting them — without reading what the selected module already integrates on its RF input; the brief says "as appropriate to the selected" part, so an unjustified front end fails either way.
- Claiming controlled 50-ohm routing — the impedance the stressor list names — without naming a stackup, dielectric height, copper weight and trace geometry from a real fabricator stack, and without checking that the connector launch and component pads preserve it.
- Asserting an antenna bias voltage and current with no stated antenna assumption; or leaving the bias network's RF behaviour, the question of whether DC must be blocked before the receiver input, and the shorted-or-absent-antenna case undecided and undocumented rather than resolved either way.
- Putting an ESD device on the antenna port and calling its loading "negligible" without its capacitance and in-band insertion-loss numbers.
- Declaring the RF path "isolated from digital clocks and switching regulators" as a floorplan assertion, with no separation distance, keep-out, shielding, return-path or switcher-harmonic argument behind it.
- Claiming a retention time for the backup supply without both the receiver's backup current and the leakage of the isolation and charging path.
- Treating the status timing output as a generic status LED, or specifying its electrical behaviour before establishing what the chosen receiver actually drives on that pin.
