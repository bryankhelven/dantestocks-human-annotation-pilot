# DANTEStocks-Dominant — Pilot404 Selection Protocol (SOURCE+UD) v1.0

## Scope

This protocol materializes the 404-post developmental human pilot directly from two layers that precede the new dominant-affect task:

1. the canonical **UD Portuguese-DANTEStocks** universe (exactly 4,042 `sent_id`s, including train/dev/test membership);
2. the **original DANTEStocks emotion annotation tables** (4,517-row source/provenance layer), joined by stable tweet ID.

The pilot selection therefore does **not** depend on the current Operational SILVER label as a sampling variable. This avoids selecting or balancing items using the very derived layer that the human study will later evaluate.

## Size

- total: **404** (~10% of 4,042)
- representative/simple: **300**
- challenge: **104**

The two strata are coordinator metadata and are never shown in the annotation interface.

## Representative/simple 300

Quotas are proportional to the full 4,042 universe over:

`ud_split × source_group`

Source groups:

- `SOURCE_SINGLETON`
- `SOURCE_MULTILABEL`
- `SOURCE_CLEAR_NEUTRAL`
- `SOURCE_UNRESOLVED`

Largest-remainder allocation closes the quotas at exactly 300. Within each quota cell, items with fewer challenge signals are preferred; seeded random tie-breaking avoids deterministic ordering artifacts.

Seed: `20260901404`.

## Challenge 104

Selected from the remaining 3,742 posts using hidden source/text discovery signals. Signals are not gold labels; they are sampling aids.

Signals include:

- source unresolved;
- original multilabel (especially 3+ labels);
- low original annotation agreement/confidence metadata;
- quoted/retweeted material;
- questions/rhetorical constructions;
- laughter/pragmatic markers;
- explicit irony/sarcasm markers;
- short/underspecified posts;
- technical/numeric density;
- graphic/punctuation phenomena;
- possible neutral-boundary cases.

A deterministic greedy procedure prioritizes high multi-signal cases while improving coverage across challenge types, source groups and UD splits.

Seed: `20260901405`.

## Source visibility

For selected items with usable original labels (source singleton, source multilabel or clear neutral), visibility is assigned approximately 50/50 between:

- `BLIND_9`
- `SOURCE_AWARE_9`

Randomization is stratified by sample stratum × source group.

Seed: `20260901406`.

Items without usable original labels are necessarily `BLIND_9` and are excluded from any causal comparison of source visibility.

`SOURCE_AWARE_9` shows only the original label(s) as provenance and **never constrains the 9-way response space**. Original confidence values are not shown.

## Annotator order

All A1/A2/A3 receive the same 404 post IDs and the same visibility condition for a given post. Only item order changes:

- A1: `20260901411`
- A2: `20260901412`
- A3: `20260901413`

## Never exposed in the app

- original confidence values;
- Operational SILVER dominant label;
- evidence spans/status;
- model rationales;
- challenge/representative stratum;
- challenge tags/scores;
- another annotator's decisions.

## Reproducibility

The exact implementation is `scripts/build_pilot404.py`.

The builder refuses to continue unless:

- UD has exactly 4,042 unique posts;
- all UD IDs join to both original source tables;
- sample has 300 + 104 = 404 unique IDs;
- A1/A2/A3 contain exactly the same 404 IDs;
- blind items contain no `source_annotation` key;
- source-aware items contain only original label(s) + explanatory note.

Coordinator-only outputs are written under `coordinator_private/` and excluded from GitHub Pages deployment.
