# G11 — Startup Success Prediction Using Global VC Investment Data

> **Newton School of Technology | Data Visualization & Analytics | Capstone 2**
> A 2-week industry simulation analyzing 54,294 global startup investment records to build a data-backed portfolio allocation framework for VC fund managers.

---

## Project Overview

| Field | Details |
|---|---|
| **Project Title** | Startup Success Prediction Using Global VC Investment Data |
| **Sector** | Finance / Venture Capital |
| **Team ID** | A-G11 |
| **Section** | A |
| **Faculty Mentor** | [ Mentor Name ] |
| **Institute** | Newton School of Technology |
| **Submission Date** | [ Date ] |
| **GitHub Repository** | https://github.com/puneetk0/A_G11_StartupInvestments |
| **Tableau Dashboard** | [ Paste Tableau Public URL here ] |

---

## Team

| Role | Name |
|---|---|
| Project & PPT Lead | Puneet
| Data Lead | Krishna
| ETL Lead | Aman Soni
| Analysis Lead | Aryan Yadav
| Visualization Lead | Kavya

---

## Business Problem

Venture capital fund managers deploy capital across hundreds of startups with limited structured data to guide allocation decisions. Without an evidence-based framework, portfolio construction relies on intuition rather than historical outcome patterns.

**Core Business Question**

> Which startup profiles — by market sector, geography, funding pattern, and stage — are most associated with successful outcomes (operating or acquired) versus failure (closed)?

**Decision Supported**

> Prioritize investment in sectors and geographies with statistically higher success rates. Set minimum funding thresholds as portfolio guardrails.

---

## Dataset

| Attribute | Details |
|---|---|
| **Source** | Crunchbase-style VC Investment Dataset |
| **Raw Rows** | 54,294 |
| **Clean Rows** | 49,436 |
| **Columns** | 39 (+ 2 engineered) |
| **Time Period** | Founding years 1902–2014 |
| **Format** | CSV (latin-1 encoding) |
| **Countries** | 140+ |

**Key Columns**

| Column | Description | Role |
|---|---|---|
| `status` | operating / acquired / closed / unknown | Target variable |
| `market` | Primary industry sector | Key grouping dimension |
| `funding_total_usd` | Total USD raised (all rounds) | Primary financial KPI |
| `country_code` | ISO 3-letter country code | Geographic dimension |
| `funding_rounds` | Number of funding rounds completed | Progression feature |
| `time_to_first_funding_days` | Engineered: days from founding to first funding | Logistic regression feature |
| `is_outlier` | Engineered: True if funding > Q3 + 3×IQR | Tableau filter toggle |

