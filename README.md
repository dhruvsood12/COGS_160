# COGS 160 · Spring 2026 · Course Repository

**Student:** Dhruv Sood (dhruv@sood.me · d2sood@ucsd.edu)
**Course:** COGS 160 — Cognitive Science Senior Seminar (Prof. David Kirsh, UCSD)
**Track:** Track 2 — Article Finder (the discovery half of the Knowledge Atlas pipeline)
**Repo:** [`dhruvsood12/COGS_160`](https://github.com/dhruvsood12/COGS_160) (default branch: `main`)

This repo holds my **course writeups, weekly deliverables, and submitted artifacts** for COGS 160. The actual Track 2 *code* (Article Finder pipeline, Knowledge Atlas site fixes) lives in nested git forks under [`track2/`](track2/) which are **not** tracked by this repo.

---

## Folder map (by week)

| Folder | Week(s) | Track | What it contains |
|---|---|---|---|
| [`week01-02_A0/`](week01-02_A0/) | 1–2 | T2 prep | **A0 Collect Articles** — 20 verified papers (10 Q1: CO₂×Decision Quality / K-ATLAS Q16; 10 Q2: Circadian Lighting × Cognition). Manifests, APA citations, queries, all 20 PDFs, submission checklist, A0 Q1 checklist PDF. |
| [`week02_T1_exD/`](week02_T1_exD/) | 2 | T1 | **Track 1 · Exercise D — Evidence Search Filter.** Working `filter.html`, real K-ATLAS `evidence.json` (1,900 records), 5 verification screenshots, full submission writeup (md + pdf). |
| [`week03_T2_phase1/`](week03_T2_phase1/) | 3 (3.5) | T2 | **Track 2 · Phase 1 — Query Diary.** 17 live PubMed Boolean queries + 8 AI-tool queries drafted across 5 tools, 12 new Include decisions, ~520-word reflection on Boolean vs. natural-language search. Raw NCBI esearch JSON in `search_outputs/`. |
| [`week04_T2/`](week04_T2/) | 4 | T2 | **Track 2 · Week 4** — Phase 2 question set (20 questions, 4 tools × 4 clusters), Phase 3 corpus-table kickoff (27 papers + KA-overlap matrix), and the Week-4 deliverable bundle (A: real topic run, B: review packet, C: focused repair). |
| [`week05_T2_task1/`](week05_T2_task1/) | 5 | T2 | **Track 2 · Task 1 — Fix the Contribute Page** (75 pts). New `/api/articles/suggest` endpoint, frontend results panel, classifier integration via `AdaptiveClassifierSubsystem.classify()`, dup probe + storage logic + 29/29 test harness. **PR open** at `dkirsh/Knowledge_Atlas#1`. Self-grade 75/75. |
| [`week06_T2_task2/`](week06_T2_task2/) | 6 | T2 | **Track 2 · Task 2 — Gap Targeting & Query Generation** (60 + 20 contract bonus). 31 VOI-ranked gaps, 10 paired AI Citation + Boolean queries, 3 manual Google Scholar spot-checks RUN, AI quality review (5 Strong / 5 OK / 0 Weak). **PR open** at `dkirsh/Article_Finder#1` (combined with Task 3). Self-grade 80/80. |
| [`week07_T2_task3/`](week07_T2_task3/) | 7 | T2 | **Track 2 · Task 3 — Search Execution & Abstract Triage** (75 + 20 contract bonus). `article_references` table + lifecycle log, 4-backend search runner, abstract collector (S2 → CrossRef → PubMed → OpenAlex), three-stage triage funnel, gated PDF cascade, PRISMA dashboard from one SQL GROUP BY. PRISMA: 91 → 77 included. 25/25 tests PASS. Same PR as Task 2. Self-grade 95/95. |
| [`track2/`](track2/) | 5–7 (active) | T2 | **External cloned forks** of `Article_Finder`, `Knowledge_Atlas`, `atlas_shared` — each has its own `.git` and is gitignored from this repo. This is where the actual Task 1/2/3 code lives. See [`track2/README.md`](track2/README.md). |

---

## Course timeline

```
2026 Spring quarter
│
├─ Week 1–2  ─ A0 Collect Articles                  → week01-02_A0/
├─ Week 2    ─ Track 1 Exercise D (Evidence Filter) → week02_T1_exD/
├─ Week 3.5  ─ Track 2 Phase 1 (Query Diary)        → week03_T2_phase1/
├─ Week 4    ─ Track 2 Phase 2 + Phase 3 kickoff
│              + Week-4 deliverable bundle          → week04_T2/
├─ Week 5    ─ Track 2 Task 1 (Fix Contribute Page) → week05_T2_task1/  ✅ PR open
├─ Week 6    ─ Track 2 Task 2 (Gap + Queries)       → week06_T2_task2/  ✅ PR open
└─ Week 7    ─ Track 2 Task 3 (Search + Triage)     → week07_T2_task3/  ✅ PR open
```

All three Track 2 PRs are open on `track2/dhruv-sood` against `dkirsh:main`:
- **Task 1** — [`dkirsh/Knowledge_Atlas#1`](https://github.com/dkirsh/Knowledge_Atlas/pull/1)
- **Tasks 2 + 3** — [`dkirsh/Article_Finder#1`](https://github.com/dkirsh/Article_Finder/pull/1) (combined, same branch)

Neither merged — instructor reviews when ready.

---

## Track 2 submission status (end of Week 7)

| Task | Points | Self-grade | Status |
|---|---:|---:|---|
| Task 1 — Fix the Contribute Page | 75 | **75 / 75** | PR open, 29/29 tests PASS |
| Task 2 — Gap Targeting & Query Generation | 60 + 20 | **80 / 80** | PR open, 11/11 tests PASS, 3/3 manual spot-checks RUN |
| Task 3 — Search Execution & Triage | 75 + 20 | **95 / 95** | PR open, 25/25 tests PASS, PRISMA funnel reconstructed |
| **Track 2 total** | **250** | **250 / 250** (estimate) | All submitted by end of Week 7 |

---

## Active research front

**C1 — CO₂ × Decision Quality** (K-ATLAS Q16 anchor cluster). Locked since Week 1. Adjacent clusters (C2 PM2.5, C3 Ventilation, C4 Thermal/IEQ) carry one question each per tool to maintain breadth.

Anchor authors: Satish, Allen, MacNaughton, Wargocki, Herbig, Cedeño Laurent, Young.
Key instrument: Strategic Management Simulation (SMS) — Streufert et al.
Active dose-response question: at what indoor CO₂ ppm does strategic decision-making decline, and is the threshold lower for cognitively demanding vs. routine tasks?

Working corpus: 27 papers (week04_T2/phase3_corpus_table/corpus_table.md). Recall/precision against KA's automated index: pending Week 5.

---

## Reading order for a new collaborator

1. Start with [`week01-02_A0/README.md`](week01-02_A0/README.md) — the literature you're working with.
2. Then [`week03_T2_phase1/README.md`](week03_T2_phase1/README.md) — how the queries were built and what was learned about Boolean-vs-natural-language search.
3. Then [`week04_T2/README.md`](week04_T2/README.md) — the operational example: one topic, one reproducible run, one review packet, one repair.
4. Then [`week05_T2_task1/README.md`](week05_T2_task1/README.md) → [`week06_T2_task2/README.md`](week06_T2_task2/README.md) → [`week07_T2_task3/README.md`](week07_T2_task3/README.md) — the three Track 2 task submissions.
5. Cross-reference [`track2/README.md`](track2/README.md) for the external code repos where the Task 1/2/3 code actually lives.

---

## What's tracked vs. what isn't

**Tracked in this repo** (you can `git log` to see history):
- All `week01-02_A0/`, `week02_T1_exD/`, `week03_T2_phase1/`, `week04_T2/` content (writeups, manifests, PDFs, raw search JSON, screenshots)
- `week05_T2_task1/`, `week06_T2_task2/`, `week07_T2_task3/` — week-by-week index READMEs that point to the Task 1/2/3 code in the external forks (the code itself is NOT in this repo; it lives in the open PRs on the `dkirsh/*` repos)
- `README.md`, `.gitignore`

**Not tracked** (per `.gitignore`):
- `track2/Article_Finder/`, `track2/Knowledge_Atlas/`, `track2/atlas_shared/` — nested forks with their own remotes
- `.claude/` (local Claude Code config), `.DS_Store`, `__pycache__/`, `*.egg-info/`, `.venv/`, `*.zip`

---

## Reproducibility commitment

Every claim in this repo that depends on an API (PubMed, NCBI E-utilities) ships with the exact `curl` command that produced it and the raw JSON output, dated and timestamped. If the API drifts, the drift is itself the data point. No screenshots-as-evidence, no "trust me" hit counts.

The Week-4 deliverable bundle is the canonical example: see [`week04_T2/deliverable_ABC/`](week04_T2/deliverable_ABC/).
