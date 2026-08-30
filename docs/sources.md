# Sources — Precision GNSS Receiver

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| GNSS module or receiver IC datasheet | Fixes RF input impedance and level limits, states what front-end filtering, gain, DC blocking or antenna-bias provision is already integrated, and gives the backup-supply pin's voltage window and retention current — the brief makes the whole front end contingent on this part. |
| LNA datasheet | Gain, noise figure, input/output match, P1dB and supply requirements are needed for any cascaded noise-figure and compression budget, whichever way the discrete-LNA decision lands. |
| SAW/band filter datasheet | Insertion loss in band and rejection at the specific out-of-band aggressors decide whether the filter earns its place and what it costs in noise figure. |
| Active-antenna class specification | The bias feed's voltage and current, and the gain already present ahead of the board, come from the antenna the board must feed — an assumption that has to be stated and sourced. |
| RF ESD protection device datasheet | Shunt capacitance, insertion loss and return loss at the GNSS band determine whether the protection degrades the receive path; clamping and rating determine whether it protects it. |
| Fabricator stackup, impedance and capability documentation | The controlled-impedance claim needs a real dielectric stack, copper weight and trace geometry from a specific vendor stack for the layer count in use, plus trace/space and via minimums and the tolerance the fabricator will actually hold. |
| Regulator and LDO datasheets | Output noise spectral density, PSRR versus frequency, switching frequency and quiescent current back the "quiet supply" argument for the RF rails. |
| Backup energy-storage element datasheet | Capacity, self-discharge or leakage, and charge constraints are required for any retention-duration claim. |
| USB-C connector and USB specification material | Port-role and CC termination rules, current advertisement, and pair impedance and routing rules for whatever USB role the board turns out to take. |
| Bias-network component data for the element chosen (inductor, ferrite, or integrated bias-tee) | Self-resonant frequency, DC current rating and impedance at the GNSS band decide whether the bias path is transparent to RF, whichever element the topology decision selects. |
| GNSS layout and integration application notes | Vendor guidance on keep-outs, ground stitching, shielding practice and separation from switchers and clocks gives a citable basis for the isolation requirement rather than an assertion. |
| RF cascade analysis method references (e.g. Friis noise-figure) | The chain budget has to be computed by a stated method, not asserted, so the noise-figure and gain numbers can be checked. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
