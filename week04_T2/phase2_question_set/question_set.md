# Phase 2 — Question Set (20 well-formed questions)

**Student:** Dhruv Sood · **Track 2 / Week 4** · Submission to shared question queue

**Targets met:**
- Total questions: **20** (target = 20) ✓
- Per tool: **5 each** across Google AI Scholar, Elicit, Consensus, PubMed/Boolean (target = 5) ✓
- Topic clusters covered: **4** — C1 CO₂ × Decision Quality, C2 PM2.5 × Cognition, C3 Ventilation × Office Productivity, C4 Thermal/IEQ × Cognitive Performance (target ≥ 4) ✓

**Tool-routing principle (from Phase 1 reflection):** Boolean is for *canon* (controlled-vocabulary, anchor-author, instrument-name searches with verifiable hit counts). Natural-language tools are for *frontier* (cross-domain analogy, contested-claim, replication-failure searches). Each question is routed to the tool whose retrieval mechanism best matches its question shape.

---

## Tool A · Google AI Scholar (5 questions)

> **Best for:** broad synthesis, citation chaining, "what does the literature collectively say" framing. Output: AI overview paragraph + cited primary sources. Use when the question is a *synthesis question* that no single paper answers.

| # | Cluster | Question | Why this tool / expected yield |
|---|---------|----------|--------------------------------|
| GS-1 | C1 | What experimental evidence shows that indoor CO₂ above 1 000 ppm impairs strategic decision-making in adult office workers, and which populations have been tested? | Synthesis question across 6+ chamber studies; AI overview should aggregate Satish 2012 + Allen 2016 + Scully 2019 + Herbig 2026 + 1–2 newer. **Expected yield:** 5–8 cited primary sources, of which ≥3 already in corpus. |
| GS-2 | C2 | Are there meta-analyses or systematic reviews on indoor air quality (CO₂, PM2.5) effects on cognitive performance in office or classroom settings published since 2020? | Date-bounded synthesis; Boolean would also work but Scholar's date filter + AI overview is faster. **Expected:** 2–4 SRs (Kuramochi 2023 confirmed; possibly 1–2 newer). |
| GS-3 | C3 | What is the dose-response relationship between outdoor-air ventilation rate and worker cognitive performance, and at what ventilation rate do returns diminish? | Cross-paper dose-response question — the frontier where no single study has the full curve. AI overview should attempt to stitch one. **Expected:** 4–6 cites; high probability of LO returning canonical Allen / Wargocki / Fisk papers. |
| GS-4 | C4 | How does combined exposure to elevated indoor temperature *and* elevated CO₂ affect cognitive performance compared to either factor alone? | Interaction question rarely asked in Boolean form. **Expected:** 2–3 papers (Yang 2026 EEG study confirmed; possibly Lan, Zhao, Wargocki). Likely surfaces a knowledge gap → high VOI. |
| GS-5 | C1 | What papers cite Satish et al. 2012 (Environmental Health Perspectives) and report null or contradictory results? | Citation-chain question targeting *failure to replicate*. AI overview should flag any negative results in the citation forward-cone. **Expected:** 2–4 candidates; Scully 2019 likely surfaces. |

---

## Tool B · Elicit (5 questions)

> **Best for:** comparative extraction across papers (effect size, sample size, study design, instrument used). Output: structured table with one row per paper. Use when you need *cross-paper comparison* on a defined set of fields.

| # | Cluster | Question | Why this tool / expected yield |
|---|---------|----------|--------------------------------|
| EL-1 | C1 | What is the lowest indoor CO₂ concentration at which adult decision-making performance has been shown to decline in randomized controlled chamber studies? | Threshold question; Elicit's column-extraction surfaces ppm + DV per paper. **Expected:** 8–12 papers with extracted thresholds; consensus near 1 000 ppm with outliers (Scully 2019 null at 1 200; Satish 2012 hit at 1 000). |
| EL-2 | C1 | Do studies using the Strategic Management Simulation replicate decision-making decrements at 1 000 ppm CO₂ across populations beyond Satish 2012? | Replication-targeted; needs *methodology* extracted per paper. **Expected:** 5–8 SMS-using studies; mixed replication record. |
| EL-3 | C3 | What effect sizes have been reported for the relationship between mechanical-ventilation rate (cfm/person) and Stroop or n-back performance in office settings? | Effect-size aggregation across studies; Elicit's structured output makes this tractable. **Expected:** 6–10 papers, effect sizes 5–15 % per ventilation doubling. |
| EL-4 | C2 | Across longitudinal observational studies of office workers, what effect size has been reported for IQR-increase in PM2.5 on Stroop response time? | Direct replication target for Cedeño Laurent 2021 (already in corpus, +0.82 % per IQR). **Expected:** 3–5 papers; possible heterogeneity by region. |
| EL-5 | C4 | What experimental studies have measured cognitive performance under combined perturbations of indoor CO₂, temperature, *and* humidity, and what extracted moderator effects do they report? | Three-factor interaction; Elicit's table is the only practical comparison surface. **Expected:** 2–4 papers (low N → high VOI gap). |

---

## Tool C · Consensus (5 questions)

> **Best for:** binary causal claims; returns Yes/Mixed/No verdict + supporting and rebutting evidence. Use when the literature is *expected to be split* and KA's argumentation layer needs the contested-claim status.

