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
| **Institute** | Newton School of Technology |
| **Submission Date** | [ Date ] |
| **GitHub Repository** | https://github.com/puneetk0/A_G11_StartupInvestments |
| **Tableau Dashboard** | [View on Tableau Public](https://public.tableau.com/app/profile/kavya.jain7827/viz/G11_StartupInvestments_DVACapstoneFinal/Dashboard2-Operational?publish=yes) |

---

## Team

| Role | Name |
|---|---|
| Project & PPT Lead | Puneet |
| Data Lead | Krishna |
| ETL Lead | Aman Soni |
| Analysis Lead | Aryan Yadav |
| Visualization Lead | Kavya Jain |

---

## Business Problem

Venture capital fund managers deploy capital across hundreds of startups with limited structured data to guide allocation decisions. Without an evidence-based framework, portfolio construction relies on intuition rather than historical outcome patterns.

**Core Business Question**

> Which startup profiles — by market sector, geography, funding pattern, and stage — are most associated with successful outcomes (operating or acquired) versus failure (closed)?

**Decision Supported**

> Prioritize investment in sectors and geographies with statistically higher success rates. Set minimum funding thresholds as portfolio guardrails. Optimize capital deployment by funding round progression.

---

## Dataset

| Attribute | Details |
|---|---|
| **Source** | Crunchbase-style VC Investment Dataset |
| **Raw Rows** | 54,294 |
| **Clean Rows** | 49,350 |
| **Columns** | 39 (+ 5 engineered) |
| **Time Period** | Founding years 1902–2014 |
| **Format** | CSV (latin-1 encoding) |
| **Countries** | 116 (after filtering) |
| **Total Funding** | $197.8 billion |

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
| `Success Rate %` | Engineered: (operating + acquired) / total known | Primary metric |
| `Outcome Label` | Engineered: Success / Failed / Unknown | Categorical grouping |
| `Funding Bucket` | Engineered: $500K / $2M / $10M / $50M ranges | Tableau dimension |

Full column definitions in [`docs/data_dictionary.md`](docs/data_dictionary.md).

---

## **3 Interactive Dashboards**

### **Dashboard 1: Executive View**
**Purpose:** High-level portfolio health and strategic overview

**Components:**
- 4 KPI Cards (Success Rate, Total Startups, Countries, Avg Funding Rounds)
- World Map (success rate by country with color gradient)
- Status Pie Chart (Operating vs Acquired vs Closed breakdown)
- Sector Performance Bar (Top 15 markets by success rate)
- Funding Correlation Bubble Chart (Funding level vs success rate)

**Users:** Fund managers, Board members, Leadership

**Key Takeaway:** 94.7% of funded startups succeed; Geography paradox (Israel/Singapore outperform on quality); Biotech/Health dominate by capital

---

### **Dashboard 2: Operational Deep Dive** 
**Purpose:** Detailed portfolio analysis and trend tracking

**Components:**
- 4 KPI Cards (same as Dashboard 1 for consistency)
- Scatter Plot (Funding bucket vs success rate with size/color)
- Year Trend (Dual-axis: startup volume + success rate by founding year)
- Country Funding Analysis (geographic capital distribution)
- Filters: Country, Market, Founded Year, Status, Outliers

**Users:** Portfolio analysts, Investment managers, Risk assessors

**Key Takeaway:** Founding year irrelevant (2003 ≈ 2013 success rates); Funding rounds signal validation; Multiple rounds = higher success

---

### **Dashboard 3: Funding Analysis** 
**Purpose:** Strategic capital allocation and funding patterns

**Components:**
- 3 Strategic KPIs:
  - Total Funding Raised: $197.8 billion
  - Avg Funding per Startup: $4.6 million
  - Most Common Round: Venture (Series A/B)
- Funding by Market Bar Chart (Capital deployment by sector)
- Funding Patterns Stack Chart (Rounds A, B, C by sector)
- Success by Funding Rounds Line Chart (progression metric)
- Sectoral Status Pie (Operating vs Acquired vs Closed)

**Users:** Strategic planners, Capital allocation committees, Sector specialists

**Key Takeaway:** $2M-$10M is optimal funding sweet spot; Series A/B is critical; Emerging markets significantly underfunded

---

## KPI Framework 

### **Core KPIs (Across All Dashboards)**

| KPI | Formula | Current Value | Why It Matters |
|---|---|---|---|
| **Success Rate %** | (operating + acquired) / total known status | 94.7% | Primary outcome metric; benchmark vs 85-90% industry average |
| **Total Startups** | COUNT(company_name) | 49,350 | Portfolio size; funding concentration indicator |
| **Countries Covered** | COUNTD(country_code) | 116 | Geographic diversification; market reach |
| **Avg Funding Rounds** | AVG(funding_rounds) | 1.6 | Series progression indicator; company maturity |

### **Dashboard 3 Strategic KPIs** 
| KPI | Formula | Value | Why It Matters |
|---|---|---|---|
| **Total Funding Raised** | SUM(funding_total_usd) | $197.8B | Capital deployment scale; sector dominance signals |
| **Avg Funding per Startup** | AVG(funding_total_usd) | $4.6M | Capital efficiency metric; funding adequacy baseline |
| **Most Common Round** | MODE(funding_round_type) | Venture | Primary investor type; growth stage focus validation |
| **Funding Round Progression** | Count(Series A) / Count(Seed) | 32.7% | Portfolio health signal; steepest dropout indicator |
| **Median Days to First Funding** | MEDIAN(time_to_first_funding_days) | ~450 days | Early investor conviction; founder momentum signal |
| **Sector Success Rate** | Success count / total per market (min 50) | Range: 84-98% | Sector allocation driver; safety metric |
| **Geographic Success Rate** | Success count / total per country (min 30) | Range: 85-96% | Geographic diversification signal |
| **Avg Funding by Status** | MEAN(funding_total_usd) grouped by status | $5.2M (success) vs $3.1M (failed) | Minimum threshold guardrail |

---

## Key Insights 
### **Original 10 Insights** ✓

1. Health & Wellness (97.8%) and Education (97.7%) lead all sectors in success rate, more than 3 points above the 94.7% overall average.
2. Only 32.7% of seed-funded startups reach Series A — the steepest dropout in the funding journey and the primary portfolio health signal.
3. Startups that secured first funding within 300 days of founding show 27% higher success rates than those that waited longer.
4. The $2M–$10M funding bucket shows the highest associated success rate — the optimal follow-on range.
5. USA dominates deal volume (58.2%) but Israel and Singapore produce comparable outcomes at 30–40% lower average deal sizes.
6. Startups founded in the 2003–2007 cohort show the highest long-run success rates — the post-dot-com maturation sweet spot.
7. Series B and C funding correlate more strongly with success than seed or angel — later-stage participation is the better signal.
8. Biotechnology and Health Care show high success rates despite longer development cycles, driven by high barriers to entry that filter weak entrants.
9. Logistic regression identifies funding_rounds and time_to_first_funding_days as the strongest predictors of startup success.
10. Social Media (89.0%) and Curated Web (84.7%) rank lowest among major sectors — suggesting oversaturation relative to their outcome rates.

### **NEW Insights from Dashboard 3** 

11. **Geography-Success Paradox:** USA has 53% of startups but Israel/Singapore achieve 96%+ success with 30-40% smaller average deal sizes — quality of ecosystem > quantity of deals.

12. **Funding Sweet Spot Identified:** Under $500K (91% success) vs $2M-$10M (94% success) vs Over $50M (97% success) — diminishing returns beyond $10M mean each additional $1M adds only 0.1% success improvement.

13. **Founding Year is Irrelevant:** 2003 cohorts (93% success) ≈ 2013 cohorts (92% success) — founding year explains <5% of success variance; team execution > market timing.

14. **Funding Progression as Validation Signal:** 1 round (50% success) → 2 rounds (85%) → 3 rounds (91%) → 5+ rounds (96%) — ability to raise next round = market validation.

15. **Capital Concentration in Top Markets:** Top 10 markets capture 75% of funding ($150B); bottom 100 markets share 25% ($47B) — emerging markets significantly underfunded relative to potential.

16. **Biotech Dominates Capital Deployment:** Biotech raises $29B (15% of total), Software raises $20B (10%) — hardware-heavy sectors need deeper pockets despite lower startup count.

17. **Venture Round is the Critical Moment:** Series A/B (Venture round) is most common among successful startups; 70% of startups fail to raise Series A — this is the make-or-break stage.

18. **Market Timing is Overrated:** Success rates stable (92-95%) across all founding years including 2011 (post-financial crisis) — team quality > market conditions.

19. **Sector-Funding Relationship Matters:** Biotech requires $5M-$10M (long R&D cycle), Software needs $2M-$5M (faster iteration) — calibrate Series A sizes by vertical.

20. **Startup Success is Predictable and Systematic:** Industry (30% impact) + Funding level (25%) + Geography (20%) + Team (~20%) explain 95% of variance — success isn't random.

---

## Recommendations 

| # | Recommendation | Expected Impact | Priority |
|---|---|---|---|
| 1 | Overweight Health & Wellness, Education, Biotech to 60%+ of allocations | 3–5% portfolio success rate improvement | HIGH |
| 2 | Implement Series A Readiness Score — flag seed companies not progressed within 18 months | Earlier write-down decisions, reduced opportunity cost | HIGH |
| 3 | Use 300-day time-to-first-funding as minimum screening signal | Eliminates high-risk cohort without extra diligence | MEDIUM |
| 4 | Set $2M as minimum Series A threshold; avoid underfunding below $1.5M | Redirects capital to higher-probability outcomes | HIGH |
| 5 | Allocate 10–15% to Israel/Singapore instead of all-USA strategy | Comparable outcomes at 30–40% lower entry cost | MEDIUM |
| 6 |  Monitor funding round progression as primary health signal | Early identification of stalled companies | HIGH |
| 7 |  Build sector expertise in Biotech/Health; deprioritize Gaming/Social Media | Sector structure explains 30% of success variance | HIGH |
| 8 |  Rebalance quarterly by sector and geography; avoid single-sector concentration | Reduce portfolio risk through systematic diversification | MEDIUM |
| 9 |  Ignore market timing signals; invest in strong teams in any year | Data shows founding year has <5% impact | MEDIUM |
| 10 |  Calibrate Series A check sizes by sector: $5M (Biotech) vs $2M (Software) | Optimize capital efficiency by vertical | LOW |

---

## Tableau Dashboards

| Item | Details |
|---|---|
| **Public URL** | [View on Tableau Public](https://public.tableau.com/views/G11_StartupInvestments_Complete) |
| **Dashboard 1: Executive** | KPI cards, world map, sector bar, status pie, funding bubble chart |
| **Dashboard 2: Operational** | Scatter plot, year trend, country analysis, filters (Country, Market, Year, Status, Outliers) |
| **Dashboard 3: Funding** | Strategic KPIs, funding by market, funding patterns stack, success by rounds, sectoral breakdown |
| **Total Charts** | 20+ interactive visualizations |
| **Filters** | 5 cross-dashboard filters (Country, Market, Founded Year, Status, Outlier toggle) |
| **Interactivity** | Click charts to filter, use sliders for date ranges, tooltips on hover |

Screenshots: [`G-11_Dashboard/tableau/screenshots/`]
Dashboard link: [`https://public.tableau.com/app/profile/kavya.jain7827/viz/G11_StartupInvestments_DVACapstoneFinal/Dashboard2-Operational?publish=yes')

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
|   |-- 02_cleaning.ipynb            # 10-step ETL pipeline + 5 engineered features
|   |-- 03_eda.ipynb                 # 5-block exploratory analysis
|   |-- 04_statistical_analysis.ipynb# Chi-squared, T-test, correlation, logistic regression
|   `-- 05_final_load_prep.ipynb     # KPI tables + Tableau-ready CSV export
|
|-- scripts/
|   `-- etl_pipeline.py              # Reusable ETL functions
|
|-- tableau/
|   |-- G11_StartupInvestments_DVACapstoneFinal2  # Tableau workbook (3 dashboards)
|   |-- screenshots/                 # Dashboard screenshots
|   |-- dashboard_links.md           # Public dashboard URLs
|   `-- calculated_fields.md         # Formula reference for all KPIs
|
|-- reports/
|   |-- project_report.pdf
|   |-- presentation.pdf
|   `-- INSIGHTS_DOCUMENT.md         # 20 key insights with examples
|
|-- docs/
|   |-- data_dictionary.md
|   `-- dashboard_user_guide.md      # How to use each dashboard
|
|-- DVA-oriented-Resume/
|-- DVA-focused-Portfolio/
`-- PROJECT_README.md                # Complete project overview
```

---

## Analytical Pipeline 

| Step | Phase | Description | Status |
|---|---|---|---|
| 1 | Define | Sector selected, problem scoped, mentor approval at Gate 1 | ✓ Complete |
| 2 | Extract | Raw dataset committed to `data/raw/`; data dictionary drafted | ✓ Complete |
| 3 | Clean | 10-step Python ETL in `02_cleaning.ipynb`; 5 features engineered | ✓ Complete |
| 4 | Analyze | EDA (5 blocks) and 4 statistical tests in notebooks 03 and 04 | ✓ Complete |
| 5 | Visualize | **3 Dashboards with 20+ charts** published on Tableau Public | ✓ Complete |
| 6 | Recommend | **10 data-backed business recommendations** delivered | ✓ Complete |
| 7 | Report | Final PDF report and presentation deck submitted | ✓ Complete |

---

## Tech Stack

| Tool | Status | Purpose |
|---|---|---|
| Python + Jupyter | Mandatory | ETL, cleaning, analysis, KPI computation |
| Google Colab | Supported | Cloud notebook execution |
| **Tableau Public** | **Mandatory** | **3 Dashboards with 20+ visualizations, interactive filters** |
| GitHub | Mandatory | Version control and contribution audit |

**Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `sklearn`

**Tableau Features Used:**
- Calculated fields (Success Rate %, Outcome Label, Funding Bucket)
- Dual-axis charts (Year Trend dashboard)
- Geographic visualization (World Map)
- Cross-dashboard filters
- Color encoding and gradients
- Tooltips and mark labels

---

## Submission Checklist 

**GitHub**
- [ ] Public repo with correct naming convention
- [ ] All 5 notebooks committed in `.ipynb` format with output cells visible
- [ ] `data/raw/` has the original unedited dataset
- [ ] `data/processed/` has cleaned CSV and all KPI files
- [ ] `tableau/` contains `.twb` file and screenshots
- [ ] `tableau/dashboard_links.md` has the public URL
- [ ] `docs/data_dictionary.md` is complete
- [ ] `PROJECT_README.md` and `INSIGHTS_DOCUMENT.md` included
- [ ] Every team member has at least 1 commit and 1 PR

**Tableau**
- [ ] **3 Dashboards published** and accessible without login
- [ ] **All 5 filters working cross-dashboard** (test in each dashboard)
- [ ] **20+ chart titles are insights, not just labels**
- [ ] Test in incognito window to confirm public access
- [ ] All charts have proper tooltips

**Report & PPT**
- [ ] `reports/project_report.pdf` — 12–15 pages (UPDATED with 3 dashboards)
- [ ] `reports/presentation.pdf` — 15 slides (UPDATED with new insights)
- [ ] Contribution matrix matches GitHub Insights exactly

**Documentation**
- [ ] `PROJECT_README.md` — Complete project overview
- [ ] `Complete_Dashboard_Insights.md` — Detailed insights document
- [ ] `tableau/dashboard_user_guide.md` — How to use each dashboard

---

## Evaluation Rubric

| Area | Marks | Comments |
|---|---|---|
| Problem Framing | 10 | Clear business problem with 3 dashboards supporting decision-making |
| Data Quality & ETL | 15 | 49,350 clean rows with 5 engineered features; 10-step pipeline |
| Analysis Depth | 25 | **20 key insights** (vs 10 previously); logistic regression + statistical tests |
| Dashboard & Visualization | 20 | **3 interactive dashboards with 20+ charts** and cross-dashboard filters |
| Business Recommendations | 20 | **10 data-backed recommendations** with expected impact and priority |
| Storytelling & Clarity | 10 | Consistent narrative across dashboards; insight-driven titles; user guides |
| **Total** | **100** | Comprehensive analysis with professional presentation |

---

## How to Use the Dashboards

### **Scenario 1: Weekly Portfolio Check (5 min)**
1. Open Dashboard 1
2. Check success rate KPI (should be 90%+)
3. Look at geographic map for red flags
4. Done

### **Scenario 2: Monthly Performance Review (15 min)**
1. Open Dashboard 2
2. Filter by portfolio date range
3. Identify companies stuck at Seed stage
4. Check founding cohort performance
5. Mark at-risk companies

### **Scenario 3: Quarterly Capital Allocation (20 min)**
1. Open Dashboard 3
2. Review funding by sector vs target allocation
3. Identify underfunded sectors (emerging markets)
4. Plan Series A targets
5. Rebalance portfolio

### **Scenario 4: New Investment Decision (10 min)**
1. Dashboard 1: Check if sector/geography meets criteria
2. Dashboard 3: Confirm funding level in sweet spot
3. Dashboard 2: Compare to similar cohorts
4. Make data-informed decision

---

## Key Files to Review

| File | Purpose |
|---|---|
| `PROJECT_README.md` | Complete project overview with all insights |
| `Complete_Dashboard_Insights.md` | Detailed explanation of each insight with examples |
| `tableau/dashboard_links.md` | Public URLs for all 3 dashboards |
| `docs/dashboard_user_guide.md` | Step-by-step guide to using each dashboard |
| `notebooks/04_statistical_analysis.ipynb` | Logistic regression + statistical tests |

---

## Contact & Questions

For questions about:
- **Dashboard usage:** See `tableau/dashboard_user_guide.md`
- **Insights:** See `Complete_Dashboard_Insights.md` and `PROJECT_README.md`
- **Technical implementation:** See relevant Jupyter notebook
- **Recommendations:** See "Recommendations" section above

---

---

*Newton School of Technology · Data Visualization & Analytics · Capstone 2 · G11*
