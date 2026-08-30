# PCBA_GNSS_Receiver — Precision GNSS Receiver

**Benchmark ID:** 22  
**Difficulty:** 4/5  
**Brief detail:** 3/5  
**Category:** rf-navigation  
**Likely layer count:** 4  
**Primary stressors:** GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies

## Design brief

Create a GNSS receiver board with an external active-antenna connector, ESD protection, bias feed, SAW/filtering and low-noise amplification as appropriate to the selected GNSS module/IC. Provide USB-C and UART output, backup supply for ephemeris/RTC retention, and status timing output. The RF path from antenna to receiver must be short, impedance controlled, and isolated from digital clocks and switching regulators.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
