# ===== PART 1: PROJECT CUSTOM INSTRUCTIONS =====
# (复制下面这段到 Project Settings → Custom Instructions 文本框)
# ================================================

You are helping Dawen complete a Systematic Literature Review (SLR) paper:
"A Systematic Literature Review of I/O Stack Evolution for Fully Utilizing SSDs"

## Key Context
- Target: ArXiv submission
- Draft 3 exists (865 lines, 16 references to 2021)
- PaperSearchTracking.xlsx has 1,184 deduplicated papers from prior work
- Search cutoff: May 31, 2025. Search execution date: Feb 8, 2026.
- PRISMA 2020 compliant methodology required

## Strict Scope Boundary
- ✅ IN: I/O stack software optimization for ULL NVMe SSDs (io_uring, SPDK, blk-mq, eBPF/XRP, kernel bypass, NVMe passthrough, user-space FS)
- ❌ OUT: CXL (separate survey), ZNS-only, KV-SSD, computational storage, pure hardware, non-CS

## Authoritative Files
- **SLR_Protocol_v1.md** in outputs: THE single source of truth for queries (Q1-Q5), exclusion criteria (EC1-EC5), extraction schema, and PRISMA flow. NEVER re-derive these — they are LOCKED.
- **PRISMA_SLR_20260208.md** in project: Gemini-drafted PRISMA standard + 6-day plan + data conventions.
- **SLR_Continuation_Package.md** in outputs: Perplexity search results summary + continuation prompt.

## Working Rules
1. Do NOT add CXL content to this SLR.
2. 5 query strings (Q1-Q5) and 4 databases (DB1-DB4) + snowballing (DB5) are locked in Protocol.
3. Exclusion codes EC1-EC5 have strict priority: EC1>EC2>EC3>EC4>EC5.
4. User's prior work (2022 Survey + PaperSearchTracking.xlsx) is an ASSET — pre-confirmed papers enter as "Prior-Work" source.
5. HTML uploads from database searches can be parsed programmatically.
6. Be efficient with Dawen's time — he is under significant pressure.

## Current Progress
(Update this section as work progresses)
- Day 1: Protocol locked. Perplexity search done. Formal DB searches in progress.
- [Update with each conversation]


# ===== PART 2: PROTOCOL v1.1 AMENDMENTS =====
# (这些更新要合并进 SLR_Protocol_v1.md)
# =============================================

## AMENDMENT 1: Prior Work Integration (回答问题3)

### How existing work enters the PRISMA pipeline:

**Source A: PaperSearchTracking.xlsx (1,184 papers)**
- These are NOT a "database search" — they are your historical working corpus
- Role in PRISMA: They serve as a VALIDATION CHECK, not a search source
- Process:
  1. After DB1-DB4 searches complete → deduplicate against PaperSearchTracking.xlsx
  2. Any paper in your xlsx that ALSO appears in DB1-DB4 → confirms search completeness
  3. Any paper in your xlsx that does NOT appear in DB1-DB4 → candidate for DB5 (Snowballing) or flag as gap

**Source B: Papers already confirmed relevant from 2022 Survey**
- These enter Extraction Table directly with:
  - `Decision: Inc`
  - `Search_Source: Prior-Work`
  - `QA_Score`: assigned based on venue
- In the Methodology section (Section 2), you write:
  > "In addition to the systematic database search, N papers identified through
  > the first author's prior survey work [cite your 2022 draft or explain] were
  > included as seed studies. These were independently verified against the
  > inclusion/exclusion criteria."
- This is PRISMA-compliant — PRISMA 2020 explicitly has a box for
  "Records identified from other methods" in the flow diagram

**Source C: Your 2022 Survey text**
- This is your Day 5 asset for Section 4 (Synthesis)
- NOT part of the search/screening pipeline
- On Day 5: map your 2022 analysis paragraphs → REG-IDs from Extraction Table

### Updated PRISMA Flow (with Prior Work):

```
IDENTIFICATION
├── Records from DATABASE SEARCHES:
│   ├── DB1 Google Scholar: Q1=___ Q2=___ Q3=___ Q4=___ Q5=___
│   ├── DB2 ACM DL:         Q1=___ Q2=___ Q3=___ Q4=___ Q5=___
│   ├── DB3 IEEE Xplore:    Q1=___ Q2=___ Q3=___ Q4=___ Q5=___
│   ├── DB4 Semantic Scholar API: ___
│   └── Subtotal (databases): ___
│
├── Records from OTHER METHODS:
│   ├── DB5 Snowballing (forward+backward citations): ___
│   ├── Prior-Work (from 2022 survey, pre-confirmed): ___
│   └── Subtotal (other methods): ___
│
├── TOTAL RAW: ___
├── Duplicates removed: ___
└── After Deduplication: ___

SCREENING (Title/Abstract)
├── Records Screened: ___
├── Records Excluded: ___ (EC1=___ EC2=___ EC3=___ EC4=___ EC5=___)
└── Passed to Full-text: ___

ELIGIBILITY (Full-text)
├── Full-texts assessed: ___
├── Excluded with reasons: ___ (EC1=___ EC2=___ EC3=___ EC4=___ EC5=___)
└── Passed to Inclusion: ___

INCLUDED
└── Studies in final review: ___
```


## AMENDMENT 2: DB5 Snowballing Protocol (回答问题2)

### What DB5 is:
Snowballing = using known relevant papers to find MORE papers that keyword search missed.

### How to execute:

**Forward Snowballing (who cited these papers?):**
1. Go to Google Scholar
2. Search each seed paper
3. Click "Cited by N"
4. Scan the citing papers for relevance
5. Save HTML as: `DB5_Forward_[SeedPaperShortName]_20260208.html`

**Backward Snowballing (what do these papers cite?):**
1. Open PDF of each seed paper
2. Scan its References section
3. Note any paper you don't already have that looks relevant
4. Record manually

**Seed papers for snowballing (minimum set):**
- XRP (OSDI 2022) — Forward citations
- I/O Passthru (FAST 2024) — Forward citations
- BypassD (ASPLOS 2024) — Forward citations
- blk-switch (OSDI 2021) — Forward citations
- Your 3 most-cited papers from Draft 3 — Forward citations

**How results enter the pipeline:**
- Each discovered paper → add to Master_Registry.csv
- `Search_Source`: `DB5-Forward-XRP` or `DB5-Backward-IOPassthru`
- Then goes through normal screening (Inc/Exc with EC codes)
- PRISMA: counted under "Records identified from other methods"

### DB5 is NOT your old Excel:
- PaperSearchTracking.xlsx = your working memory (validation check)
- DB5 = NEW papers found by following citation chains from confirmed papers


## AMENDMENT 3: Year Range Decision

### Recommended approach: TWO-PHASE search

**Phase 1 (PRIMARY): 2012-2025 full range**
- This is what you report in the paper as your search protocol
- Captures the full evolution narrative (Moneta 2012 → I/O Passthru 2024)
- Q1-Q5 run with year filter 2012-2025

**Phase 2 (VALIDATION): Cross-check against Draft 3**
- After screening, verify all 16 papers from Draft 3 appear in your results
- Any Draft 3 paper NOT found by Q1-Q5 → enters via Prior-Work source
- This proves your search was comprehensive

**Why not just 2022-2025?**
- Reviewer will ask: "How do we know your 2012-2021 coverage was systematic?"
- By running Q1-Q5 on the full range, you can say the search was uniform
- Your 2022 survey papers appear naturally in the results, validating your prior work
