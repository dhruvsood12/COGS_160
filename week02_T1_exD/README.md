# Week 2 — Track 1 · Exercise D (Evidence Search Filter)

**Student:** Dhruv Sood · **Course:** COGS 160 · Spring 2026 · Week 2 (AI-Directed Programming)
**Exercise:** D — Evidence Search Filter (Track 1: Evidence Explorer)
**Date:** 2026-05-03

## Goal

Build a client-side search-and-filter bar for `ka_evidence.html` that lets a user narrow ~1,900 K-ATLAS evidence claims by warrant class, credence, topic, status, qualifier, defeat type, study type, support/attack counts, and keyword.

Two primary user stories drove the design:
- **Architect:** *"What does the evidence say about biophilic design and stress reduction?"*
- **Philosophy student:** *"All contested claims with undercutting defeaters."*

## Files

| File | Purpose |
|---|---|
| [`SUBMISSION.md`](SUBMISSION.md) | Full markdown writeup (context init, AI exchanges, design decisions, screenshots) |
| [`SUBMISSION.pdf`](SUBMISSION.pdf) | PDF render of the submission |
| [`filter.html`](filter.html) | Working implementation — open in a browser, attach `evidence.json` |
| [`evidence.json`](evidence.json) | Real K-ATLAS evidence dataset (1,900 records, 5.7 MB) used for verification |
| [`screenshots/`](screenshots/) | Five visual checkpoints: initial state, biophilia × stress, contested-undercut, high-trust, empty-state |

## What this proves

The component runs entirely in memory (data is fetched once); filtering is conjunctive across ~10 fields with substring/contains matching for free-text. The hard part wasn't filter logic — it was deciding which filters are visible by default (progressive disclosure had to be defended, not assumed) and showing the count of *filtered-out* results so the user never thinks they're seeing the whole evidence base.
