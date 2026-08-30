# Benchmark entry — board 22 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_GNSS_Receiver` |
| Board id | `gnss_receiver` |
| Category | rf-navigation |
| Difficulty | 4 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

At difficulty 4 with a mid-detail (3/5) brief in the rf-navigation category, this board tests whether a design agent can build a defensible RF receive chain — antenna bias, ESD, filtering and low-noise amplification, and controlled-impedance routing — while it still gets to choose the receiver part. The stressors (GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies) mean the grading pressure sits on noise-figure and impedance reasoning and on keeping switching and clock noise off the receive path, not on digital complexity. The brief's phrase "as appropriate to the selected GNSS module/IC" deliberately makes the front-end topology contingent on a part the agent has not chosen yet, so the test is whether the agent derives its front end from the chosen part's datasheet and justifies it in whichever direction it lands — extra discrete stages or none — rather than asserting a topology without reading what the part already integrates.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
