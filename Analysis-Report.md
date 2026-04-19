# Lown Hospital Index Analysis (2025–2026)
### A Healthcare Analytics Project

---

## Project Overview

This project analyses the Lown Hospital Index dataset to explore the relationship between hospital inclusivity, clinical outcomes, patient safety, and patient experience across 3,956 U.S. hospitals.

The central question driving this analysis:

> "Do hospitals that prioritize equitable care perform differently on clinical outcomes and patient experience compared to those that don't?"

---

## Dataset

- **Source:** Lown Institute Hospital Index (2025–2026)
- **Total hospitals:** 3,956
- **Tool used:** SQL (SQLite)
- **Key variables:**
  - `TIER_1_RANK_Lown_Composite` — overall composite rank
  - `BADGE_TIER_3_Inclusivity` — inclusivity badge (1 = awarded, 0 = not awarded)
  - `TIER_4_STARS_*` — sub-scores across outcomes, safety, experience and inclusivity
  - `TYPE_urban` — urban or rural classification

---

## Data Cleaning

- Checked for duplicate rows using `SELECT DISTINCT *`
- Verified `BADGE_TIER_3_Inclusivity` contains only 0 and 1 values
- Hospitals with NULL composite rank excluded from ranking analysis but analysed separately
- No rows deleted — all cleaning decisions documented

---

## Key Findings

### 1. Inclusivity Badge Distribution

- Total hospitals: **3,956**
- Hospitals with inclusivity badge: **200 (~5.1%)**
- Unranked hospitals: **110** (5 inclusive, ~4.5%)

### 2. Inclusivity vs Ranking Tier

| Tier | Inclusive | Rate |
|---|---|---|
| Top 50 | 9 | 18% |
| Bottom 50 | 0 | 0% |
| Unranked | 5 | 4.5% |

Badge hospitals rank significantly higher on average:
- **Badge hospitals:** avg rank 723
- **Non-badge hospitals:** avg rank 1,076

> Inclusive hospitals sit in roughly the top 18% on average, compared to top 27% for non-inclusive hospitals.

### 3. Clinical Outcomes and Safety

Comparing badge vs non-badge hospitals on a 1–5 star scale:

| Metric | No Badge | Badge |
|---|---|---|
| 30-day mortality | 4.06 | 4.07 |
| CLABSI (bloodstream infection) | 3.44 | 3.43 |
| CAUTI (urinary infection) | 3.51 | 3.86 |
| Patient experience | 3.31 | 2.79 |

**Key insight:** Inclusive hospitals perform virtually identically on clinical outcomes and safety. The only meaningful gap is in patient experience (0.52 difference), where inclusive hospitals score lower.

### 4. Why Do Inclusive Hospitals Score Lower on Patient Experience?

Inclusive hospitals serve significantly more disadvantaged populations:

| Dimension | No Badge | Badge |
|---|---|---|
| Income score | 2.88 | 4.70 |
| Race score | 2.91 | 3.99 |
| Education score | 2.89 | 4.46 |

Higher scores indicate the hospital serves more low-income, minority, and less-educated patients. Research consistently shows these patient groups tend to rate experiences lower in satisfaction surveys regardless of care quality — a known limitation of HCAHPS survey methodology.

### 5. Urban vs Rural Breakdown

The patient experience gap exists in both urban and rural settings:

| Urban type | No Badge | Badge |
|---|---|---|
| Rural | 3.34 | 2.84 |
| Urban | 3.33 | 2.76 |

Geography does not explain the gap — it is consistent across both settings, further supporting the population-mix hypothesis.

### 6. Hospital Size and Inclusivity

| Size | Total | Inclusive | Rate |
|---|---|---|---|
| CAH (Critical Access) | 896 | 100 | 11.2% |
| XL | 38 | 2 | 5.4% |
| L | 714 | 31 | 4.3% |
| M | 805 | 29 | 3.6% |
| S | 515 | 11 | 2.1% |
| XS | 638 | 8 | 1.3% |

Critical Access Hospitals — small, rural hospitals serving underserved communities — show the highest inclusivity rate at 11.2%.

---

## Conclusion

> "Hospitals with the inclusivity badge rank significantly higher on average and match non-inclusive hospitals on clinical outcomes and safety. Their lower patient experience scores are likely a reflection of the more disadvantaged populations they serve, rather than inferior care quality. This suggests that equitable care and clinical excellence are not mutually exclusive — but that current patient satisfaction metrics may inadvertently penalise hospitals that serve the most vulnerable communities."

---

## SQL Queries

All queries used in this analysis are documented in `/queries.sql`

---

## Next Steps

- Tableau dashboard visualising key findings
- Statistical significance testing (chi-square) on badge vs rank tier distribution
- Deeper analysis of individual Lown sub-score dimensions

---

## Author

- **Tool:** SQLite
- **Dataset:** Lown Institute Hospital Index 2025–2026
