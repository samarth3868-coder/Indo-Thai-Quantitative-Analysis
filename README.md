# Indo Thai Quantitative Data Analyst Intern — Take-Home Assessment

## 1. Project Overview

This project analyses how BSE corporate announcements are associated with short-term stock-price and trading-volume movements, and examines post-earnings price drift for five supplied BSE-listed stocks.

The analysis focuses on:

- Announcement timestamp validation
- Event clustering and market-event consolidation
- Short-term price impact
- Trading-volume impact
- Subject-wise statistical analysis
- Stock-wise announcement analysis
- Price-conditioned post-earnings drift (PEAD)

## 2. Stocks Analysed

The five supplied stocks are:

- Reliance Industries
- HDFC Bank
- FSN E-Commerce Ventures (Nykaa)
- Hindustan Aeronautics
- Rail Vikas Nigam

## 3. Methodology

### Announcement Processing

A valid `DissemDT` is preferred as the announcement timestamp, with `DT_TM` used as a fallback when required.

### Event Clustering

Announcements for the same stock separated by 30 minutes or less are grouped into one initial event cluster.

After market alignment, multiple clusters mapping to the same stock and effective one-minute market bar are consolidated to avoid double-counting the same market reaction.

### Event Alignment

Each announcement is aligned to the first complete tradable one-minute bar at or after dissemination.

Pre-open, after-hours, weekends, holidays and non-standard trading sessions are handled using the observed trading-session timestamps.

### Price Impact

Returns are calculated over:

- 5 minutes
- 30 minutes
- 60 minutes
- D0 session close

Longer-term returns are calculated over:

- D+1
- D+3
- D+5
- D+10
- D+20

### Volume Impact

Trading-volume activity is compared with a rolling historical baseline based on comparable session-minute observations.

### Subject Classification

Announcements are assigned to eight transparent rule-based categories:

- Financial Results
- Corporate Actions
- Business / Strategic
- Board / Management
- Investor / Analyst
- Credit / Financing
- Regulatory / Compliance
- Other

### Statistical Analysis

The analysis reports:

- Mean
- Median
- Standard deviation
- Bootstrap 95% confidence intervals
- One-sample t-test versus zero
- Kruskal-Wallis comparison across announcement subjects

### PEAD

Financial Results events are used for a price-conditioned post-earnings drift analysis.

The initial D0 return determines the direction, and subsequent returns are examined at D+1, D+3, D+5, D+10 and D+20.

Because analyst expectations and earnings-surprise data were not supplied, this is treated as price-conditioned PEAD rather than surprise-based PEAD.

## 4. Final Analysis Flow

```text
Corporate Announcements
        ↓
Data Validation
        ↓
Subject Taxonomy
        ↓
30-Minute Event Clustering
        ↓
Stock Data Validation
        ↓
Timestamp / Trading-Bar Alignment
        ↓
Event-Level Price & Volume Metrics
        ↓
Market-Bar Event Consolidation
        ↓
Subject & Stock Analysis
        ↓
Kruskal-Wallis Test
        ↓
PEAD Analysis
        ↓
Figures + Report