# Precision GNSS Receiver

Precision GNSS Receiver: a GNSS receiver board with an external active-antenna connector (ESD, bias feed, SAW/filtering, LNA), USB-C and UART output, backup supply, and status timing output.

This repository holds the design problem for PCBA_GNSS_Receiver, the "Precision GNSS Receiver" board of the benchmark, built around a GNSS module or receiver IC that the design agent selects. The brief fixes the interfaces and the RF discipline: an external active-antenna connector with ESD protection and a bias feed, SAW/filtering and low-noise amplification "as appropriate to the selected GNSS module/IC", USB-C and UART output, a backup supply for ephemeris/RTC retention, and a status timing output. It also fixes one hard layout constraint — the antenna-to-receiver RF path must be short, impedance controlled, and isolated from digital clocks and switching regulators — and the header's stressor list names 50-ohm routing as the impedance the routing is judged against. Everything else is open: the receiver part itself, whether discrete LNA/SAW stages are actually needed, how the antenna bias is fed and whether DC has to be blocked before the receiver input, the connector families, the power tree, the stackup, geometry and impedance tolerance, the board outline, and the backup-supply element. Those choices belong to the design agent and must be made and documented from datasheets, not assumed here.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 14 requirements and deliberately leaves
18 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Repository / board title | PCBA_GNSS_Receiver (title: Precision GNSS Receiver) | metadata |
| Board function | GNSS receiver board | brief |
| Category | rf-navigation | metadata |
| Difficulty | 4 / 5 | metadata |
| Brief detail | 3 / 5 | metadata |
| Likely layer count | 4 | metadata |
| Primary stressors | GNSS RF chain; 50-ohm routing; LNA/filter; quiet supplies | metadata |
| Antenna interface | External active-antenna connector, with ESD protection and a bias feed | brief |
| RF front end | SAW/filtering and low-noise amplification, scoped to whatever the selected GNSS module/IC needs | brief |
| Host / data interfaces | USB-C and UART output | brief |
| Backup supply | Backup supply for ephemeris/RTC retention | brief |
| Timing output | Status timing output | brief |
| RF path constraint | Antenna-to-receiver path must be short, impedance controlled, and isolated from digital clocks and switching regulators | brief |
| Impedance named in the source | 50-ohm routing, named in the brief header's primary-stressor list (no tolerance, geometry or stackup stated anywhere) | brief |
| GNSS module / receiver IC | Not fixed by the brief — the design agent selects the part, and the front-end topology follows from it | open |
| Board outline, size, mounting | Not fixed by the brief — design agent's choice | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 22 of 32 |
| Category | rf-navigation |
| Difficulty | 4 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies |

At difficulty 4 with a mid-detail (3/5) brief in the rf-navigation category, this board tests whether a design agent can build a defensible RF receive chain — antenna bias, ESD, filtering and low-noise amplification, and controlled-impedance routing — while it still gets to choose the receiver part. The stressors (GNSS RF chain, 50-ohm routing, LNA/filter, quiet supplies) mean the grading pressure sits on noise-figure and impedance reasoning and on keeping switching and clock noise off the receive path, not on digital complexity. The brief's phrase "as appropriate to the selected GNSS module/IC" deliberately makes the front-end topology contingent on a part the agent has not chosen yet, so the test is whether the agent derives its front end from the chosen part's datasheet and justifies it in whichever direction it lands — extra discrete stages or none — rather than asserting a topology without reading what the part already integrates.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_GNSS_Receiver.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `72965c43b536d3ab1db18566af96177416b5d1071563a091fe58c896983c146d`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
