# Week 5 — Track 2 · Task 1 · Fix the Contribute Page

**Track:** Article Finder · **Task:** 1 of 3 · **Points:** 75
**Status:** ✅ Submitted (PR open, waiting for instructor review)
**PR:** https://github.com/dkirsh/Knowledge_Atlas/pull/1

---

## What this week was about

Per the course schedule, Week 5 is the first track-production week. Every track ships **Task 1** with a PR due end of week.

For Track 2, Task 1 was **"Fix the Contribute Page"**: the public PDF upload page on the Knowledge Atlas accepted submissions but did nothing with them — no classification, no storage, no feedback. The job was to wire it end-to-end and prove it works with at least four test papers.

---

## What I built

| Component | Where |
|---|---|
| New backend endpoint `POST /api/articles/suggest` | `track2/Knowledge_Atlas/ka_article_endpoints.py` |
| Frontend results panel (async fetch, multi-submit stacking, XSS-safe DOM) | `track2/Knowledge_Atlas/ka_contribute_public.html` |
| Classifier integration via `AdaptiveClassifierSubsystem.classify()` | wired through existing `_classify_article_payload()` wrapper |
| Duplicate probe (SHA-256 + DOI + fuzzy title) before any storage | `_suggest_check_dup()` in same file |
| Storage rules (ACCEPT → quarantine + DB row + audit; EDGE_CASE → same + `edge_flag`; REJECT → response only, no storage; `needs_more_info` for ambiguous classifier output) | same endpoint |
| Test harness (29 checks, in-process FastAPI TestClient) | `track2/Knowledge_Atlas/data/test_pdfs/validate_task1.py` |
| 4 test PDFs (on-topic, off-topic, edge-case, duplicate) | `track2/Knowledge_Atlas/data/test_pdfs/` |
| Contract: Classifier Integration Contract | `track2/Knowledge_Atlas/docs/CLASSIFIER_INTEGRATION_CONTRACT_TASK1.md` |
| Submission report (boxology + gap statement + verification log + storage proof + diagnosis) | `track2/Knowledge_Atlas/docs/SUBMISSION_TASK1.md` |
| Audit-pass docs (bug review, security review, validation matrix, completion checklist, file manifest, PR summary) | `track2/Knowledge_Atlas/docs/task1_*.md` |

---

## Test results

`python3 data/test_pdfs/validate_task1.py` → **29/29 PASS**

Two layers:
- **Layer A** (6 checks): classifier-only smoke test on the 4 rubric-required test papers
- **Layer B** (23 checks): live in-process endpoint test that asserts file on disk + DB row + audit row for ACCEPT/EDGE_CASE rows; asserts no row + no file for REJECT/bad-file/duplicate rows

---

## Audit passes (Copilot + self-review caught real bugs)

| # | Bug | Fix |
|---|---|---|
| 1 | XSS via filename / PDF title in result rendering | Switched to `document.createElement` + `textContent` |
| 2 | Race condition in `_suggest_next_id` (`COUNT(*)+1`) | Random `secrets.token_hex(4)` with uniqueness retry |
| 3 | DB connection leak on exception | `try / except (rollback) / finally (close)` |
| 4 | Concurrent-write "database is locked" errors | `PRAGMA busy_timeout=5000` |
| 5 | `email` + `citation` dropped on PDF path | Persisted into `validation_notes` JSON |
| 6 | Endpoint bypassed canonical `AdaptiveClassifierSubsystem.classify()` | Refactored to use the existing `_classify_article_payload()` wrapper; added `next_action` + `evidence_stage` to response; added `needs_more_info` verdict for `need_abstract_or_keywords` |

---

## Files (where the actual code lives)

Not duplicated here — they're in the open PR on the `Knowledge_Atlas` fork.

```
track2/Knowledge_Atlas/
├── ka_article_endpoints.py            (added /api/articles/suggest endpoint)
├── ka_contribute_public.html          (wired the form, added results panel)
├── data/test_pdfs/
│   ├── validate_task1.py              (29/29 test harness)
│   ├── test_ontopic_empirical.pdf
│   ├── test_offtopic_ml.pdf
│   └── test_edgecase_theory.pdf
├── docs/
│   ├── CLASSIFIER_INTEGRATION_CONTRACT_TASK1.md
│   ├── SUBMISSION_TASK1.md
│   ├── task1_completion_checklist.md
│   ├── task1_bug_review.md
│   ├── task1_security_review.md
│   ├── task1_validation_matrix.md
│   ├── task1_file_manifest.md
│   └── task1_pr_summary.md
└── PR_DRAFT_TASK1.md
```

---

## Self-grade

| Criterion | Earned / Max |
|---|---:|
| Diagnosis | 15 / 15 |
| Spec quality | 20 / 20 |
| Verification questions | 15 / 15 |
| Validation (4 papers) | 15 / 15 |
| Diagnosis of failures | 5 / 5 |
| File manifest | 5 / 5 |
| **Total** | **75 / 75** |
