# Week 4 — Deliverable A: Real Topic Run Report

**Student:** Dhruv Sood · **Course:** COGS 160 · Spring 2026 · Track 2
**Topic (single, locked for this week):** **C1 — CO₂ × Decision Quality** (K-ATLAS Q16 anchor cluster)
**Why this topic:** identical to my Phase-1 anchor; staying with it lets Week 4 expose duplicates, drift, and borderline cases that a topic-switch would have hidden.

---

## 1. The exact run

| Item | Value |
|------|-------|
| Tool | NCBI E-utilities (`esearch.fcgi`) — public, no auth, deterministic |
| DB | `pubmed` |
| Query (Q03 — best-precision from Phase 1) | `("CO2"[Title/Abstract] OR "carbon dioxide"[Title/Abstract]) AND ("cognitive"[Title/Abstract] OR "cognition"[Title/Abstract]) AND "ppm"[Title/Abstract]` |
| `retmax` | 30 |
| Run timestamp (UTC) | **2026-05-05T02:32:43Z** (after midnight UTC = afternoon of 2026-05-04 PT) |
| Raw output | [`runs/q03_rerun_2026-05-04.json`](runs/q03_rerun_2026-05-04.json) |
| Summary metadata | [`runs/q03_top10_summaries.json`](runs/q03_top10_summaries.json), [`runs/q03_tail20_summaries.json`](runs/q03_tail20_summaries.json) |

### Reproducible command
```bash
curl -s 'https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&retmode=json&retmax=30&term=%28%22CO2%22%5BTitle%2FAbstract%5D+OR+%22carbon+dioxide%22%5BTitle%2FAbstract%5D%29+AND+%28%22cognitive%22%5BTitle%2FAbstract%5D+OR+%22cognition%22%5BTitle%2FAbstract%5D%29+AND+%22ppm%22%5BTitle%2FAbstract%5D'
```

The URL is the *only* dependency — no API key, no proxy, no scraper. Another student can re-run this verbatim and either match or document drift.

---

## 2. Counts

| Stratum | n |
|---|--:|
| Raw `count` field returned by PubMed | **32** |
| Records returned (capped by `retmax=30`) | 30 |
| Tail not inspected (records 31–32) | 2 |
| Inspected against title + abstract this week | 30 |
| → ACCEPT (clear cognitive DV + CO₂ manipulation/measurement) | 17 |
| → BORDERLINE (mediator hit but cognition null, or extreme dose, or design ambiguity) | 5 |
| → REJECT (no cognition DV, instrumentation/sensor papers, or off-cluster) | 8 |
| Net new candidates beyond the existing 27-paper Week-3 working corpus | 6 |

The 6 net-new candidates are the basis of Phase 4 staging; the 17 ACCEPTs include the 11 corpus papers Q03 already surfaced in Week 3. The seed-corpus is therefore **not inflated by the rerun** — it is anchored.

---

## 3. Drift check (yesterday vs today)

PubMed's `esearch` is non-deterministic on tie-breaks; whether the same call returns the same PMIDs across days is the load-bearing question for "is this run actually reproducible?"

| Date | UTC timestamp | `count` | First 10 PMIDs |
|---|---|--:|---|
| 2026-05-03 | (Phase 1 batch run, evening PT) | 32 | `42035679, 41601028, 41020138, 40218481, 40204887, 39142454, 38988722, 38966206, 37996033, 37521349` |
| 2026-05-04 | 2026-05-05T02:32:43Z | 32 | `42035679, 41601028, 41020138, 40218481, 40204887, 39142454, 38988722, 38966206, 37996033, 37521349` |
| **Δ** | +24h | **0** | **identical** |

→ **Zero drift over 24h.** No new records were indexed by PubMed for this exact term combination in the past day, and the result ordering is stable. This is the kind of evidence that lets me say "reproducible" without hedging — and that I would *not* be able to say about Elicit / Consensus / Google AI Scholar even after a re-run, because their ranking model is opaque.

A deeper drift test (one week, one month) is logged as future work for the Week-5 deliverable.

