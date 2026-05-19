# A0 — Collect Articles (COGS 160 Track 2, Weeks 1–2)

**Student:** Dhruv Sood (d2sood@ucsd.edu)
**Total:** 20 articles = 10 Q1 (empirical-only) + 10 Q2 (any type)

## Q1 — CO2 Concentration & Decision Quality (empirical only, K-ATLAS Q16)
**Question:** At what CO2 concentration does strategic decision-making quality (measured by SMS or comparable instrument) begin to decline, and is the threshold lower for cognitively demanding vs. routine tasks?

**KA topic match:** CO2 Concentration × Decision Quality (Q16)
**Key instrument:** Strategic Management Simulation (SMS)

All 10 Q1 papers are empirical (original data, human subjects, CO2 as IV or measured exposure, cognitive/decision outcome as DV).

## Q2 — Circadian-effective lighting & cognitive performance (any type)
**Question:** What peer-reviewed evidence shows that variations in circadian-effective lighting (melanopic lux, blue-enriched white light, dynamic day-like schedules) in office/classroom settings affect alertness, sustained attention, and working-memory performance in adults, and what ipRGC/melanopsin → SCN mechanisms explain these effects?

**KA topic match:** Luminous Environment × Cognitive Performance (Circadian), VOI 0.57

Mix of experiments, systematic review, consensus statement, and methods paper.

## Per-article requirements (met for all 20)
- APA 7 citation — see `apa_citations.txt` in each folder
- DOI — full `https://doi.org/...` link in manifest
- Abstract — verbatim from publisher in manifest `abstract` column
- Peer-reviewed (or IZA working paper for Künn 2019); publication range 2012–2025
- Source journal in manifest `source` column

## Folder layout
```
A0_collect_articles/
├── README.md                 # this file
├── SUBMISSION_CHECKLIST.md
├── Q1_assigned/
│   ├── manifest.csv          # 10 rows, columns: title,authors,year,doi,abstract,source,notes
│   ├── apa_citations.txt     # 10 APA 7 citations
│   ├── queries.md            # Google AI Citation queries used
│   └── pdfs/                 # PDFs to be added (see checklist)
└── Q2_selected/
    ├── manifest.csv
    ├── apa_citations.txt
    ├── queries.md
    └── pdfs/
```

## Search method
Google AI Citation (semantic sentence-form queries, not Boolean). Pattern A (broad framing) and Pattern B (empirical measure × population × condition × control) were the workhorses. See each `queries.md`.

## Note on PDFs
DOIs for all 20 papers are in the manifests. PDFs should be downloaded into `Q1_assigned/pdfs/` and `Q2_selected/pdfs/` named `<firstauthor>_<year>_<shorttitle>.pdf` before final upload. The K-ATLAS ingest pipeline can also fetch abstracts directly from DOI if the instructor re-runs classification.