| # | Cluster | Question | Why this tool / expected yield |
|---|---------|----------|--------------------------------|
| CO-1 | C1 | Does elevated indoor CO₂ cause measurable cognitive decrements in healthy adults at concentrations below 2 000 ppm? | Core contested claim for K-ATLAS Q16. **Expected:** Mixed verdict; ≈6 supporting (Satish/Allen lineage), ≈3 rebutting (Scully/Snow/replication-failures). |
| CO-2 | C2 | Does indoor PM2.5 exposure degrade decision-making quality independently of CO₂ in office or classroom settings? | Cluster-independence claim — important because Cedeño Laurent 2021 reports both effects from one dataset. **Expected:** Mixed → Yes (≈6:2). |
| CO-3 | C3 | Does increasing outdoor-air ventilation rate above ASHRAE minima improve cognitive performance in office workers? | Tests the *intervention* claim that drives the Allen/MacNaughton economic argument. **Expected:** Yes verdict; ≈10:1 supporting. |
| CO-4 | C4 | Do indoor temperatures outside the 21–23 °C comfort range degrade decision-making in office workers? | Tests Young 2024's non-linear thermal claim. **Expected:** Mixed / Yes; non-linear pattern likely surfaces in supporting cites. |
| CO-5 | C1 | Does CO₂ inhalation at 1 000–2 500 ppm impair attention as measured by the Stroop test? | Narrower-DV variant of CO-1; routes to an instrument-specific subliterature. **Expected:** Mixed; useful for triangulating Stroop-vs-SMS sensitivity. |

---

## Tool D · PubMed / Boolean (5 questions)

> **Best for:** controlled-vocabulary canon search with verifiable hit counts. Use when you know the right anchor terms (instrument names, anchor authors, MeSH codes) and want a reproducible record.

| # | Cluster | Question (operationalised as TIAB Boolean) | Why this tool / expected yield |
|---|---------|--------------------------------------------|--------------------------------|
| PM-1 | C1 | `("Strategic Management Simulation"[TIAB]) AND (CO2[TIAB] OR "carbon dioxide"[TIAB] OR ventilation[TIAB])` | Drops the noisy `OR SMS` token (Phase 1 lesson from Q02). **Expected:** ~8 hits, ≥6 Include. |
| PM-2 | C1 | `(Wargocki P[Author] OR Allen JG[Author] OR Satish U[Author] OR MacNaughton P[Author] OR Herbig B[Author]) AND (CO2[TIAB] OR ventilation[TIAB] OR IAQ[TIAB]) AND ("2020"[PDAT] : "3000"[PDAT])` | Author-anchor + post-2020 filter; converts the Phase 1 Q13 workhorse into a high-precision recent-canon sweep. **Expected:** 25–40 hits, ≥15 Include. |
| PM-3 | C3 | `("ventilation rate"[TIAB] OR "outdoor air"[TIAB]) AND ("Cognition"[Mesh] OR "Cognitive Function"[TIAB] OR Stroop[TIAB])` | Adds MeSH for Cognition to broaden recall while keeping precision (Phase 1 Q07 had no MeSH). **Expected:** 30–50 hits, ≥10 Include. |
| PM-4 | C2 | `(PM2.5[TIAB] OR "particulate matter"[TIAB]) AND ("cognitive performance"[TIAB] OR "executive function"[TIAB]) AND ("office"[TIAB] OR "classroom"[TIAB] OR "indoor"[TIAB]) NOT (animal*[TIAB] OR mouse*[TIAB] OR mice[TIAB] OR rat[TIAB])` | Trims animal models; expands cognitive vocabulary. **Expected:** 12–20 hits, ≥6 Include. |
| PM-5 | C4 | `("indoor environmental quality"[TIAB] OR IEQ[TIAB] OR "thermal comfort"[TIAB]) AND (Stroop[TIAB] OR "n-back"[TIAB] OR "decision-making"[TIAB] OR EEG[TIAB]) AND (office[TIAB] OR worker*[TIAB] OR classroom[TIAB])` | Cross-cluster — pulls IEQ work that uses any of the canonical attention/decision DVs. **Expected:** 15–25 hits, ≥5 Include. |

---

## Cluster coverage matrix

|        | C1 (CO₂×DQ) | C2 (PM2.5×Cog) | C3 (Vent×Prod) | C4 (Thermal/IEQ) | row total |
|--------|:-----------:|:--------------:|:--------------:|:----------------:|:---------:|
| Google AI Scholar | 2 (GS-1, GS-5) | 1 (GS-2) | 1 (GS-3) | 1 (GS-4) | 5 |
| Elicit | 2 (EL-1, EL-2) | 1 (EL-4) | 1 (EL-3) | 1 (EL-5) | 5 |
| Consensus | 2 (CO-1, CO-5) | 1 (CO-2) | 1 (CO-3) | 1 (CO-4) | 5 |
| PubMed | 2 (PM-1, PM-2) | 1 (PM-4) | 1 (PM-3) | 1 (PM-5) | 5 |
| **column total** | **8** | **4** | **4** | **4** | **20** |

> C1 is intentionally double-weighted — it is the K-ATLAS Q16 anchor cluster and the highest-VOI gap to fill. The other three clusters get one question per tool to maintain topical breadth (assignment requires ≥4 clusters).

## Submission to shared queue

Machine-readable export at [`question_set.json`](question_set.json) — same data, structured for ingest into the class shared question queue. Format: `[{id, tool, cluster, question, expected_yield, executed: false}, …]`.
