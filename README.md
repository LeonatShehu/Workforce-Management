# Workforce Management Analytics

An end-to-end workforce analytics project built on a simulated Workforce Management environment. It analyzes employee schedules, attendance, workload, productivity and KPI performance using **Excel**, a **web dashboard** and a **Power BI project**.

<!-- ![<img width="828" height="790" alt="Screenshot 2026-10-01 at 11 27 00" src="https://github.com/user-attachments/assets/cdca79c8-c342-438c-ac19-2c042eb42a49" />
<img width="1081" height="815" alt="Screenshot 2026-10-01 at 11 27 46" src="https://github.com/user-attachments/assets/00f9e24a-1713-489f-8175-978b654d8565" />
]() -->

---

## Business questions

- How reliable is attendance, and where is absence concentrated (department, shift, day of week)?
- How much of the planned labor time is actually worked?
- How productive is each department, shift and employee?
- Are employees meeting their KPI targets?
- Which employees need attention (high absence, low productivity, below KPI)?

---

## Dataset

`Workforce_Management_Analytics_Dataset.xlsx` is simulated data covering **1–25 September 2026**, **40 employees**, **3 departments** (Customer Service, Operations, Warehouse) and **3 shifts** (Morning, Afternoon, Night).

| Sheet | Rows | Description |
|---|---|---|
| `Workforce_Data` | 1,000 | One row per employee-shift: schedule, attendance, hours, work volume, productivity, KPI target vs. actual, overtime, staffing figures |
| `Employee_Master` | 40 | Employee ID, name, department, employment type, hire year |
| `Daily_Planning` | 75 | Daily roll-up per department |
| `KPI_Summary` | 11 | Headline metrics |

---

## Key results

| Metric | Value |
|---|---|
| Scheduled employee-shifts | 1,000 |
| Present / Late / Absent | 881 / 46 / 73 |
| Attendance rate | 92.7% |
| Absence rate | 7.3% |
| Planned vs. actual hours | 8,000 vs. 7,155 (89.4% utilization) |
| Productivity (volume per hour) | 12.54 |
| Average KPI achievement | 104.5% |
| Overtime hours | 16.5 |

- All three departments fall short of the 95% attendance target set in the Excel assumptions (Warehouse lowest at 91.3%, Operations highest at 93.7%).
- With the default thresholds in the workbook, 10 of 40 employees are flagged "High absence".

---

## Methodology

- **Attendance rate** = (Present + Late) / scheduled shifts.
- **Productivity** = total work volume / total actual hours. This is hours-weighted, so absent rows (0 hours, 0 volume) do not distort it.
- **KPI averages** exclude absent rows, because their KPI is stored as 0.
- **Hours utilization** = actual hours / planned hours.
- **Employee status** uses configurable thresholds: absence rate above 10%, productivity below 85% of the department average, or KPI achievement below 100%.

### Data quality notes

- The staffing columns (`Required_Staff`, `Scheduled_Staff`, `Actual_Staff`, `Staffing_Gap`) look like raw headcounts rather than staff on shift. `Actual_Staff` averages about 14.7 against about 5.4 scheduled, so the staffing gap is about −9 on almost every row. These columns are **excluded** from the analysis until their definition is confirmed.
- `Forecast_Volume` is on a different scale from actual `Work_Volume`, so it is not used as a forecast-accuracy measure.
- The sample is small (about 25 rows per employee) and overtime is rare, so employee-level and overtime findings are indicative only.

---

## What's in this repository

```
.
├── data/
│   └── Workforce_Management_Analytics_Dataset.xlsx
├── excel/
│   └── Workforce_Analysis.xlsx          # Excel analysis layer
├── dashboard/
│   └── Workforce_Dashboard.html         # Interactive web dashboard
└── README.md
```

### 1. Excel analysis layer (`Workforce_Analysis.xlsx`)

- Sheets: README, Dashboard, Assumptions, Dept / Shift / Day summaries, Daily trend, Employee scorecard, Data.
- About 5,000 live formulas (`COUNTIFS`, `SUMIFS`, `AVERAGEIFS`, `INDEX/MATCH`). Change a threshold on the **Assumptions** sheet and everything updates.
- The Dashboard sheet has six KPI cards and four charts.

### 2. Interactive web dashboard (`Workforce_Dashboard.html`)

A self-contained page with filters for department, shift and weekday/weekend. It shows six KPI cards and four charts. Open it in any browser, no install needed.

## Tools

Excel (formulas, conditional formatting, charts)


**Your Name** · [LinkedIn](https://www.linkedin.com/) · [Portfolio](https://github.com/your-username)

## License

Add your preferred license (for example MIT). The dataset is simulated and contains no real employee data.
