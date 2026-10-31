# 3D Lenses — concept brief

*Chart the Common Wealth, 31 Oct 2026 · Team **CommonSpace** · Priority track: B, "The Passage"*

**Live demo:** https://egornikot.github.io/mass-ai-atlas/atlas3d.html ·
**Code:** [`atlas3d.html`](../atlas3d.html) (one file, no build step) ·
**Pull request:** [holzerjm/mass-ai-atlas#79](https://github.com/holzerjm/mass-ai-atlas/pull/79)

## The problem

The Atlas records its own doubt: `approx`, `lastVerified`, missing `stages`, missing
`links`, funders with no check size, deadlines that only say "rolling". None of it reaches
the map. An exact address and a neighborhood guess look the same. A founder walking between
three Kendall labs is reading an estimate drawn as a fact. The connections exist only inside
the Galaxy, away from the geography.

## What it does

**Credibility lens.** Every entry gets a 0–100 reading computed from its own fields. Each of
the six doubt signals in the brief takes points off: an approximate pin, the verification
month, no founder stage, no connections, a funder with no check size, and a deadline that is
rolling, dated or passed. Two signals found while building are added: entries that share
exact coordinates (on the main map one pin hides the other), and links that only one side
lists.

- *On the map:* green, amber or red. A hollow ring means an approximate pin, with a soft halo
  for the area it could be in. Pins fade as their verification gets older.
- *On the card:* a **Before you act** box tells the founder what each doubt should change
  ("get the street address before you plan a visit", "ask about their typical check before
  you pitch"). Below it, every signal links to **the exact line** in `data/entities.yml` that
  supports it.
- *Honesty:* the reading is labelled as computed, not as a verification. Event mentions are
  labelled as an inferred name match.

**Connections lens.** The Galaxy's links are drawn as arcs on the real map. Links between two
areas merge into one arc, and a thicker arc means more links. Grey arcs are listed by one side
only. Selecting an organization shows just its network; ← → walks through it.

**3D and readability.** Tilt and rotate the map. Columns rise for credibility or for
connections. Buildings appear from street zoom and hillshade shows relief statewide.

- Crowded areas group into bubbles named after their neighborhood (Kendall Sq, Seaport…).
  They split as you zoom, and labels never overlap.
- The legend works as a filter: click a category to show only it, click more to add, and
  clear them all to show everything.

## Why it matters

A founder should know *before* they act which parts of an entry to double-check. The confident
entries stay confident; the doubtful ones say exactly what is doubtful and what to do next. For
the maintainer, the "Least certain entries" list is a review queue, and "Suggest a fix" opens
the existing flag form, so nothing is written to the data without a human.

## Morning numbers made visible

The side panel counts each probe live from the data, and every one is drawn on the map:
approximate pins (rings), verified June or earlier (faded), no stage, no links of their own,
connected to nothing either way, funders with no check size, and rolling / dated deadlines.

## Data sources

| Source | Used for |
|---|---|
| `data/*.yml` — Mass AI Atlas, The Open Accelerator (CC BY 4.0) | every entry, link, date and fact |
| the-open-accelerator.com/ecosystem/events.json | "active this month" (inferred name match; optional) |
| OpenFreeMap / OpenMapTiles / OpenStreetMap contributors | basemap, 3D buildings |
| AWS Open Data terrain tiles (Mapzen terrarium) | hillshade |

There are no API keys, no scraping and no writes. `data/entities.yml` is untouched.

## What it refuses to do

- It never edits data. Fixes go through the flag issue form for a maintainer to review.
- It never shows a computed score as a verification, or a name match as a confirmed event.
- It never invents an organization or a connection. Every pin and arc comes from the data.

## Try it

`python3 -m http.server`, then open `/atlas3d.html`. Add `?entry=<id>` to open any
organization directly, for example `?entry=liquid` (Liquid AI).

*Dataset: Mass AI Atlas, The Open Accelerator — the-open-accelerator.com/ecosystem (CC BY 4.0).
Map data © OpenStreetMap contributors via OpenFreeMap. Code MIT.*
