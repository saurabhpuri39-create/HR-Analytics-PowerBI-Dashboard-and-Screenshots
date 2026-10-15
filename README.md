# HR Analytics & Employee Attrition Dashboard

**Power BI Portfolio Project | HR Analytics | Workforce Insights | Employee Attrition**

An interactive **five-page Power BI dashboard** exploring workforce composition, employee attrition, compensation, performance, and rule-based retention risk using **1,470 employee records**.

> **Project scope:** Five main dashboard pages. Employee Satisfaction & Work-Life Balance is **not** a separate dashboard page. Satisfaction is still analyzed as a factor on the Attrition Analysis page.

## Project Overview

**Business problem:** HR teams need a clear view of workforce composition, where attrition is concentrated, how employee characteristics relate to departures, and which employee groups may warrant further review.

**Objectives:**
- Monitor headcount, attrition, and retention KPIs.
- Compare attrition across departments, tenure, age, salary, and job satisfaction.
- Understand employee demographics and compensation patterns.
- Explore transparent, rule-based retention risk indicators.
- Provide an interactive report for workforce planning discussions.

## Tools and Technologies

| Tool / Technique | Use |
|---|---|
| Microsoft Power BI Desktop | Interactive reports and visualizations |
| Power Query (M) | Cleaning, transformations, and custom columns |
| DAX | KPIs, filter-aware measures, and ratios |
| Star schema | Fact and dimension tables with relationships |
| Power BI interactions | Slicers, page navigation, bookmarks, tooltips, drill-through |
| GitHub | Project files, screenshots, and documentation |

## Dataset Description

The HR dataset contains **1,470 employee records**, including fields such as `EmployeeNumber`, `Age`, `Gender`, `Department`, `JobRole`, `EducationField`, `MaritalStatus`, `MonthlyIncome`, `PercentSalaryHike`, `PerformanceRating`, `YearsAtCompany`, `JobSatisfaction`, `OverTime`, and `Attrition`.

**Power Query-derived columns** used in the analysis include:
`Age Group`, `Salary Band`, `Tenure Group`, `Distance Group`, `Attrition Flag`, `Overtime Flag`, and `Employee Risk Category`.

The repository includes the Power BI report. The underlying CSV is not redistributed here; dataset sharing should follow its original licensing and permissions.

## Dashboard Pages

### 1. HR Executive Overview

Summary of workforce and attrition:
- **1,470** total employees
- **1,233** active employees
- **237** attrition employees
- **16.12%** attrition rate
- **36.92 years** average age
- **7.01 years** average tenure

Includes departmental attrition rates, workforce status, overtime comparison, and department/gender/age-group filters.

![HR Executive Overview](Screenshots/1.%20HR%20Executive%20Overview.png)

### 2. Employee Attrition Analysis

Examines attrition across **departments, salary bands, tenure groups, age groups, and job satisfaction**. Includes a departmental summary matrix and overall retention metrics.

Selected findings visible in the dashboard:
- **34.88%** attrition among new joiners
- **28.61%** attrition in the low salary band
- **22.84%** attrition in the low job satisfaction category

These are descriptive comparisons, not causal estimates.

![Employee Attrition Analysis](Screenshots/2.%20Employee%20Attrition%20Analysis.png)

### 3. Employee Demographics

Explores workforce distribution by **age group, education field, department, gender, and marital status**.

Selected findings:
- **882 male** employees (**60%**)
- **588 female** employees (**40%**)
- **961** employees in Research & Development
- **446** employees in Sales
- **63** employees in Human Resources

![Employee Demographics](Screenshots/3.%20Employee%20Demographics.png)

### 4. Compensation & Performance

Analyzes salary, salary growth, and employee performance:
- **6,503** average monthly income (dataset units; currency not specified)
- **15.21%** average salary hike
- **2.06** average job level
- **3.15** average performance rating
- **9,559,309** sum of recorded monthly incomes across all employee records