Full column definitions in [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## KPI Framework

| KPI | Formula | Why It Matters |
|---|---|---|
| Startup Success Rate | (operating + acquired) / total known status | Primary outcome metric |
| Funding Round Progression | Count(Series A > 0) / Count(Seed > 0) | Portfolio health signal |
| Median Days to First Funding | MEDIAN(time_to_first_funding_days) | Early investor conviction signal |
| Sector Success Rate | Success count / total per market (min 50) | Sector allocation driver |
| Geographic Success Rate | Success count / total per country (min 30) | Geographic diversification signal |
| Avg Funding by Status | MEAN(funding_total_usd) grouped by status | Minimum threshold guardrail |

---

## Key Insights

1. Health & Wellness (97.8%) and Education (97.7%) lead all sectors in success rate, more than 3 points above the 94.7% overall average.
2. Only 32.7% of seed-funded startups reach Series A — the steepest dropout in the funding journey and the primary portfolio health signal.
3. Startups that secured first funding within 300 days of founding show 27% higher success rates than those that waited longer.
4. The \$2M–\$10M funding bucket shows the highest associated success rate — the optimal follow-on range.
5. USA dominates deal volume (58.2%) but Israel and Singapore produce comparable outcomes at 30–40% lower average deal sizes.
6. Startups founded in the 2003–2007 cohort show the highest long-run success rates — the post-dot-com maturation sweet spot.
7. Series B and C funding correlate more strongly with success than seed or angel — later-stage participation is the better signal.
8. Biotechnology and Health Care show high success rates despite longer development cycles, driven by high barriers to entry that filter weak entrants.
9. Logistic regression identifies funding_rounds and time_to_first_funding_days as the strongest predictors of startup success.
10. Social Media (89.0%) and Curated Web (84.7%) rank lowest among major sectors — suggesting oversaturation relative to their outcome rates.

---

## Recommendations

| # | Recommendation | Expected Impact |
|---|---|---|
| 1 | Overweight Health & Wellness, Education, Biotechnology, and Health Care to 60%+ of new allocations | 3–5% improvement in portfolio success rate |
| 2 | Implement a Series A Readiness Score — flag seed companies not progressed within 18 months | Earlier write-down decisions, reduced opportunity cost |
| 3 | Use 300-day time-to-first-funding as a minimum screening signal | Eliminates high-risk cohort without extra diligence cost |
| 4 | Set \$2M as minimum meaningful follow-on threshold | Redirects capital to higher-probability outcomes |
| 5 | Allocate 10–15% of deal flow to Israel and Singapore | Comparable outcomes at 30–40% lower entry cost |

---

## Tableau Dashboard

| Item | Details |
|---|---|
| **Public URL** | [ Paste Tableau Public URL ] |
| **Dashboard 1** | Executive view: KPI cards, world map (success rate by country), sector bar, funding funnel, status pie |
| **Dashboard 2** | Operational drill-down: scatter plot, country table, year trend, stage success rates |
| **Filters** | Country Code, Market Sector, Founded Year (slider), Status, Outlier toggle |

Screenshots: [`tableau/screenshots/`](tableau/screenshots/)
Dashboard links: [`tableau/dashboard_links.md`](tableau/dashboard_links.md)

---

## Repository Structure

```
A_G11_StartupInvestments/
|
|-- README.md
|
|-- data/
|   |-- raw/                         # investments_VC.csv — never edited
|   `-- processed/                   # investments_VC_cleaned.csv + KPI CSVs
|
|-- notebooks/
|   |-- 01_extraction.ipynb          # Load and inventory raw data
|   |-- 02_cleaning.ipynb            # 10-step ETL pipeline
|   |-- 03_eda.ipynb                 # 5-block exploratory analysis
|   |-- 04_statistical_analysis.ipynb# Chi-squared, T-test, correlation, logistic regression
|   `-- 05_final_load_prep.ipynb     # KPI tables + Tableau-ready CSV export
|
|-- scripts/
|   `-- etl_pipeline.py
|
|-- tableau/
|   |-- screenshots/
|   `-- dashboard_links.md
|
|-- reports/
|   |-- project_report.pdf
|   `-- presentation.pdf
|
|-- docs/
|   `-- data_dictionary.md
|
|-- DVA-oriented-Resume/
`-- DVA-focused-Portfolio/
```

---

## Analytical Pipeline

| Step | Phase | Description |
|---|---|---|
| 1 | Define | Sector selected, problem scoped, mentor approval at Gate 1 |
| 2 | Extract | Raw dataset committed to `data/raw/`; data dictionary drafted |
| 3 | Clean | 10-step Python ETL in `02_cleaning.ipynb`; 2 features engineered |
| 4 | Analyze | EDA (5 blocks) and 4 statistical tests in notebooks 03 and 04 |
| 5 | Visualize | Two-view Tableau dashboard published on Tableau Public |
| 6 | Recommend | 5 data-backed business recommendations delivered |
| 7 | Report | Final PDF report and presentation deck submitted |

---

## Tech Stack

| Tool | Status | Purpose |
|---|---|---|
| Python + Jupyter | Mandatory | ETL, cleaning, analysis, KPI computation |
| Google Colab | Supported | Cloud notebook execution |
| Tableau Public | Mandatory | Dashboard design, publishing, and sharing |
| GitHub | Mandatory | Version control and contribution audit |

**Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `sklearn`

---

## Submission Checklist

**GitHub**
- [ ] Public repo with correct naming convention
- [ ] All 5 notebooks committed in `.ipynb` format with output cells visible
- [ ] `data/raw/` has the original unedited dataset
- [ ] `data/processed/` has cleaned CSV and all KPI files
- [ ] `tableau/screenshots/` has at least 4 screenshots
- [ ] `tableau/dashboard_links.md` has the public URL
- [ ] `docs/data_dictionary.md` is complete
- [ ] Every team member has at least 1 commit and 1 PR

**Tableau**
- [ ] Dashboard accessible without login (test in incognito)
- [ ] At least 5 interactive filters working and cross-dashboard
- [ ] Chart titles are insights, not labels

**Report & PPT**
- [ ] `reports/project_report.pdf` — 10–15 pages
- [ ] `reports/presentation.pdf` — 12 slides
- [ ] Contribution matrix matches GitHub Insights exactly

---

---

## Evaluation Rubric

| Area | Marks |
|---|---|
| Problem Framing | 10 |
| Data Quality & ETL | 15 |
| Analysis Depth | 25 |
| Dashboard & Visualization | 20 |
| Business Recommendations | 20 |
| Storytelling & Clarity | 10 |
| **Total** | **100** |

---

*Newton School of Technology · Data Visualization & Analytics · Capstone 2 · G11*
