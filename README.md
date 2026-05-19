# COGS 160 — Spring 2026

Hi Prof. Kirsh and TAs — this repo is everything I built for the course this quarter, organized by week. The intended reading order is just top to bottom.

**Student:** Dhruv Sood (`d2sood@ucsd.edu`)
**Track:** Track 2 — Article Finder
**Locked research topic since Week 1:** CO₂ × Decision Quality (K-ATLAS Q16)

A note on layout: my graded Track 2 task code (Tasks 1, 2, 3) does not live inside this repo. It lives in the open Pull Requests on your `Knowledge_Atlas` and `Article_Finder` repos. Each Track-2 week folder here is a short index page that explains what I built and points to the right PR. Everything else (the A0 papers, the Track 1 exercise, the query diary, the Week-4 deliverable bundle) lives directly in this repo with the raw outputs and writeups.

---

## What I did, week by week

### Weeks 1–2 · A0 Collect Articles
→ [`week01-02_A0/`](week01-02_A0/)

Twenty papers across two questions, with APA citations, DOIs, abstracts, PDFs, and per-paper manifests.

- **Q1 (10 empirical):** CO₂ × Decision Quality. Anchored on Satish 2012, Allen 2016, MacNaughton 2015, with newer adds from Young (2024), Bejder & Klausen (2023), Shimazaki (2025). Key instrument: the Strategic Management Simulation (Streufert et al.).
- **Q2 (10, any type):** Circadian-effective lighting × cognitive performance. Mix of experiments (Chellappa 2011, Smolders 2014, Mills 2007), a consensus statement (Brown 2022), the Lucas 2014 melanopsin standardization paper, and the Souman 2018 review of alerting effects.

### Week 2 · Track 1 Exercise D — Evidence Search Filter
→ [`week02_T1_exD/`](week02_T1_exD/)

This was the first AI-directed programming exercise, the Thursday after Prof Kirsh's live demo. I built a client-side filter bar for `ka_evidence.html` that narrows 1,900 K-ATLAS evidence claims by warrant class, credence, topic, status, qualifier, defeat type, study type, support/attack counts, and free-text keyword.

The exercise was less about filter logic than about UX defenses: which filters should be visible by default, and how do you tell a user they're not seeing the whole evidence base? My answer was a persistent "filtered out X of 1,900" counter and progressive disclosure for the rarely-used fields. The full writeup is in `SUBMISSION.md` (and `.pdf`); the five verification screenshots show the four user stories from the spec plus the empty-state case.

### Week 3 · Track 2 Phase 1 — Query Diary
→ [`week03_T2_phase1/`](week03_T2_phose1/)

The first real Track 2 deliverable. The Phase 1 page asked for 15+ Boolean queries, all four AI tools sampled, 8+ Include decisions, and a 500-word reflection. I ended up with 25 queries — 17 Boolean queries actually run through NCBI E-utilities (raw JSON in `search_outputs/`), plus 8 AI-tool queries drafted for PubMed, Elicit, Google AI Scholar, Consensus, and Scholar AI (the AI-tool queries are marked `pending-execution` because each tool needs interactive auth).

The 520-word reflection (`reflection_phase1.md`) is the thing I'd point at first. Short version: Boolean is precise but brittle (`AND` chains lose papers that index the construct under a near-synonym), and natural-language tools are good at finding the *right neighborhood* but quietly drift away from your operationalization. The Include decisions doc records 12 new keepers, bringing the working corpus from 10 → 22.

### Week 4 · Track 2 Phase 2 + Phase 3 kickoff + Deliverables A/B/C
→ [`week04_T2/`](week04_T2/)

Mid-quarter checkpoint. Three things in one folder:

- **Phase 2** — 20 questions across 4 AI tools × 4 topic clusters (C1 CO₂, C2 PM2.5, C3 Ventilation, C4 Thermal/IEQ). Lives in `phase2_question_set/`.
- **Phase 3 kickoff** — 27-paper working corpus + KA-overlap matrix in `phase3_corpus_table/`. The matrix is the start of a recall/precision calculation against KA's automated index.
- **Deliverables A/B/C** — one operational example, end to end, in `deliverable_ABC/`:
  - **A. Real topic run.** Topic C1, run from a single `curl` against PubMed, manifest in `runs/run_manifest.txt`, raw esearch + esummary JSON next to it.
  - **B. Review packet.** Ten records from the run hand-reviewed (5 ACCEPT + 5 BORDERLINE/REJECT) with per-paper reasoning. Two of the borderlines genuinely complicate the K-ATLAS Q16 claim — that's documented honestly, not papered over.
  - **C. Focused repair.** The Q02 query had 80% noise. I dropped `OR SMS` and broadened the second clause; the rerun (`q02_repaired_PM1_2026-05-04.json`) went from 41 hits to 3, noise rate 80% → 0%, and the change pulled one in-canon paper back into range.

If you only read one folder from the first half of the quarter, this is the one.

---

## The three graded Track 2 tasks

These are the actual assignment submissions. The code is on open PRs against your repos, not inside this one. Each week folder below is a one-page index that summarizes what I built and points to the PR.

