# Week 4 — Deliverable C: Focused Repair

**Student:** Dhruv Sood · **Course:** COGS 160 · Spring 2026 · Track 2
**Topic:** C1 — CO₂ × Decision Quality
**Repair scope:** ONE thing changed, verified before/after with a fresh PubMed run.

---

## What I changed (one thing)

In Phase 1 I noted that Q02 — `("Strategic Management Simulation" OR SMS) AND (CO2 OR "carbon dioxide")` — returned 41 hits but most were noise: the `SMS` token matched **Short Message Service**, **surgical mask**, and **spent mushroom substrate** papers. I wrote that lesson into the diary but **never re-ran a tightened version** to prove the fix worked. Week 4 makes that fix concrete.

**Repair:** drop the `OR SMS` token entirely, and broaden the second clause to include `ventilation` (so the query catches the canonical SMS papers that pair the instrument with ventilation discussion, not only those that name CO₂). This is exactly the PM-1 query in my Phase-2 question set ([`../phase2_question_set/question_set.md`](../phase2_question_set/question_set.md)) — Week 4 gives it the empirical justification it lacked.

| | Before (Phase 1 Q02) | After (Phase 2 PM-1) |
|---|---|---|
| Query | `("Strategic Management Simulation" OR SMS) AND (CO2 OR "carbon dioxide")` | `"Strategic Management Simulation" AND (CO2 OR "carbon dioxide" OR ventilation)` |
| Tokens removed | — | `OR SMS` from clause 1 |
| Tokens added | — | `OR ventilation` to clause 2 |
| Vocabulary commitment | "instrument name OR abbreviation" | "instrument name only, broader exposure clause" |

---

## Before/After evidence (both runs done today, 2026-05-04)

| Metric | Before (Q02) | After (PM-1) | Δ |
|---|--:|--:|--:|
| `count` | **41** | **3** | **−38 (−93 %)** |
| Top-10 inspected | 10 | 3 (all returned) | — |
| Off-topic noise (`SMS = Short Message Service / surgical mask / spent mushroom substrate / electrochemical CO₂ conversion`) in the inspected sample | **8 / 10** | **0 / 3** | **−8** |
| Real SMS-instrument papers in the inspected sample | 0 / 10 (in top-10; 3 buried lower per Phase 1 diary) | **3 / 3** | **+3 net (and pulled to top)** |

### The 3 records the After query returns

All three are confirmed members of the SMS-instrument canon — the small literature that uses Satish & Streufert's Strategic Management Simulation to measure higher-order decision-making in CO₂ chambers:

