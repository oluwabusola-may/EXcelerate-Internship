[README (6).md](https://github.com/user-attachments/files/30657707/README.6.md)
# DePaul University — International Applications Analysis
### Excelerate 2026 Internship | Team Haven | Oluwabusola Oyenuga

---

## Project Overview

This project is a full end-to-end data analytics case study completed during the Excelerate 2026 virtual internship. The dataset came from DePaul University's Slate CRM system and contains **7,543 international graduate applications** spanning **95 countries** and **153 programs**.

The work ran across four weeks, each building on the last — from raw data cleaning through to a live interactive Power BI dashboard presented to stakeholders.

> **Core finding:** Non-admitted applicants are almost never contacted — only 23.25% have a logged call, compared to 76.75% of admitted applicants. This isn't an admissions quality problem. It's a contact problem.

---

## The Story in One Line

*The pipeline isn't a quality problem — it's an outreach problem.*

---

## Week-by-Week Breakdown

### Week 1 — Data Cleaning
**Tools:** Excel, Power Query

The raw Slate CRM export had several issues before any analysis could begin:

- **141 phone numbers** stored in scientific notation (e.g. `9.17E+11`) — converted back to full digits
- **1,332 inconsistent status labels** in the Comments field (case variants, trailing punctuation, synonym phrases) — standardized down to ~700 categories
- **10 missing Country values** and **3 missing Program Name values** — filled using pattern matching against the Intake field
- **"N/A" text ≠ true blank** in the Outcome_1 column — this distinction mattered significantly for DAX filter logic in Power BI
- **Year anomalies** (2022: 1 record, 2026: 41 records) — flagged with a `Year_Flag` column rather than deleted, preserving the audit trail

**Deliverable:** Cleaned dataset exported as `DePaul_Cleaned_PowerBI.xlsx` with three additional helper columns (`Has_Call_Log`, `Has_Admit_Date`, `Admit_Status`) built for use in the dashboard.

---

### Week 2 — Visualization Report
**Tools:** Excel, Power Query, Matplotlib

A before/after visualization report documenting the cleaning impact and first-pass distribution analysis:

- Missing value comparison (before vs after)
- Status category consolidation chart
- Country distribution (India: 53.7% of all applications)
- Program distribution (Business Analytics + Computer Science: ~26% combined)
- Year anomaly flagging

**Deliverable:** `DePaul_Cleaning_Report.xlsx` (4 sheets) + `DePaul_Cleaning_Report.docx`

---

### Week 3 — Interactive Dashboard
**Tool:** Power BI Desktop

A single-page Power BI dashboard built around one argument: the outreach gap.

**Dashboard components:**
| Zone | Visual Type | Purpose |
|---|---|---|
| Header band | Text box | Title + narrative subtitle |
| 4 KPI cards | Card visuals | Total apps, call coverage, non-admit contact rate, transcript stall rate |
| Hero chart | 100% Stacked Bar | Admitted vs non-admitted call log coverage |
| Narrative panel | Text box | 3-sentence explanation of the core finding |
| Support chart 1 | Column chart | Call outcome breakdown (transcript stall dominates at 53%) |
| Support chart 2 | Horizontal bar | Call log coverage by program |
| Support chart 3 | Horizontal bar | Evaluation completion by country |
| Action panel | Text box | 3 recommendations |

**Key DAX measures written:**
```
Call Log Coverage =
DIVIDE(
  CALCULATE(COUNTROWS('Cleaned Data'), 'Cleaned Data'[Has_Call_Log]="Yes"),
  [Total Applications]
)

Non-Admit Call Coverage =
CALCULATE([Call Log Coverage], 'Cleaned Data'[Admit_Status]="Not Admitted")

Transcript Stall Rate =
DIVIDE(
  CALCULATE(COUNTROWS('Cleaned Data'),
    'Cleaned Data'[Outcome_1] IN {"Missing 0 Transcript (NOT Study Group)",
    "Missing >1 Transcript (NOT Study Group)"}),
  CALCULATE(COUNTROWS('Cleaned Data'), NOT(ISBLANK('Cleaned Data'[Outcome_1])))
)
```

**Deliverable:** Power BI `.pbix` file + `Week3_Oluwabusola_Oyenuga_DashboardReport.docx`

---

### Week 4 — Final Presentation
**Tools:** PowerPoint, Word

A 10-slide final presentation package consolidating all three weeks, delivered as a live team presentation (3 speakers, 8 minutes including a 2-minute dashboard video walkthrough).

**Deliverable:** `Week4_Oluwabusola_Oyenuga_FinalPresentationPackage.pptx`

---

## Key Findings

### 1. The Outreach Gap
| Group | Call Log Coverage |
|---|---|
| Admitted applicants | 76.75% |
| Non-admitted applicants | 23.25% |

Non-admitted applicants are not being turned down after review — they are largely absent from the outreach process entirely.

### 2. Transcript Collection is the Dominant Bottleneck
Of 1,806 logged calls, **53% are stalled on a missing transcript** — more than three times the next largest call outcome. This is a process problem, not a judgment call.

### 3. Counselor Coverage is Uneven by Program
| Program | Call Coverage |
|---|---|
| Computer Science | 68.0% |
| Information Systems | 63.8% |
| Data Science | 63.1% |
| Business Analytics | 60.4% |
| Artificial Intelligence | 58.3% |
| Cybersecurity | 52.6% |

Cybersecurity and AI trail comparable programs by 10–15 percentage points with no clear reason in the data.

### 4. Geography: Nigeria, Ghana, and the US All Cluster Below 17%
| Country | Evaluation Completion |
|---|---|
| Pakistan | 33.3% |
| Nepal | 29.6% |
| India | 23.2% |
| China | 21.6% |
| Ghana | 17.0% |
| United States | 16.9% |
| Nigeria | 15.6% |

The US appearing alongside Nigeria and Ghana — countries with very different logistical contexts — suggests the cause is internal process rather than geography.

---

## Recommendations

1. **Automate transcript reminders** at the point of submission — targets the single largest blocker (53% of stalled calls) without adding to counselor workload
2. **Rebalance counselor coverage** toward Cybersecurity and AI, with a minimum per-program coverage floor (recommended: 60%)
3. **Audit Nigeria, Ghana, and US pipelines** specifically — the shared pattern despite different contexts points to something process-specific worth investigating

---

## Tools & Technologies

| Tool | Used For |
|---|---|
| Microsoft Excel | Data cleaning, Power Query transforms |
| Power Query | Data loading, column transformations |
| Power BI Desktop | Interactive dashboard, DAX measures |
| DAX | Calculated columns and measures |
| Matplotlib | Visualization report charts |
| PowerPoint | Final presentation deck |


---

## About This Project

**Internship:** Excelerate 2026 Virtual Internship  
**Team:** Team Haven  
**Duration:** 4 weeks (June 2026)  
**Analyst:** Oluwabusola Oyenuga  
**GitHub:** [github.com/oluwabusola-may](https://github.com/oluwabusola-may)  
**LinkedIn:** [linkedin.com/in/oluwabusola-oyenuga](https://linkedin.com/in/oluwabusola-oyenuga)

---

*Dataset used under internship agreement with Excelerate and DePaul University. Raw data not included in this repository.*
