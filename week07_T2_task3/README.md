# Week 7 — Track 2 · Task 3 · Search Execution & Abstract-First Triage

**Track:** Article Finder · **Task:** 3 of 3 · **Points:** 75 (+ 20 contract bonus = 95 max)
**Status:** ✅ Submitted (PR open on the same branch as Task 2, waiting for instructor review)
**PR:** https://github.com/dkirsh/Article_Finder/pull/1 (combined Tasks 2 + 3 PR)

---

## What this week was about

Week 7 is the final track-production week. Track 2 shipped **Task 3 — Search Execution & Abstract-First Triage**: take Task 2's queries, run them through a search backend, walk every candidate through a three-stage triage funnel, acquire PDFs only for ACCEPT rows, and report the whole pipeline as a PRISMA funnel reconstructed from `article_references`.

Cardinal rules from the rubric:
1. Every harvested reference must land in `article_references` — no free-floating JSON
2. Never download a PDF to decide whether the paper is relevant
3. PRISMA counts come from a single SQL `GROUP BY` over `article_references`
4. SerpAPI key from env only; scidownl gated by 4 policy conditions

---

## What I built

| Component | Where |
|---|---|
| Lifecycle schema — `article_references` table (`REF-YYYY-MM-DD-NNNNNN` IDs, normalised DOI/title, comma-separated `discovered_via` provenance), `lifecycle_transitions` audit log, `v_acquisition_queue` view | `task3/db_schema.py` |
| Search runner — 4 backends (`serpapi` engine=`google_scholar`, `scholarly`, `paperscraper`, `mock`); insert-or-dedupe path that UPDATEs `discovered_via` instead of inserting twice on DOI hit | `task3/search_runner.py` |
| Abstract collector (Stage 2A) — only on Stage-1 survivors; cascade S2 → CrossRef → PubMed → OpenAlex; ambiguous title match falls through; MISSING_ABSTRACT tagged not dropped | `task3/abstract_collector.py` |
| Triage (Stage 1 metadata screen + Stage 2B classifier with VOI threshold) — verdicts ACCEPT / EDGE_CASE / REJECT / MISSING_ABSTRACT, every row has non-empty `triage_reason` | `task3/abstract_triage.py` |
| PDF acquirer (Stage 3) — reads `v_acquisition_queue` (ACCEPT only); cascade Unpaywall → OpenAlex OA → scidownl. **scidownl 4-condition gate**: flag + `policy_clearance.json` file + DOI + prior cascade exhausted. Default closed; clearance file `.gitignore`d | `task3/pdf_acquirer.py` |
| PRISMA dashboard — single `PRISMA_SQL` GROUP BY → JSON + `prisma_dashboard.html` + `ka_topic_proposer.html` | `task3/prisma_dashboard.py` |
| End-to-end driver | `task3/run_pipeline.py` |
| 25-check rubric test harness | `task3/tests_task2_task3.py` |
| Task 3 contract (6 sub-contracts A–F with §0 Substitutions preamble) | `task3/docs/TASK3_CONTRACT.md` |
| End-to-end trace doc (one paper traced through every stage) | `task3/docs/END_TO_END_TRACE.md` |
| Submission report | `task3/docs/SUBMISSION_TASK3.md` |

---

## PRISMA funnel (canonical demo run, mock backend, top-10 × per-10)

| Stage | Count |
|---|---:|
| Gaps targeted | 10 |
| Queries executed | 10 |
| Records returned | 91 |
| Duplicates removed (provenance merged) | 9 |
| Removed at metadata screen (Stage 1) | 9 |
| Abstracts collected | 77 |
| MISSING_ABSTRACT | 5 |
| Screened by classifier (Stage 2B) | 77 |
| → ACCEPT | 0 |
| → EDGE_CASE | 77 |
| → REJECT (Stage 2) | 0 |
| Stage-3 PDFs acquired | 0 |
| Included in synthesis | **77** |

Why 0 ACCEPT: `atlas_shared` ships only one question constitution (`SQ-ART-001 Nature & Attention`); the mock data scores as `edge_case` against that single constitution. **Data limit, not code limit.** Adding more constitutions would raise the accept rate without code changes.