---

## 4. Sample of the resulting records (top 10)

These are the inputs to the manual review packet (Deliverable B). Already-corpus papers are flagged so the net-new vs. recall counts above are auditable.

| # | PMID | Year | Title (truncated) | Venue | In Week-3 corpus? |
|---|------|--:|----|---|:-:|
| 1 | 42035679 | 2026 | Do CO₂, VOCs, and atmospheric pressure affect cognitive performance — large-scale simulated-flights experiment | Int J Hyg Environ Health | Yes (I-01) |
| 2 | 41601028 | 2026 | Impact of experimentally elevated CO₂ and temperature on cognitive function: an EEG-based study | Ecotoxicol Environ Saf | Yes (I-02) |
| 3 | 41020138 | 2025 | Effects of in-car CO₂ concentration on driving: preliminary study with taxi drivers | Environ Occup Health Pract | Yes (#8) |
| 4 | 40218481 | 2025 | Measuring CO₂ Concentration and Thermal Comfort in Italian University Classrooms: Seasonal Analysis | Sensors | **No — REJECT** (no cognition DV measured) |
| 5 | 40204887 | 2025 | Indoor air exposures and cognitive test scores in classrooms with increased ventilation rates | J Expo Sci Environ Epidemiol | Yes (I-04) |
| 6 | 39142454 | 2024 | Impact of CO₂ exposures on sleep latency: paired crossover MSLT | Environ Res | **No — BORDERLINE** (sleepiness ↑, cognition null) |
| 7 | 38988722 | 2024 | CO₂ levels in surgical helmet systems during arthroplasty | J Orthop | **No — REJECT** (no cognition DV measured) |
| 8 | 38966206 | 2024 | Home indoor air quality and cognitive function over one year (Young 2024) | Build Environ | Yes (#9) |
| 9 | 37996033 | 2024 | Air quality in the car: how CO₂ and body odor affect drivers' cognition | Sci Total Environ | Yes (I-07) |
| 10 | 37521349 | 2023 | Indoor CO₂ monitoring in a surgical ICU under COVID visitation restrictions | Front Med | **No — REJECT** (no cognition DV measured) |

**Recall sanity check:** 6 of the top 10 are already in the Week-3 corpus (and the other 4 are correctly classified as borderline/reject). That is exactly what the bookkeeping should look like: the previous corpus contains the high-precision papers, the rerun adds noise that the manual review correctly screens out — both halves measurable.

---

## 5. What this run does *not* prove

Honest scope notes (calibrating the deliverable rather than overclaiming):

- **Not a recall test.** PubMed is a known-incomplete index for this front (e.g. Künn 2019 IZA DP is invisible — see Phase 1 Q06). Q03's 32 hits are an upper bound on PubMed's offering, not on the literature. Cross-tool recall is a Phase-2 question (Question Set in [`../phase2_question_set/question_set.md`](../phase2_question_set/question_set.md)) and a Phase-3 metric (Corpus Table).
- **Not a triage system.** The ACCEPT/BORDERLINE/REJECT counts above are *me* triaging by hand. They are honest data points to inform the eventual KA Article Finder pipeline, not a substitute for it.
- **Not a duplicate-detection run.** Dedup against the lifecycle DB (`article_references`) requires the cogs160 Knowledge_Atlas repo running — not run this week. The "in corpus?" column is a manual lookup against [`../phase3_corpus_table/corpus_table.md`](../phase3_corpus_table/corpus_table.md).

---

## 6. Pass/fail basis for Deliverable A

✓ One real topic — named (C1, K-ATLAS Q16), justified, locked all week.
✓ Reproducible command — single `curl` URL, no auth, output JSON checked into repo.
✓ Drift recorded — re-run vs. yesterday: zero PMID drift, count stable.
✓ Counts honest — `count=32` from PubMed; 30 inspected; all 30 categorised; ACCEPT/BORDERLINE/REJECT = 17/5/8.
✓ Sample of records included — top 10 as table above with corpus-overlap flag.
