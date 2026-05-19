# Phase 3 — Corpus Table & KA Overlap (start)

**Student:** Dhruv Sood · **Track 2 / Weeks 4–5**
**Phase 3 deliverable:** Recall / precision table comparing the manual corpus against KA's automated pipeline. Target: 50 papers assessed, 25+ Include, KA overlap measured.

## Status

| Metric | Current | Target | Note |
|--------|--------:|-------:|------|
| Corpus size (Include) | **27** | 25+ ✓ | Target met at start of Phase 3 |
| Papers assessed (Include + Reject + Edge) | 27 + 17 reject + 8 edge = **52** | 50+ ✓ | Counted from query_diary `decision_count` |
| KA overlap — measured Y / N | 10 Y / 0 N (Q1 only); 17 pending | full 27 | Requires KA Article Search lookup per row (user action) |
| New to KA — submitted to intake | 0 | per Phase 4 (≥150 records over Weeks 6–7) | Not yet staged |

## Methodology note for "In KA?" and "Pipeline would find?"

- **In KA?** is determined by querying KA's Article Search by DOI. The 10 Q1 papers were submitted in A0 and are presumed `Y` (verify via the Article Intake page after this submission). The 17 Phase-1 new finds are presumed `N` (verify the same way) — once verified, this is the recall metric.
- **Pipeline would find?** asks whether KA's automated AI-Citation / Boolean queries (per the [Knowledge Atlas Article Finder context](../../A0_collect_articles/Q1_assigned/queries.md)) would surface the paper. Heuristic: does the paper's abstract contain the canonical KA Q16 vocabulary (CO₂, ventilation, decision quality, cognition, ppm, office, classroom, IEQ, IAQ, Stroop, SMS)? If yes → `Y`. If no → flag as a pipeline gap.

## Corpus

