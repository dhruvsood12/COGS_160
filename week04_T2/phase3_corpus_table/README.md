# Week 4 · Phase 3 (kickoff) — Corpus Table & KA Overlap

**Phase 3 deliverable:** Recall / precision table comparing the manual Track-2 corpus against KA's automated pipeline. Target: 50 papers assessed, 25+ Include, KA overlap measured.

## Status at kickoff

| Metric | Current | Target | Note |
|---|--:|--:|---|
| Corpus size (Include) | **27** | 25+ ✓ | Target met at start of Phase 3 |
| Papers assessed (Include + Reject + Edge) | **52** | 50+ ✓ | From Phase-1 query diary `decision_count` |
| KA overlap measured | 10 Y / 0 N (Q1 only); 17 pending verification | full 27 | Requires KA Article Search lookup per row |
| New to KA — staged for intake | 0 | per Phase 4 (≥150 records over Weeks 6–7) | Not yet staged |

## Files

| File | Purpose |
|---|---|
| [`corpus_table.md`](corpus_table.md) | 27-paper corpus + 8 Reject/Edge examples + recall/precision metric design |

## Methodology note (per [Track 2 Week 5 page](../../track2/Knowledge_Atlas/160sp/track2_week_5.html))

- **In KA?** is determined by querying KA's Article Search by DOI. The 10 Q1 papers (already in A0_collect_articles) are presumed `Y`; the 17 Phase-1 new finds are presumed `N` until verified — that's the recall metric.
- **Pipeline would find?** asks whether KA's automated AI-Citation / Boolean queries would surface the paper. Heuristic: does the abstract contain the canonical KA Q16 vocabulary (CO₂, ventilation, decision quality, cognition, ppm, office, classroom, IEQ, IAQ, Stroop, SMS)?

## Deferred to Week 5

- DOI-by-DOI lookup of all 17 unverified rows against the KA Article Search index
- Running the KA automated pipeline (or its query bank) against the C1 research front and counting overlap