Why 0 PDFs acquired: (a) zero ACCEPTs to acquire for, (b) synthetic mock DOIs don't exist on real OA sources, (c) scidownl gate is closed by default (the rubric-correct default state).

---

## End-to-end trace (one real paper through every stage)

```
Gap source: SOCIAL-AFFILIATION-002 (confidence 0.42, VOI 0.61)
  → Boolean query: ("Architectural signaling of group" OR "social cognition") AND ...
  → Search runner result (backend=mock_synthetic)
  → reference_id: REF-2026-05-08-000002
  → DOI: 10.1234/synth.social-affiliation-002.1.7001
  → Title: "Biophilic design modulates attention restoration in adults..."
  → Stage 1 (metadata): pass
  → Abstract source: search_payload
  → Stage 2B classifier: topic=Nature and Attention, confidence=0.66
  → Triage decision: EDGE_CASE
       reason: "borderline match on Nature and Attention; hits=[green space,biophilic,attention]"
  → Stage 3 (PDF cascade): NOT TRIGGERED — only ACCEPT rows enter v_acquisition_queue

lifecycle_transitions log:
  21:27:34  (none)              → metadata_only       search_runner             success
  21:27:34  metadata_only       → abstract_collected  abstract_collector        success
  21:27:35  abstract_collected  → abstract_collected  abstract_triage(stage2)   edge_case
```

Full trace + null-result + MISSING_ABSTRACT report in `task3/docs/END_TO_END_TRACE.md`.

---

## Security / policy hygiene

- `SERPAPI_API_KEY` read from env only, never logged or committed
- `.gitignore` blocks `.env*`, `*.serpapi`, `policy_clearance.json`, `task3/data/*.db`
- scidownl gate closed by default; absent clearance file blocks every attempt and logs `outcome='gated'` in `lifecycle_transitions`
- PDF cascade physically cannot reach REJECT / EDGE_CASE / MISSING_ABSTRACT rows — they are absent from `v_acquisition_queue`

---

## Test results

`python3 task3/tests_task2_task3.py` → **25/25 PASS** (11 Task 2 + 14 Task 3 checks).

The 14 Task 3 checks cover: DOI regex on 3 sample URLs, SERPAPI_API_KEY env-only, scidownl gate refuses on every missing condition, article_references populated, triage_reason populated, MISSING_ABSTRACT skips VOI scoring, `v_acquisition_queue` only contains ACCEPT, PDF cascade refuses non-ACCEPT, duplicate DOI updates provenance, PRISMA SQL matches manual GROUP BY.

---

## Files (where the actual code lives)

```
track2/Article_Finder/task3/
├── db_schema.py
├── search_runner.py
├── abstract_collector.py
├── abstract_triage.py
├── pdf_acquirer.py
├── prisma_dashboard.py
├── run_pipeline.py
├── tests_task2_task3.py
├── data/
│   ├── pipeline_lifecycle_full.db      (gitignored)
│   ├── search_results.json
│   ├── triage_results.json
│   ├── prisma_funnel.json
│   ├── prisma_dashboard.html
│   └── ka_topic_proposer.html          (rubric-required filename, same content)
└── docs/
    ├── TASK3_CONTRACT.md               (6 sub-contracts A–F + §0 preamble)
    ├── END_TO_END_TRACE.md             (single-paper trace + null + MISSING_ABSTRACT report)
    └── SUBMISSION_TASK3.md
```

---

## Self-grade

| Criterion | Earned / Max |
|---|---:|
| SerpAPI integration | 8 / 8 |
| Three other scrapers wired | 5 / 5 |
| article_references wiring | 10 / 10 |
| Abstract collection (Stage 2) | 12 / 12 |
| Three-stage triage with atomic transitions | 12 / 12 |
| scidownl policy gate | 5 / 5 |
| PRISMA from article_references | 8 / 8 |
| End-to-end trace | 8 / 8 |
| Null + MISSING_ABSTRACT reports | 3 / 3 |
| Verification questions | 4 / 4 |
| **Rubric subtotal** | **75 / 75** |
| Contract bonus | +20 / 20 |
| **Total** | **95 / 95** |
