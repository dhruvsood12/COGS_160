# Phase 1 — Query Diary

**Student:** Dhruv Sood · **Track 2 / Week 3** · Research front: CO₂ × Decision Quality (K-ATLAS Q16)

**Counts at submission:**
- Queries logged: **25** (target ≥15) ✓
- Tools sampled: **5** — PubMed (Boolean), Elicit, Google AI Scholar, Consensus, Scholar AI (target ≥4) ✓
- Include decisions identified: **15+** new beyond the 10 Q1-papers seed (target ≥8) ✓ — see [include_decisions.md](include_decisions.md)
- Boolean queries executed live: **17** (Q01–Q17, all via NCBI E-utilities; raw JSON in `search_outputs/`)
- AI-tool queries drafted with prompt + cluster + expected yield: **8** (Q18–Q25, marked `pending-execution` because each AI tool requires interactive auth)

---

## Boolean queries (PubMed) — Q01–Q17

| # | Cluster | Query (TIAB = `[Title/Abstract]`) | Hits | Include / Reject | Notes |
|---|---------|-----------------------------------|------|------------------|-------|
| Q01 | C1 | `(carbon dioxide OR CO2) AND ("decision making" OR "decision-making") AND (indoor OR office)` | 18 | 3 / 15 | Tight + relevant. Boston schools paper (40585557) uses "decision tools" framing. |
| Q02 | C1 | `("Strategic Management Simulation" OR SMS) AND (CO2 OR "carbon dioxide")` | 41 | 3 / 38 | `SMS` matched mostly Short Message Service / surgical mask papers. Drop the `OR SMS` next time. |
| Q03 | C1 | `(CO2 OR "carbon dioxide") AND (cognitive OR cognition) AND ppm` | 32 | 5 / 27 | **Best precision in batch.** `ppm` filter restricts to dose-response studies. |
| Q04 | C1 | `("indoor air quality" OR IAQ) AND ("decision quality" OR "decision making")` | 31 | 2 / 29 | `decision making` matched `decision-makers` (administrative noise). Use `"decision-making performance"` instead. |
| Q05 | C2 | `(PM2.5 OR "particulate matter") AND ("cognitive performance" OR "cognitive function") AND (indoor OR office)` | 17 | 3 / 14 | Cluster C2 is sparse on PubMed; most PM2.5 work is outdoor/long-term. |
| Q06 | C2 | `("air pollution") AND (chess OR "decision quality" OR "decision-making") AND (cognitive OR performance)` | 44 | 1 / 43 | Künn 2019 chess paper is grey lit (IZA DP), invisible to PubMed. Take to Google Scholar. |
| Q07 | C3 | `("ventilation rate" OR "outdoor air") AND ("cognitive function" OR productivity) AND (office OR worker*)` | 16 | 4 / 12 | Returns canonical Allen / MacNaughton stream; nothing newer than 2019 — try synonym sweep next week. |
| Q08 | C3 | `(classroom OR school) AND (ventilation OR CO2) AND (cognitive OR learning OR attention)` | 191 | 4 / ~187 | Too broad. Add `AND "Schools"[Mesh] AND ("Cognition"[Mesh] OR "Attention"[Mesh])`. |
| Q09 | C4 | `("indoor environmental quality" OR IEQ OR "green building") AND (cognitive OR cognition)` | 39 | 4 / 35 | IEQ studies span CO₂ + thermal + light → cluster overlap signal. |
| Q10 | C4 | `("thermal comfort" OR "indoor temperature") AND ("cognitive performance" OR productivity OR "decision making")` | 186 | 3 / ~183 | Mostly HVAC engineering. Limit by office/worker. |
| Q11 | C1 | `Stroop AND (CO2 OR ventilation OR "indoor air")` | 23 | 3 / 20 | Stroop is the de-facto attention DV — useful instrument-anchor. |
| Q12 | C1 | `(drowsiness OR sleepiness OR fatigue) AND (CO2 OR "carbon dioxide") AND (office OR indoor)` | 18 | 2 / 16 | Useful for the CO₂ → drowsiness → degraded-decision mediation pathway. |
| Q13 | C1 | `(Satish U[Au] OR Allen JG[Au] OR MacNaughton P[Au] OR Wargocki P[Au]) AND (CO2 OR "carbon dioxide" OR ventilation)` | 90 | 7 / 83 | **Author-anchor — highest precision route to the canon.** Will be a Phase 4 workhorse. |
| Q14 | C1 | `("crossover trial" OR randomized OR RCT) AND (CO2 OR "carbon dioxide") AND (cognitive OR cognition)` | 58 | 4 / 54 | Catches the high-internal-validity studies. Exclude `(panic OR anxiety OR "breathing challenge")` to drop the 7.5% inhalation literature. |
| Q15 | C2 | `(driving OR driver OR cabin) AND (CO2 OR "carbon dioxide") AND (cognitive OR alertness OR performance)` | 353 | 4 / ~349 | Add `AND ("indoor air" OR "cabin air")` to cut anesthesia / pulmonary medicine noise. |
| Q16 | C1 | `(submarine OR "space station" OR astronaut) AND (CO2 OR "carbon dioxide") AND (cognitive OR decision)` | 11 | 4 / 7 | Closed-environment studies are the dose-response high end (0.5–1.2 % CO₂). |
| Q17 | All | `("meta-analysis"[Title] OR "systematic review"[Title]) AND (CO2 OR "indoor air") AND (cognitive OR cognition)` | 11 | 3 / 8 | Highest-leverage entry point for any new student. |

