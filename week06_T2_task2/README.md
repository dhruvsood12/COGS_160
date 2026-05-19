# Week 6 — Track 2 · Task 2 · Gap Targeting & Query Generation

**Track:** Article Finder · **Task:** 2 of 3 · **Points:** 60 (+ 20 contract bonus = 80 max)
**Status:** ✅ Submitted (PR open on the same branch as Task 3, waiting for instructor review)
**PR:** https://github.com/dkirsh/Article_Finder/pull/1 (combined Tasks 2 + 3 PR)

---

## What this week was about

Week 6 is the middle track-production week. Track 2 shipped **Task 2 — Gap Targeting & Query Generation**: read the Article_Eater PNU mechanism templates, identify low-confidence knowledge gaps, score them by Value of Information (VOI), and turn the top gaps into paired natural-language and Boolean search queries that Task 3 will execute.

---

## What I built

| Component | Where |
|---|---|
| Gap extractor — walks the mechanism manifest, filters by confidence threshold, scores each gap with `compute_voi()` (base + centrality + temporal − coverage) | `track2/Article_Finder/gap_extractor.py` |
| Query generator — emits AI Citation + Boolean queries per gap with `query_quality_flags` and a corpus-awareness check | `track2/Article_Finder/query_generator.py` |
| Ranked gap list (31 gaps over 15 frameworks) | `track2/Article_Finder/gap_results.json` |
| 10 paired queries with `template_id`, `gap_summary`, `query_terms`, `query_quality_flags` | `track2/Article_Finder/query_results.json` |
| Gap extractor contract (with §0 Substitutions preamble) | `docs/GAP_EXTRACTOR_CONTRACT_TASK2.md` |
| Query generator contract (closed-enum `query_quality_flags`, 5-component AI Citation pattern, Boolean rule set) | `docs/QUERY_GENERATOR_CONTRACT_TASK2.md` |
| Manual spot-check (3 queries RUN with top result titles recorded) | `docs/QUERY_SPOT_CHECK_TASK2.md` |
| AI quality review (5 Strong / 5 OK / 0 Weak verdict) | `docs/AI_QUERY_QUALITY_REVIEW_TASK2.md` |
| Submission report | `docs/SUBMISSION_TASK2.md` |

---

## Important substitution (documented honestly in the contract §0)

The rubric points at `Article_Eater/data/templates/` (166 PNU templates) and `Article_Eater/src/services/voi_search.py::VOICalculator.calculate_voi()`. The Article_Eater repo's working tree is unavailable on this checkout (`.git` exists but `git checkout` of `main` produces no files — verified repeatedly).

**Substitute:** `Knowledge_Atlas/data/ka_payloads/mechanisms.json` (71 mechanisms × 15 frameworks) — the canonical manifest Article_Eater produces. VOI scoring re-implemented locally with the documented formula. `--mechanisms-path` and `--use-voicalculator` flags ready for the swap when Article_Eater is back.

---

## Manual spot-check (3/3 queries returned on-topic primary literature)

| # | Gap | Top result on Google Scholar |
|---|---|---|
| 1 | INTERO-PP-ALLOSTASIS-001 | *Allostatic interoceptive overload across psychiatric and neurological conditions* (Biological Psychiatry, 2024) |
| 2 | MULTISENSORY-CONGRUENCE-001 | *The multifaceted interplay between attention and multisensory integration* (PMC3306770) |
| 3 | CIRCADIAN-DEV-PROGRAM-001 | *Effects of light on human circadian rhythms, sleep and mood* (PMC6751071) |

---

## Test results

`python3 task3/tests_task2_task3.py` (Task 2 section) → **11/11 PASS**.

Includes boundary tests (confidence 0.59 included / 0.60 excluded), threshold edge cases (`--confidence-threshold 0.0` returns 0 gaps; `--confidence-threshold 1.0` returns all 71), JSON validity, no-duplicate-template-id, and query shape rules.

---

## Files (where the actual code lives)

```
track2/Article_Finder/
├── gap_extractor.py
├── query_generator.py
├── gap_results.json
├── query_results.json
└── docs/
    ├── GAP_EXTRACTOR_CONTRACT_TASK2.md
    ├── QUERY_GENERATOR_CONTRACT_TASK2.md
    ├── QUERY_SPOT_CHECK_TASK2.md
    ├── AI_QUERY_QUALITY_REVIEW_TASK2.md
    └── SUBMISSION_TASK2.md
```

---

## Self-grade

| Criterion | Earned / Max |
|---|---:|
| Gap extraction | 15 / 15 |
| VOI scoring | 10 / 10 |
| AI Citation queries | 10 / 10 |
| Boolean queries | 10 / 10 |
| Spot-check (3 RUN) | 5 / 5 |
| Verification questions | 10 / 10 |
| **Rubric subtotal** | **60 / 60** |
| Contract bonus | +20 / 20 |
| **Total** | **80 / 80** |
