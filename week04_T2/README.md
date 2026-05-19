# Week 4 — Track 2 (Article Finder)

**Student:** Dhruv Sood · **Course:** COGS 160 · Spring 2026 · Track 2
**Date:** 2026-05-04 · **Branch:** `main` (Track 2 task PRs will go on `track2/dhruv-sood`)
**Topic locked all week:** **C1 — CO₂ × Decision Quality** (K-ATLAS Q16 anchor cluster)

This folder bundles all Week 4 Track 2 work: Phase 2 question set, Phase 3 corpus-table kickoff, and the Week-4 evidence bundle (Deliverables A + B + C) per the [Track 2 Week 4 page](../track2/Knowledge_Atlas/160sp/track2_week_4.html).

## Subfolders

| Subfolder | Phase | Contents |
|---|---|---|
| [`phase2_question_set/`](phase2_question_set/) | Phase 2 | 20 well-formed questions across 4 AI tools × 4 topic clusters. Output of the question maker. |
| [`phase3_corpus_table/`](phase3_corpus_table/) | Phase 3 (kickoff) | 27-paper working corpus + KA-overlap tracking matrix. Recall/precision metric design. |
| [`deliverable_ABC/`](deliverable_ABC/) | Week-4 evidence bundle | Real topic run + manual review packet + focused repair, all reproducible. |

## What this week proves

By the end of Week 4 I have *one genuinely operational example, not a speculative architecture*:

- **One real topic** (C1, named, kept the entire week) — re-runnable by another student with a single `curl` against PubMed.
- **One reviewed sample of 10 records** drawn from that run (5 ACCEPT + 5 BORDERLINE/REJECT) with explicit per-paper reasoning, including two *real* borderlines that complicate the K-ATLAS Q16 claim.
- **One concrete repair** (drop `OR SMS`, broaden second clause): 41 hits → 3 hits today, noise rate 80 % → 0 %, plus one in-canon paper recovered.

## File map (deliverable_ABC)

| Deliverable | File |
|---|---|
| A — Real topic run | [`deliverable_ABC/A_run_report.md`](deliverable_ABC/A_run_report.md) |
| B — Manual review packet | [`deliverable_ABC/B_review_packet.md`](deliverable_ABC/B_review_packet.md) |
| C — Focused repair | [`deliverable_ABC/C_repair.md`](deliverable_ABC/C_repair.md) |
| Run manifest | [`deliverable_ABC/runs/run_manifest.txt`](deliverable_ABC/runs/run_manifest.txt) |
| Q03 fresh raw JSON | [`deliverable_ABC/runs/q03_rerun_2026-05-04.json`](deliverable_ABC/runs/q03_rerun_2026-05-04.json) |
| Q02 BEFORE raw JSON | [`deliverable_ABC/runs/q02_original_2026-05-04.json`](deliverable_ABC/runs/q02_original_2026-05-04.json) |
| Q02 AFTER (PM-1) raw JSON | [`deliverable_ABC/runs/q02_repaired_PM1_2026-05-04.json`](deliverable_ABC/runs/q02_repaired_PM1_2026-05-04.json) |
| Top-10 Q03 esummary | [`deliverable_ABC/runs/q03_top10_summaries.json`](deliverable_ABC/runs/q03_top10_summaries.json) |
| Tail-20 Q03 esummary | [`deliverable_ABC/runs/q03_tail20_summaries.json`](deliverable_ABC/runs/q03_tail20_summaries.json) |
| Q02-original noise inspection | [`deliverable_ABC/runs/q02_original_top10_summaries.json`](deliverable_ABC/runs/q02_original_top10_summaries.json) |
| PM-1 (3-record) esummary | [`deliverable_ABC/runs/pm1_repaired_summaries.json`](deliverable_ABC/runs/pm1_repaired_summaries.json) |
| Borderline abstracts (4 records) | [`deliverable_ABC/runs/borderline_abstracts.txt`](deliverable_ABC/runs/borderline_abstracts.txt) |
| Borderline abstract (5th, 20 000 ppm) | [`deliverable_ABC/runs/borderline_34605578.txt`](deliverable_ABC/runs/borderline_34605578.txt) |
| ACCEPT abstracts (5 records) | [`deliverable_ABC/runs/accept_abstracts.txt`](deliverable_ABC/runs/accept_abstracts.txt) |