| # | APA Citation (brief) | DOI / PMID | Cluster | In KA? | Pipeline would find? | Action |
|---|---------------------|-----------|---------|:------:|:--------------------:|--------|
| 1 | Satish U, et al. (2012). Is CO₂ an indoor pollutant? Direct effects of low-to-moderate CO₂ concentrations on human decision-making performance. *EHP*. | 10.1289/ehp.1104789 / PMC3548274 | C1 | Y | Y | already in corpus |
| 2 | Allen JG, et al. (2016). Associations of Cognitive Function Scores with Carbon Dioxide, Ventilation, and Volatile Organic Compound Exposures in Office Workers. *EHP*. | 10.1289/ehp.1510037 / PMC4892924 | C1 + C3 | Y | Y | already in corpus |
| 3 | Scully RR, et al. (2019). Effects of acute exposures to carbon dioxide on decision making and cognition in astronaut-like subjects. *npj Microgravity*. | 10.1038/s41526-019-0071-6 | C1 | Y | Y | already in corpus |
| 4 | Cedeño Laurent JG, et al. (2021). Associations between acute exposures to PM2.5 and CO₂ indoors and cognitive function in office workers. *Environ Res Lett*. | 10.1088/1748-9326/ac1bd8 | C1 + C2 | Y | Y | already in corpus |
| 5 | MacNaughton P, et al. (2015). Economic, Environmental and Health Implications of Enhanced Ventilation in Office Buildings. *IJERPH*. | 10.3390/ijerph121114709 / PMC4661675 | C3 | Y | Y | already in corpus |
| 6 | Vehvilainen T, et al. (2016). High indoor CO₂ concentrations in an office environment increase transcutaneous CO₂ and sleepiness. *J Occup Environ Hyg*. | 10.1080/15459624.2015.1076160 | C1 + C4 | Y | Y | already in corpus |
| 7 | Künn S, Palacios J, Pestel N. (2019). Indoor Air Quality and Cognitive Performance. *IZA DP 12632*. | 10.2139/ssrn.3460848 | C2 | Y | **N** (grey lit; PubMed-invisible) | already in corpus — flag pipeline gap |
| 8 | Shimazaki K, et al. (2025). Effects of in-car CO₂ concentration on driving: a preliminary study with taxi drivers. *Environ Occup Health Pract*. | 10.1539/eohp.2025-0001 / PMID 41020138 | C1 (vehicle) | Y | Y | already in corpus |
| 9 | Young AS, et al. (2024). Home indoor air quality and cognitive function over one year for people working remotely during COVID-19. *Build Environ*. | 10.1016/j.buildenv.2024.111551 / PMC11221786 | C4 + C1 | Y | Y | already in corpus |
| 10 | Bejder Klausen F, et al. (2023). The effect of air quality on sleep and cognitive performance in school children. *IJOMEH*. | 10.13075/ijomeh.1896.02032 / PMC10464806 | C1 + C3 | Y | Y | already in corpus |
| 11 | Herbig B, Mayer F, Norrefeldt V, Wargocki P. (2026). Do CO₂, VOCs and atmospheric pressure affect cognitive performance: large-scale simulated-flights experiment. *Int J Hyg Environ Health*. | 10.1016/j.ijheh.2026.114809 / PMID 42035679 | C1 + C3 | **N** (verify) | Y | **stage to intake** |
| 12 | Yang Y, et al. (2026). Impact of experimentally elevated CO₂ and temperature on cognitive function: an EEG-based study under constant ventilation. *Ecotoxicol Environ Saf*. | 10.1016/j.ecoenv.2025.119578 / PMID 41601028 | C1 + C4 | **N** (verify) | Y | **stage to intake** |
| 13 | Ge B, et al. (2025). Decision tools for schools using continuous IAQ monitors: CO₂ in Boston Public Schools. *Lancet Reg Health Am*. | 10.1016/j.lana.2025.101148 / PMID 40585557 | C3 | **N** (verify) | Y | **stage to intake** |
| 14 | Dedesko S, Pendleton J, Young AS, et al. (2025). Indoor air exposures and cognitive test scores among university students in classrooms with increased ventilation. *J Expo Sci Environ Epidemiol*. | 10.1038/s41370-025-00770-6 / PMID 40204887 | C3 + C1 | **N** (verify) | Y | **stage to intake** |
| 15 | Zhang S, Ma T, Zuoqiu S. (2026). EEG response and productivity outcome under changing indoor environment. *Front Public Health*. | 10.3389/fpubh.2026.1767357 / PMID 41869617 | C4 | **N** (verify) | Y | **stage to intake** |
| 16 | Wälde J, et al. (2026). Heat stress impacts affective processes and risk-taking behaviour. *Sci Rep*. | 10.1038/s41598-026-47250-x / PMID 41957074 | C4 | **N** (verify) | partial (no CO₂) | **stage to intake** — flagged: pipeline must add "heat stress" + "risk task" vocab |
| 17 | Wang C, Lin Y, Ptukhin Y, Liu S. (2024). Air quality in the car: How CO₂ and body odor affect drivers' cognition and driving performance? *Sci Total Environ*. | 10.1016/j.scitotenv.2023.168785 / PMID 37996033 | C1 (vehicle) | **N** (verify) | Y | **stage to intake** |
| 18 | Herbig B, et al. (2023). Effects of increased recirculation air rate and aircraft cabin occupancy on passengers' health: an RCT. *Environ Res*. | 10.1016/j.envres.2022.114770 / PMID 36370817 | C3 + C1 | **N** (verify) | Y | **stage to intake** |
| 19 | Zhao Q, Seow WJ. (2026). Environmental regulation, air pollution, and cognitive function among middle-aged and older adults in China: A quasi-experimental study. *Ecotoxicol Environ Saf*. | 10.1016/j.ecoenv.2025.119626 / PMID 41512775 | C2 | **N** (verify) | partial (no indoor focus) | **stage to intake** — flagged: pipeline misses policy-instrumented designs |
| 20 | Kuramochi H, Tsurumi R, Ishibashi Y. (2023). Meta-Analysis of the Effect of Ventilation on Intellectual Productivity. *IJERPH*. | 10.3390/ijerph20085576 / PMID 37107857 | C3 | **N** (verify) | Y | **stage to intake** — high-VOI SR |
| 21 | (2025). Indoor air pollution from solid fuels and cognitive impairment: a systematic review and meta-analysis. *Rev Environ Health*. | 10.1515/reveh-2023-0158 / PMID 38413202 | C2 | **N** (verify) | partial (LMIC contexts) | **stage to intake** as boundary case |
| 22 | (2025). Carbon Dioxide as a Multisystem Threat in Long Duration Spaceflight. *Aerosp Med Hum Perform*. | 10.3357/AMHP.6716.2025 / PMID 41253359 | C1 (closed env) | **N** (verify) | Y | **stage to intake** |
| 23 | Vyas P, et al. (2021). Effects of head-down tilt bed rest plus elevated CO₂ on cognitive performance. *J Appl Physiol*. | 10.1152/japplphysiol.00865.2020 / PMID 33630672 | C1 (closed env) | **N** (verify) | Y | **stage to intake** |
| 24 | (2021). The effects of a spaceflight analog with elevated CO₂ on sensorimotor adaptation. *J Neurophysiol*. | 10.1152/jn.00306.2020 / PMID 33296611 | C1 (closed env) | **N** (verify) | partial | **stage to intake** as edge |
| 25 | (2021). Head-Down-Tilt Bed Rest With Elevated CO₂: Effects of a Pilot Spaceflight Analog on Neural Function and Performance During a Cognitive-Motor Task. *Front Physiol*. | 10.3389/fphys.2021.654906 / PMID 34512371 | C1 (closed env) | **N** (verify) | Y | **stage to intake** |
| 26 | Fisk WJ. (2011). Benefits and costs of improved IEQ in U.S. offices. *Indoor Air*. | 10.1111/j.1600-0668.2011.00719.x / PMID 21470313 | C3 + C4 | **N** (verify) | Y | **stage to intake** — canonical IEQ-economics paper |
| 27 | (2025). Sick building syndrome and indoor air quality in Malaysian bank offices: a cross-sectional analysis. *Dialogues Health*. | 10.1016/j.dialog.2025.100249 / PMID 41140948 | C1 + C4 | **N** (verify) | Y | **stage to intake** as cross-cultural data point |