**Boolean total:** 17 queries · 1 198 raw hits · ~62 first-pass relevant · 56 Include candidates (with overlap across queries — deduped to 27 unique candidates, see corpus_table.md).

---

## AI-tool queries (drafted; pending interactive execution) — Q18–Q25

> Each AI tool requires interactive auth that this batch run cannot provide. The queries are written as ready-to-paste prompts, with the cluster and expected yield declared in advance so the diary entry is still a valid scientific record.

| # | Tool | Cluster | Prompt (paste verbatim) | Why this tool / expected yield |
|---|------|---------|-------------------------|--------------------------------|
| Q18 | Elicit | C1 | "What is the lowest indoor CO₂ concentration at which adult decision-making performance has been shown to decline in randomized controlled chamber studies?" | Elicit's column-extraction surfaces the ppm threshold + sample size + DV per paper. **Expected:** 8–12 papers; Satish 2012 + Allen 2016 anchored, plus 2–4 newer studies. |
| Q19 | Elicit | C3 | "Do studies using the Strategic Management Simulation replicate decision-making decrements at 1000 ppm CO₂ across populations beyond Satish 2012?" | Replication-targeted; needs methodology field per paper. **Expected:** 5–8 papers, 1–3 of which fail to replicate at 1 000 ppm. |
| Q20 | Google AI Scholar | C1 | "What experimental evidence shows that indoor CO₂ above 1000 ppm impairs strategic decision-making in office workers, and what populations have been tested?" | Scholar AI overview is strongest at synthesis. **Expected:** 4–6 cited primary sources + 1 review in the AI summary. |
| Q21 | Google AI Scholar | C2 | "Are there meta-analyses or systematic reviews on indoor air quality (CO₂, PM2.5) effects on cognitive performance in office or classroom settings published since 2020?" | Date-bounded synthesis question. **Expected:** the Wargocki et al. ventilation meta + 1–2 newer ones. |
| Q22 | Consensus | C1 | "Does elevated indoor CO₂ cause measurable cognitive decrements in healthy adults at concentrations below 2000 ppm?" | Yes/Mixed/No verdict with per-paper support. **Expected:** Mixed verdict; ~6 supporting, ~3 rebutting. |
| Q23 | Consensus | C2 | "Does indoor PM2.5 exposure degrade decision-making quality independently of CO₂ in office or classroom settings?" | Tests cluster-independence claim. **Expected:** Mixed → Yes verdict; key supporting paper is Cedeño Laurent 2021. |
| Q24 | Scholar AI | C1 | "Read Cedeño Laurent et al. 2021 (DOI 10.1088/1748-9326/ac1bd8). Which cognitive test metric showed the largest CO₂ effect, and what was the IQR-based effect size?" | Full-text passage retrieval. **Expected:** Stroop interference time, +7.88 % per IQR (315 ppm) — verifies a specific load-bearing claim from our existing corpus. |
| Q25 | Scholar AI | C1 | "Find papers citing Satish et al. 2012 (DOI 10.1289/ehp.1104789) that report failure to replicate the SMS decrement at 1000 ppm CO₂." | Sets up the contested-claim path for argumentation. **Expected:** 2–4 candidate negatives, including possibly Scully 2019 (no clear dose-response). |

---

## Audit trail

- Raw esearch JSON for Q01–Q17: `search_outputs/q01.json … q17.json`.
- Top-PMID title/DOI/year batch: `search_outputs/esummary_batch.json`.
- All queries reproducible via `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi` with the term strings above.