### Week 5 · Task 1 — Fix the Contribute Page (75 pts)
→ [`week05_T2_task1/`](week05_T2_task1/) · **PR:** [dkirsh/Knowledge_Atlas#1](https://github.com/dkirsh/Knowledge_Atlas/pull/1)

The contribute page accepted PDFs and threw them away. I wired it to a new `POST /api/articles/suggest` endpoint that validates the upload, checks for duplicates (SHA-256, DOI, fuzzy title) *before* any storage, runs the file through `AdaptiveClassifierSubsystem.classify()`, stores ACCEPT and EDGE_CASE papers in quarantine + the lifecycle DB (EDGE_CASE flagged so it's distinguishable later), and reports the verdict back on the page. The frontend results panel uses safe DOM construction (no `innerHTML`) and `prepend`s each new result so multi-submission sessions don't overwrite earlier cards.

The test harness in `data/test_pdfs/validate_task1.py` covers the four rubric test papers plus duplicate handling, bad-file rejection, multi-submission accumulation, and the ambiguous-classifier `needs_more_info` branch — 29 checks, all passing. The Copilot auto-review on the PR caught five real issues during the audit pass (XSS in result rendering, race in article-ID generation, DB connection leak, missing `busy_timeout`, dropped citation/email field on the PDF path) — all fixed in a follow-up commit, documented in `task1_bug_review.md`.

### Week 6 · Task 2 — Gap Targeting & Query Generation (60 + 20 contract bonus)
→ [`week06_T2_task2/`](week06_T2_task2/) · **PR:** [dkirsh/Article_Finder#1](https://github.com/dkirsh/Article_Finder/pull/1) (combined with Task 3)

`gap_extractor.py` walks the canonical PNU mechanism manifest, finds steps below a 0.6 confidence threshold, and scores each gap by VOI (base + centrality bonus + temporal bonus − coverage penalty). It returned 31 gaps across 15 frameworks, sorted highest-VOI first.

`query_generator.py` takes the top 10 by VOI and writes two queries each: a natural-language AI Citation question and a Boolean query with quoted phrases, OR-synonym groups, and `-review`. I added per-gap synonym overrides so cross-framework hubs get domain vocabulary (`interoception`, `circadian rhythm`, `oxytocin`, `cross-modal congruence`) instead of generic fallbacks, and a mediator-fallback so mechanisms without a `→` separator still produce grammatical sentences.

For the manual spot-check I ran three queries against Google Scholar and recorded the top results: the interoception query surfaced *Allostatic interoceptive overload across psychiatric and neurological conditions* (Biological Psychiatry, 2024); the multisensory query surfaced *The multifaceted interplay between attention and multisensory integration*; the morning-light query surfaced *Effects of light on human circadian rhythms, sleep and mood*. All three on-topic.

**Honest substitution:** the rubric points at `Article_Eater/data/templates/`, but that repo's working tree didn't come down on any of my `git checkout` attempts. I used `Knowledge_Atlas/data/ka_payloads/mechanisms.json` (the canonical manifest Article_Eater produces) as the substitute, with `--mechanisms-path` and `--use-voicalculator` flags ready for the swap when Article_Eater is back. This is called out in §0 of `docs/GAP_EXTRACTOR_CONTRACT_TASK2.md`.

### Week 7 · Task 3 — Search Execution & Abstract-First Triage (75 + 20 contract bonus)
→ [`week07_T2_task3/`](week07_T2_task3/) · **PR:** same as Task 2

The full Stage 1 → 2 → 3 pipeline.

I built the `article_references` table (with `REF-YYYY-MM-DD-NNNNNN` IDs, normalized DOI and title, comma-separated `discovered_via` provenance so duplicates merge instead of duplicating rows), a `lifecycle_transitions` audit log, and a `v_acquisition_queue` view that surfaces only ACCEPT rows for PDF retrieval. The schema mirrors the column names in your rubric § 3A verbatim.

The search runner has four backends — SerpAPI on `engine=google_scholar`, `scholarly` as fallback, `paperscraper` for preprints, and a deterministic mock for offline runs. Stage 1 (metadata-only screen on title + venue) rejects ~10% of search noise before any abstract collection happens. Stage 2A walks the Semantic Scholar → CrossRef → PubMed → OpenAlex cascade with proper rate-limiting, never treats a SerpAPI snippet as a full abstract, and tags `MISSING_ABSTRACT` instead of silently dropping. Stage 2B runs the `atlas_shared` classifier + VOI threshold to assign `ACCEPT / EDGE_CASE / REJECT / MISSING_ABSTRACT`, and every row gets a non-empty `triage_reason`.

The PDF cascade is Unpaywall → OpenAlex OA → scidownl. The scidownl step is locked behind a 4-condition policy gate: it requires the `--enable-scidownl` flag *and* a countersigned `policy_clearance.json` in the repo root *and* a DOI *and* the prior cascade exhausted. The clearance file is `.gitignored`; in the default state scidownl simply cannot run. I deliberately did not wire the real scidownl call until you decide; the cascade reports `gated:no_policy_clearance` on every attempt instead.

The PRISMA dashboard reconstructs the entire funnel from a single `GROUP BY` over `article_references` — no parallel state. The canonical demo run shows: 91 records identified → 9 rejected at metadata → 77 abstracts collected (5 MISSING_ABSTRACT) → 77 EDGE_CASE → 0 ACCEPT → 77 included. The 0-ACCEPT count is honest: `question_constitutions_starter.json` ships only `SQ-ART-001 Nature & Attention`, so the mock data scores `edge_case` against that single constitution. Adding more constitutions raises the accept rate without touching the code.

End-to-end trace: I traced `REF-2026-05-08-000002` from the `SOCIAL-AFFILIATION-002` gap through the Boolean query, into the harvest row, through Stage 1, abstract collection, Stage 2B classification (EDGE_CASE, confidence 0.66, hits `green space, biophilic, attention`), and confirmed the PDF cascade correctly did *not* fire because the verdict wasn't ACCEPT. Three `lifecycle_transitions` rows show the audit chain.

`task3/tests_task2_task3.py` covers 25 rubric line items including DOI regex on three sample URLs, env-only SERPAPI key, scidownl-gate refusal paths, MISSING_ABSTRACT-skips-VOI, `v_acquisition_queue` containing only ACCEPT, and PRISMA SQL matching a separate manual GROUP BY. All 25 pass.

---

## Submission status at end of Week 7

All three task PRs are open against `dkirsh:main` from `track2/dhruv-sood`. Nothing is merged — they're waiting on your review.

| Task | PR | Tests | Self-grade |
|---|---|---|---:|
| Task 1 — Fix the Contribute Page | [Knowledge_Atlas#1](https://github.com/dkirsh/Knowledge_Atlas/pull/1) | 29/29 PASS | 75 / 75 |
| Task 2 — Gap + Queries | [Article_Finder#1](https://github.com/dkirsh/Article_Finder/pull/1) | 11/11 PASS · 3/3 spot-checks RUN | 80 / 80 |
| Task 3 — Search + Triage | same PR | 25/25 PASS · PRISMA funnel reconstructed | 95 / 95 |

I want to be upfront about the self-grades — they're estimates, not claims. The contracts are written to be testable against the rubric line-by-line, so each number above is grounded in a specific checklist, but you and the TAs will have the final say.

---

## A few things I want to flag honestly

- **Article_Eater offline.** The repo's working tree didn't come down on my checkouts. I worked around it with the `mechanisms.json` manifest (the canonical Article_Eater output) and re-implemented `calculate_voi()` locally using the documented formula. Both the contract and the gap-extractor docstring call this out as a substitution.
- **One question constitution in `atlas_shared`.** The starter file ships only `SQ-ART-001 Nature & Attention`. That's why the mock-mode Task 3 demo produced 0 ACCEPTs — the data hasn't grown to cover the gaps the queries target. The pipeline is correctly wired; adding more constitutions raises the accept rate.
- **scidownl deliberately not wired.** The four-condition gate is in place and tested, but the real `scihub_download` call is left as a stub returning `miss`. The course rubric flags "scidownl runs by default" as a fatal failure condition; I'd rather be over-cautious here than ship a default that downloads from sci-hub mirrors without your sign-off.
- **The Task 2 spot-check is small.** Three queries × first-page-only. That's the rubric minimum; broader sampling would expose hit-rate variation in the OK-rated queries.

---

## Reproducibility

Every Phase-1/Phase-2/Phase-3/Week-4 claim that depends on an API ships with the exact `curl` invocation and the raw JSON it produced, dated. If PubMed drifts, the drift is the data point. `week04_T2/deliverable_ABC/` is the cleanest example — read its `A_run_report.md` end-to-end if you want a tour of how I document evidence.

For the Track 2 tasks the equivalent is the test harness. `python3 task3/tests_task2_task3.py` runs the rubric checklist end-to-end (25 checks); `python3 data/test_pdfs/validate_task1.py` does the same for Task 1 (29 checks). Both run from a fresh checkout in seconds.

---

## Folder map

| Folder | Week | Description |
|---|---|---|
| [`week01-02_A0/`](week01-02_A0/) | 1–2 | A0 — 20 collected papers, manifests, all PDFs |
| [`week02_T1_exD/`](week02_T1_exD/) | 2 | Track 1 Exercise D — Evidence Search Filter |
| [`week03_T2_phase1/`](week03_T2_phase1/) | 3 | Track 2 Phase 1 — Query Diary + reflection |
| [`week04_T2/`](week04_T2/) | 4 | Track 2 Phases 2 + 3 + Deliverables A/B/C |
| [`week05_T2_task1/`](week05_T2_task1/) | 5 | Task 1 index → Knowledge_Atlas PR |
| [`week06_T2_task2/`](week06_T2_task2/) | 6 | Task 2 index → Article_Finder PR |
| [`week07_T2_task3/`](week07_T2_task3/) | 7 | Task 3 index → same Article_Finder PR |

Thanks for reading. If anything below is unclear, the per-week READMEs go into more detail, and the PRs themselves have the file manifests + commit history + audit-pass notes.

— Dhruv