All raw JSON / text was generated 2026-05-04 by direct `curl` to NCBI E-utilities — no API key, no proxy, no auth, no scraper. Reproducible by any reader.

## Verification checklist (against the Week-4 prompt)

| ✓ | Criterion | Where it's proven |
|---|---|---|
| ✓ | One real topic — name it and reproduce the exact command. | A §1 (topic = C1; `curl` URL given). |
| ✓ | One reviewed sample — 5 strong + 5 problematic, with reasons. | B (A-1…A-5, B-1…B-5). |
| ✓ | One false positive — initially-relevant-looking but should not pass. | B (B-3 / B-4 / B-5: sensor papers with motivational `cognitive`). |
| ✓ | One repair — code, query, or spec change in response to evidence. | C: drop `OR SMS`, broaden second clause; before/after `count` 41 → 3. |
| ✓ | Pass/fail basis clear — what succeeded vs. uncertain. | Each deliverable has its own "Pass/fail" section. |

## Succeeded vs. deferred

**Succeeded this week:**
- C1 topic path is reproducible end-to-end with a single `curl`. Rerun produced zero PMID drift over 24 h.
- Three rejects of the *same shape* (`cognitive` keyword, no cognitive DV) classified by hand — the false-positive pattern is named and stable.
- Two real borderlines (B-1 mediator-hit / cognition-null; B-2 high-dose null) tied to specific spec gaps for next week's repair and the K-ATLAS Q16 constitution.
- The `OR SMS` repair is a 93 % noise reduction with full signal preservation and one previously-missed in-canon paper recovered (PMID 29789085, submariner study).

**Deferred to Week 5:**
- **Recall against KA's existing index.** Phase 3 corpus table marks 17 of 27 papers as "verify In KA?" — that lookup is a Week-5 task and closes the recall metric.
- **Cross-tool recall.** PubMed missed Künn 2019 (grey lit). Whether Elicit / Consensus / Google AI Scholar catch papers PubMed misses is the empirical question of the Phase-2 question set, pending interactive execution.
- **B-1 / B-2 spec change.** "Mediator-positive / cognition-null" triage state and "exclude > 5 000 ppm from K-ATLAS Q16 evidence base" — logged in B, not implemented.
- **B-3 / B-4 / B-5 spec change.** "Require named DV in abstract" feature for the abstract classifier — logged in B, not implemented.

## Honest limits

- **PubMed only.** Q03 is one query against one tool. Multi-tool runs (Elicit, Consensus, Google AI Scholar) are drafted in [`phase2_question_set/question_set.md`](phase2_question_set/question_set.md) but require interactive auth and are deferred.
- **Manual triage.** ACCEPT/BORDERLINE/REJECT decisions are mine, not the canonical KA classifier (`atlas_shared.classifier_system.AdaptiveClassifierSubsystem` — wiring is Task-3 work in the Track-2 plan).
- **No PDF acquisition.** Stops at abstract-level triage — consistent with the Track-2 contract (never download a PDF to decide relevance).

## Exit condition (per Week-4 prompt)

> *You can move on when you have one topic path that another student could rerun, inspect, and challenge.*

A student who clones this folder can:
1. Re-run the Q03 `curl` and verify count = 32 with the same first 10 PMIDs (or document drift).
2. Re-run the Q02 BEFORE / AFTER `curl`s and verify the 41 → 3 collapse, and read off the same 3 in-canon PMIDs.
3. Read B and challenge any of the 10 ACCEPT/BORDERLINE/REJECT calls — the abstracts are in `deliverable_ABC/runs/`.
4. Read C and decide whether the abbreviation-token rule generalises to other instruments (IAQ, IEQ, MMSE, PVT) — next student's Week-4 work.

The path is now explicit, inspectable, and no longer imaginary.
