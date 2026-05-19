# Week 4 — Deliverable B: Manual Review Packet

**Student:** Dhruv Sood · **Course:** COGS 160 · Spring 2026 · Track 2
**Topic:** C1 — CO₂ × Decision Quality
**Source run:** Q03 rerun on 2026-05-04 (see [`A_run_report.md`](A_run_report.md))
**Inclusion definition (locked):** peer-reviewed empirical study OR systematic review/meta-analysis; primary measurement OR explicit experimental manipulation of indoor CO₂; cognition / decision-quality / productivity DV (Stroop, SMS, n-back, MSLT, EEG correlate, simulator-error rate, etc.); adult or school-age population in indoor setting (office, classroom, vehicle, closed-environment analog). Excludes: clinical CO₂-inhalation panic-induction studies (≥7.5 % = ≥ 75 000 ppm), pure HVAC engineering papers without a behavioral DV, sensor-deployment papers without a human cognition outcome.

**Why this packet matters:** the value of this triage isn't in the easy yes/yes/yes — it's in the **5 cases below the line**. Three are clear rejects that look topical because the title pings on "CO₂" and "cognitive"; two are real-borderlines that show where the question filter and the dose-response model in K-ATLAS Q16 get tested.

---

## ACCEPT — 5 records

### A-1 · PMID 42035679 · Herbig et al. 2026 — *Int J Hyg Environ Health*
**Why ACCEPT.** Factorially manipulates CO₂ × VOC × atmospheric pressure in a simulated-flight chamber — directly disentangles the confound that has dogged every Satish/Allen-style cognitive-decline claim since 2012. Cognition DV is a battery of attention/decision tests. Wargocki + Herbig are European canon; this is the most recent multi-factor experiment in cluster C1. **Highest VOI in the run.**
**Evidence base:** title + abstract names cognitive performance as the primary DV; design is RCT-equivalent within-subject crossover.

### A-2 · PMID 41601028 · Yang, Dong, Wang et al. 2026 — *Ecotoxicol Environ Saf*
**Why ACCEPT.** Adds an *objective neural correlate* (EEG) on top of the SMS/Stroop behavioral DVs that dominate the canon. The constant-ventilation control isolates CO₂ from outdoor-air-rate confounding — methodologically what's missing from Allen 2016's design. Direct extension of the within-subject experimental tradition.
**Evidence base:** "EEG-based study under constant ventilation" in the title is unambiguous; abstract specifies CO₂ × temperature factorial.

### A-3 · PMID 40204887 · Dedesko, Pendleton, Young et al. 2025 — *J Expo Sci Environ Epidemiol*
**Why ACCEPT.** Repeated-measures observational design with a *natural-experiment shock* (post-COVID ventilation upgrade in classrooms). This is methodologically novel in the cluster — most C1 work is chamber-only. Authors are the Allen/Spengler stream extension of MacNaughton 2015.
**Evidence base:** titled "Associations between indoor air exposures and cognitive test scores"; population is university students in real classrooms; cognition DV is a test battery.