## Reject / Edge-case examples (sampled from Boolean noise; documented for the Phase 5 report)

| # | Brief | Reason |
|---|-------|--------|
| R-1 | Façade-Level Monitoring of CO₂ Variability under Urban Heat Island (PMID 41460748, *J Vis Exp* 2025) | Instrumentation methods paper; no human cognition outcome. |
| R-2 | Deep learning and multi-objective optimization for real-time occupancy-based energy control (PMID 41219414, *Sci Rep* 2025) | Pure HVAC engineering; no behavioral DV. |
| R-3 | Physiological impact of surgical masks and N95 masks on obese operating room staff (PMID 39994350) | Hits on `SMS` token; off-topic. |
| R-4 | Ensiled mushroom substrate for cattle feed (PMID 40161239) | Hits on `SMS` token (mushroom substrate); totally off-topic — example of `SMS` lexical noise. |
| R-5 | tDCS in 7.5 % CO₂ inhalation challenge (PMID 41810527, *J Psychopharmacol* 2026) | Anxiety-induction paradigm at 7.5 % (75 000 ppm) — outside the indoor-environment range. |
| E-1 | Residential environment quality with mild cognitive impairment in middle/elderly Chinese (PMID 39608295) | Out-of-population (elderly with MCI) — keep as edge for the boundary argument. |
| E-2 | Air pollution and dementia mediators (PMID 40717464, *J Alzheimers Dis* 2025) | Out-of-population (dementia) but the mediator framework (inflammation, vascular) is potentially adoptable for KA's argumentation layer — edge. |
| E-3 | Ozone-skin chemistry and indoor mixing (PMID 41987913) | No cognition outcome but adds mechanistic context for VOC pathway — edge. |

## Recall / Precision metric design (for completion in Week 5 once KA lookup is run)

```
Recall  = (manual_corpus ∩ KA_existing) / manual_corpus
        = papers KA already had / papers I found = lower bound on what KA would have found me

Precision = (KA_pipeline_returns ∩ manual_corpus) / KA_pipeline_returns
          = how many of KA's automated hits I also flagged Include
          = upper bound on KA's relevance to my research front
```

Both metrics require Week-5 follow-up: (a) DOI-by-DOI lookup against the KA Article Search index, and (b) running the KA automated pipeline (or its query bank) against my research front and counting overlap.
