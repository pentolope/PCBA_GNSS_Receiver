# PCBA_GNSS_Receiver — Precision GNSS Receiver
## Design brief

Create a GNSS receiver board with an external active-antenna connector, ESD protection, bias feed, SAW/filtering and low-noise amplification as appropriate to the selected GNSS module/IC. Provide USB-C and UART output, backup supply for ephemeris/RTC retention, and status timing output. The RF path from antenna to receiver must be short, impedance controlled, and isolated from digital clocks and switching regulators.

## Functional requirements

- The UART shall carry navigation output whenever the board is powered, without USB enumeration; USB shall carry it with no UART host attached.
- Receiver status shall be observable on the board, and the timing output shall reach an external connection point undegraded by that indication.

## Antenna port, bias and RF front end

- One external 50 Ω coaxial connector, its launch matched to the board's 50 Ω trace structure.
- Bias shall be fed on the centre conductor through a network that is high impedance across every band received; a shorted antenna or cable shall be non-destructive and shall not collapse a shared rail.
- SAW and LNA stages shall be added where the selected module's own front end does not meet its data-sheet noise figure and rejection with the intended antenna, and omitted where it does.
- ESD protection shall sit at the connector ahead of everything else, its capacitance low enough not to degrade the front end in band.

## Power, rails and backup supply

- Rails feeding the receiver and front end shall be filtered so their noise does not degrade the module's specified sensitivity.
- Switching fundamentals and harmonics shall be clear of the bands received, or attenuated below the receiver's in-band noise floor.
- The backup supply shall hold the RTC and ephemeris domain for a stated retention time, within the element's rated limits, without back-feeding the main rail.

## Interfaces and connectors

- The USB-C receptacle shall present device terminations on both CC pins so the port works in either orientation, with ESD protection at the receptacle.
- USB data shall run as a matched 90 Ω pair, stub-free, over a continuous reference plane.

## Layout and isolation

- The antenna-to-receiver path shall be the shortest routable run over an unbroken reference plane, with no split, void or crossing trace beneath it.
- Oscillators, clock traces, USB pairs, switching nodes and inductors shall be kept out of the RF region, off the layers beneath it, and as far from the antenna connector as the outline allows.

## Test and bring-up access

- Every rail, the antenna bias at the connector, the timing output and both UART lines shall be probeable without rework, and the bias shall be isolatable without permanent modification.

## Open choices

- GNSS module or IC and the bands covered, which set bias voltage, the need for external SAW/LNA, and the front-end budget.
- Whether USB is native to the receiver or bridged from the UART, and whether the board is powered from VBUS, an external input, or both.