> **Interpretation note:** The sum of monthly incomes shown in the report includes records for employees marked as having left; it should not be interpreted as the current active-workforce payroll without filtering to active employees.

![Compensation and Performance](Screenshots/4.%20Compensation%20and%20Performance%20Analysis.png)

### 5. Employee Retention Risk

Presents **exploratory, rule-based categories** for active employees:
- **16 high risk** (**1.30%** of active employees)
- **633 medium risk** (**51.34%**)
- **584 low risk** (**47.36%**)
- **649 employees requiring review** (**52.64%**, high + medium)

Includes risk distribution by overtime, department, tenure, and job role, plus a review table.

> **Important:** These risk labels are heuristic classifications, **not a validated predictive model**. They should not be used as the sole basis for individual employment decisions.

![Employee Retention Risk](Screenshots/5.%20Employee%20Retension%20Risk.png)

## Data Modeling and DAX

The report uses a star-schema-style model with the central **`Fact_Employee`** table and supporting dimensions:

- `Dim_Department`
- `Dim_JobRole`
- `Dim_Education`
- `Dim_Demographics`
- `Dim_Overtime`

Core DAX measures:

```dax
Total Employees =
DISTINCTCOUNT(Fact_Employee[EmployeeNumber])

Attrition Employees =
CALCULATE(
    [Total Employees],
    Fact_Employee[Attrition] = "Yes"
)

Active Employees =
CALCULATE(
    [Total Employees],
    Fact_Employee[Attrition] = "No"
)

Attrition Rate =
DIVIDE([Attrition Employees], [Total Employees], 0)

Retention Rate =
DIVIDE([Active Employees], [Total Employees], 0)

Average Monthly Income =
AVERAGE(Fact_Employee[MonthlyIncome])
```

Percent measures should be formatted as percentages in Power BI.

## Key Business Insights

| Metric | Result |
|---|---:|
| Total employees | 1,470 |
| Active employees | 1,233 |
| Employees who left | 237 |
| Overall attrition rate | 16.12% |
| Retention rate | 83.88% |
| Sales attrition rate | 20.63% |
| Human Resources attrition rate | 19.05% |
| Research & Development attrition rate | 13.84% |
| Overtime group attrition rate | 30.53% |
| Non-overtime group attrition rate | 10.44% |

**Interpretation:** Sales has the highest departmental attrition rate in this dataset. Employees reporting overtime have a higher observed attrition rate than employees without overtime. These patterns warrant further investigation; they do **not** establish cause and effect.

**Potential HR actions:** Investigate workload distribution, examine early-tenure experiences, review career development opportunities, and track departmental trends over time.

## Report Features

- Interactive department, gender, and age-group filters
- KPI cards, bar/column charts, donut charts, and matrices
- Page navigation across five dashboards
- Bookmarks and reset-filter interactions
- Supporting drill-through and report-page tooltip experiences

## Repository Structure

```text
HR-Analytics-PowerBI-Dashboard-and-Screenshots/
├── README.md
├── HR Analytics & Employee Attrition Dashboard-Final.pbix
├── Screenshots/
│   ├── 1. HR Executive Overview.png
│   ├── 2. Employee Attrition Analysis.png
│   ├── 3. Employee Demographics.png
│   ├── 4. Compensation and Performance Analysis.png
│   └── 5. Employee Retension Risk.png
└── .gitignore
```

## How to Open the PBIX File

1. Install **Microsoft Power BI Desktop**.
2. Download `HR Analytics & Employee Attrition Dashboard-Final.pbix` from this repository.
3. Open the `.pbix` file in Power BI Desktop.
4. Explore the five report pages and use the slicers, navigation, and other interactions.
5. If Power BI requests a data source refresh, configure the source path to a legitimately obtained copy of the original dataset.

## Author

**Saurabh Puri**


**Skills demonstrated:** Power BI, Power Query, DAX, data modeling, HR analytics, KPI design, and data storytelling.