### A-4 · PMID 38966206 · Young et al. 2024 — *Build Environ*
**Why ACCEPT.** One-year longitudinal home-IAQ × cognition study — the *temporal* extension of the chamber tradition. Working-from-home population is exactly the post-COVID cohort the K-ATLAS argumentation layer needs to address. Already in corpus (Week-3 #9); this rerun confirms it surfaces stably under Q03.
**Evidence base:** "cognitive function over one year for people working remotely" — both manipulation (passive — observed real-world CO₂) and DV are explicit.

### A-5 · PMID 37996033 · Wang, Lin, Ptukhin, Liu 2024 — *Sci Total Environ*
**Why ACCEPT.** Three CO₂ levels (800 / 1 800 / 3 500 ppm) × 2 odor conditions in a highway driving simulator, with working-memory DV. Finer dose-response than Shimazaki 2025 (already in corpus) and adds an interaction with body odor — useful for the cabin-air sub-cluster. **Replication candidate** for the dose-response curve in the Phase-5 report.
**Evidence base:** abstract specifies n=25, three CO₂ levels, simulator + working-memory tests.

---

## BORDERLINE / REJECT — 5 records

### B-1 · PMID 39142454 · Jin et al. 2024 — *Environ Res* — **BORDERLINE → MARK FOR REVIEW**
**Why borderline.** This is a *replication-failure-style* finding that is *not* a true negative. CO₂ at ~5 000 ppm significantly shortened sleep latency on the MSLT (Control 13.1 min → CO₂ 9.7 min) AND raised subjective sleepiness — but **post-nap cognitive responses showed no significant difference**. Two interpretations:
  1. CO₂ acts via a sleepiness mediator; the mediator hits but the cognition DV is too coarse / too short to register the downstream effect (n=11 is small; possible Type-II error).
  2. The cognition pathway is genuinely independent of the sleepiness pathway and both can be triggered without the other.
Interpretation 1 is *exactly* the mediation pathway already represented by Q12 in my Phase-1 diary (CO₂ → drowsiness → degraded decision). Interpretation 2 would be a genuine boundary on the K-ATLAS Q16 claim.
**Why this exposes a weakness in my filter.** My Phase-1 inclusion rule says "primary measurement … of indoor CO₂ + cognition DV" — this paper has both, but the cognition DV is **null** while the mediator DV is **positive**. The rule does not tell me which half to weight. → Update the Phase-2 question filter to handle "positive on mediator, null on cognition" as a separate triage state, not a forced ACCEPT or REJECT. (See Deliverable C.)
**Evidence base:** abstract reports both effects; concentration is 5 000 ppm, within the realistic-indoor upper-bound range (workplace 8h-TLV).

### B-2 · PMID 34605578 · Maniscalco et al. 2022 — *Indoor Air* — **BORDERLINE → MARK FOR REVIEW**
**Why borderline.** Healthy adults exposed to **20 000 ppm** CO₂ for 4 h, with attention/flexibility/sustained-attention battery (TAP) and CFF. Result: blood pH ↓ and pCO₂ ↑ (within normal range), respiratory rate ↑ slightly, **no change in heart rate, CFF, or task performance**. The authors conclude "impairment of cognitive performance is not expected from exposure to 20 000 ppm CO₂." This is a *high-quality null at an extreme dose*.
**Why this exposes a weakness in my filter.** 20 000 ppm = 2 % CO₂. That is **20× the K-ATLAS Q16 indoor range** (Satish 2012 used 600/1 000/2 500 ppm). My Phase-1 exclusion rule already kicks out the 7.5 % inhalation panic literature, but **does not** kick out the 0.5–5 % industrial-occupational range — and that range produces nulls for the wrong reason: the dose is so high that physiological adaptation kicks in. If this paper were uncritically counted as evidence *against* K-ATLAS Q16, it would silently destroy the dose-response argument. → BORDERLINE / MARK FOR REVIEW. The repair is to add an explicit `concentration_ppm` field to triage and exclude doses > 5 000 ppm from the K-ATLAS Q16 evidence base (separately catalogue them as "high-dose-occupational" boundary cases). (See Deliverable C.)
**Evidence base:** abstract specifies 770 ppm vs. 20 000 ppm; cognitive battery enumerated; null result stated.

### B-3 · PMID 40218481 · Fedele et al. 2025 — *Sensors* — **REJECT** (sensor-deployment paper, no human cognition DV)
**Why reject.** Sensor study only. CO₂, temperature, and humidity were measured in 3 Italian university classrooms across 20 days — *no human cognitive performance was measured*. The abstract speculates that "Poor IAQ can impair students' cognitive performance" but no test, survey, or behavioral DV is administered. The paper is appropriate for an *engineering* corpus, not for K-ATLAS Q16 evidence.
**Why this exposes a weakness in my filter.** The Q03 query keys on `cognitive` in the abstract — and the Fedele abstract uses "cognitive performance" *speculatively*. The Phase-1 filter as written ("primary measurement … of indoor CO₂ + cognition DV") would catch this, but a less-strict reader could be tricked. → Future tightening for Phase-2 question prompts: require the abstract to name a *specific cognitive test or behavioural DV* (Stroop, SMS, n-back, MSLT, EEG, error rate, throughput) — the absence of any specific DV in the abstract is itself a near-perfect REJECT signal. (Captured as a candidate next-week repair.)

### B-4 · PMID 38988722 · Board et al. 2024 — *J Orthop* — **REJECT** (no cognition DV; speculative connection to known thresholds)
**Why reject.** CO₂ inside surgical helmet systems was monitored during 30 arthroplasty procedures (mean 3 006 ppm). The paper *cites* the 2 500 ppm cognitive-effect threshold from prior work but does **not** measure cognition or surgical performance. It is a measurement / occupational-exposure paper, not a cognition study.
**Why this is the same false-positive shape as B-3.** Title has "carbon dioxide", abstract has "cognitive function" — but only as a speculative motivator for the measurement study. Same recovery-rule applies: require a *named DV*, not just the word *cognitive*.

### B-5 · PMID 37521349 · Chou et al. 2023 — *Front Med* — **REJECT** (no cognition DV; descriptive monitoring only)
**Why reject.** IoT-based CO₂ monitoring in a 24-bed surgical ICU during COVID visitation restrictions. Reports CO₂ medians (576 ppm restricted vs. 628 ppm standard) and PM2.5 levels. Says ICU healthcare providers "experience high cognitive load" — cognitive load is *named* but not *measured*. No DV, no manipulation, no behavioral or neural endpoint.
**Why this matches B-3, B-4.** Same false-positive failure mode: keyword `cognitive` in the abstract → query hit, but the paper has no human-performance measurement. Three rejects of the *same shape* in one top-10 is the strongest single signal in this run that the rule "abstract contains `cognitive`" is too weak — and is the empirical motivation for the repair logged in Deliverable C.

---

## False-positive pattern this packet exposes

**B-3, B-4, B-5 share a structure: sensor / measurement / monitoring papers whose abstracts use "cognitive" in a motivational sentence but never measure cognition.** Three of ten top-Q03 hits are this pattern. That is a 30 % false-positive rate at the top of the highest-precision query I have. Not catastrophic — these are easy to triage by hand at the top — but a real signal for the Phase-3 pipeline: the abstract-classifier needs an "names-a-cognitive-DV" feature, not just keyword presence.

The borderlines (B-1, B-2) are a *different* failure mode: real cognition studies whose result complicates the K-ATLAS Q16 claim (B-2 null at 20 000 ppm, B-1 null on cognition / hit on mediator). These are the papers where the **constitution** behind Q16 needs to be sharper — does Q16 cover only ≤ 2 500 ppm? Does it require a direct cognition outcome or accept mediator outcomes? Those are exactly the constitution-clarification questions the Phase-2 question set was designed to surface, and they validate that the question-routing strategy works.

---

## Pass/fail basis for Deliverable B

✓ Five clear ACCEPTs with named cognition DVs and explicit reasoning per record.
✓ Five reviewed problematic / borderline records, including **two** real-borderlines (not just trivial rejects) that exposed weaknesses in my current rule.
✓ Each entry references observable evidence (named test, named concentration, named design) — no vague intuition.
✓ At least one borderline (B-1, B-2) drives a concrete spec change, recorded as Deliverable C.
✓ Includes the false-positive pattern (B-3 / B-4 / B-5: sensor papers with motivational `cognitive`) as a distinct failure mode.