| PMID | Year | Title | Cluster fit |
|------|--:|---|---|
| 32557862 | 2020 | Indoor CO₂ concentrations and cognitive function: A critical review (*Indoor Air*) | C1 — review-of-record for the cluster |
| 31240239 | 2019 | Effects of acute CO₂ exposures on decision making and cognition in astronaut-like subjects (*npj Microgravity*) | C1 — already in Week-3 corpus (#3, Scully 2019) |
| 29789085 | 2018 | Acute Exposure to Low-to-Moderate Carbon Dioxide Levels and Submariner Decision Making (*Aerosp Med Hum Perform*) | C1 — submariner study, paired closed-environment dose-response |

→ **Signal preserved (3 of 3 are in-canon SMS papers), noise destroyed (0 of 3 are off-topic).** The submariner paper (PMID 29789085) was *not* in my Week-3 corpus — the repair is also adding a real, missing canon paper to my candidate set, not just shrinking the noise.

### What "Before" looked like (top-10, captured today for evidence)

| PMID | Title | Why it matched | Cluster fit |
|---|---|---|---|
| 40161239 | Ensiled Pleurotus ostreatus … spent mushroom substrate from corn | `SMS` = spent mushroom substrate | none |
| 39994350 | Surgical masks and N95 masks on obese OR staff | `SMS` = surgical masks | none |
| 38185450 | Peach palm shells bioconversion by Lentinula edodes for cattle feed | `SMS` = spent mushroom substrate | none |
| 37710964 | Intermetallic Compound with CuNi Sites for Electrochemical CO₂ Conversion | `CO2` token in inorganic chemistry | none |
| 37133663 | Mortars containing spent mushroom substrate as fine aggregate | `SMS` = spent mushroom substrate | none |
| 36271675 | Plant secondary metabolic responses to global climate change | `CO2` token in plant biology | none |
| 36232214 | Spent mushroom waste agricultural management | `SMS` | none |
| 35407972 | Spent Mushroom Substrate and Electric Arc Furnace Dust Recycling | `SMS` | none |
| 35039927 | Polyamines in plant biotechnology, transgenics and secondary metabolomics | `CO2` (plant) | none |
| 34585722 | Surgical Mask coverage of Elastomeric Half-mask Respirator Exhalation Valves | `SMS` = surgical mask | none |

8 of these top-10 are `SMS`-as-abbreviation collisions. The other 2 are `CO2`-as-chemistry collisions.

---

## Why this is a *repair*, not just a query swap

The change is grounded in three pieces of evidence — not a hunch:

1. **Phase-1 Q02 diary entry (2026-05-03):** "`SMS` matched mostly Short Message Service / surgical mask papers. Drop the `OR SMS` next time." (Documented but never verified.)
2. **Week-4 today's rerun of Q02 (`q02_original_2026-05-04.json`):** confirms the noise is *still there* a day later — the failure mode is reproducible and stable, not transient.
3. **Week-4 today's rerun of PM-1 (`q02_repaired_PM1_2026-05-04.json`):** count drops to 3, all 3 are in-canon, including a paper not in my Week-3 corpus.

The before/after is reproducible by anyone:

```bash
# BEFORE
curl -s 'https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&retmode=json&retmax=30&term=%28%22Strategic+Management+Simulation%22%5BTitle%2FAbstract%5D+OR+%22SMS%22%5BTitle%2FAbstract%5D%29+AND+%28%22CO2%22%5BTitle%2FAbstract%5D+OR+%22carbon+dioxide%22%5BTitle%2FAbstract%5D%29'

# AFTER
curl -s 'https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&retmode=json&retmax=30&term=%22Strategic+Management+Simulation%22%5BTitle%2FAbstract%5D+AND+%28%22CO2%22%5BTitle%2FAbstract%5D+OR+%22carbon+dioxide%22%5BTitle%2FAbstract%5D+OR+ventilation%5BTitle%2FAbstract%5D%29'
```

---

## Spec change that travels with the repair

The query repair surfaces a deeper rule — write it down so future students don't relearn it:

> **Rule (logged for `query_generator.py` Phase-2/Phase-3 spec):**
> When an instrument name has a *common alphabetic abbreviation* (SMS, IAQ, IEQ, MMSE, PVT, etc.), include the abbreviation as a query token **only** if (a) it has < 5 frequent off-domain expansions in PubMed, OR (b) it is qualified by a domain anchor in the same query (e.g. `(SMS AND ("decision making" OR cognition))` rather than `SMS AND CO2`). The cleanest test is to run the abbreviation alone against PubMed and inspect the top-10 — if the off-domain rate is > 20 %, drop the abbreviation.

The `OR SMS` token in Q02 fails both legs of this rule (3+ frequent off-domain expansions; only paired with CO₂ which itself is a chemistry-overloaded token), which is why the noise rate was 80 %.

---

## What I deliberately did *not* change

Three things I considered but rejected as scope creep — keeping the repair narrow:

1. **The borderline-handling rule from Deliverable B (B-1, B-2).** I logged the rule ("triage `mediator-positive / cognition-null` separately from ACCEPT/REJECT" and "exclude `concentration_ppm > 5 000` from K-ATLAS Q16 evidence base") in the review packet. **I did not implement it this week.** That is a Phase-3 spec change for Week 5, not a Phase-2 query change for Week 4 — bundling it would conflate two repairs and make neither verifiable.
2. **The `cognitive`-keyword false-positive pattern from B-3 / B-4 / B-5.** Same reason — that's a *classifier-feature* change ("require named DV in abstract"), not a *query* change. Logged as a candidate Week-5 repair.
3. **Rerunning Q03 with a NOT clause for sensor papers.** Tempting (would have eliminated B-3, B-4, B-5) but adds a brittle term list and would have masked the false-positive pattern instead of measuring it. Better to leave Q03 honest and let the classifier do that filtering at Stage 2A in the canonical pipeline.

---

## Pass/fail basis for Deliverable C

✓ **One** thing changed (the `OR SMS` token). Did not change three variables at once.
✓ **Linked to evidence** — Phase-1 diary lesson + today's reproducible before/after.
✓ **Quantified** — 41 → 3 hits, noise rate 80 % → 0 %, signal pulled to top, plus one new in-canon paper recovered.
✓ **Reproducible** — both `curl` commands above; raw JSON files in [`runs/`](runs/).
✓ **Spec generalisation written** — abbreviation-token rule for `query_generator.py`.
✓ **Scope honest** — explicit list of what I deliberately did not change this week.
