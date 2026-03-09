# Why Are Our Best People Leaving?
### HR Analytics — Employee Attrition Analysis
**Tool:** Microsoft Excel &nbsp;|&nbsp; **By:** Temidayo Olubayo

## Business Context

Employee attrition is one of the most expensive problems organizations face. 
Losing skilled employees increases recruitment costs, slows productivity, and disrupts team stability.

Understanding **who is leaving and why** allows companies to design better compensation strategies, retention programs, and career development pathways.

This analysis investigates employee attrition patterns using HR data to identify the factors most strongly associated with voluntary employee exits.

> *The analysis revealed a surprising pattern: the company was not losing low performers- many of the employees leaving were high-performing early-career staff.*

## Table of Contents
1. [Project Overview](#project-overview)
2. [Problem Statement](#problem-statement)
3. [Key Questions](#key-questions)
4. [Dataset Overview](#dataset-overview)
5. [Data Cleaning Process](#data-cleaning-process)
6. [Key Findings](#key-findings)
7. [Dashboard & Visuals](#dashboard--visuals)
8. [Recommendations](#recommendations)
9.  [Business Impact](#business-impact)
10. [Tools Used](#tools-used)

## Project Overview

This project analyzes an HR dataset to understand patterns behind employee attrition and identify factors associated with voluntary employee exits.

Using Microsoft Excel, the dataset was cleaned, validated, and analyzed across 1,470 employee records. The analysis explores relationships between age, tenure, salary growth, stock options, job satisfaction, and employee departures.

The findings reveal a clear pattern behind why high-performing early-career employees are leaving the company.

## Problem Statement

The company wants to understand why employees are leaving and identify patterns associated with voluntary attrition.

## Key Questions

• Which employees are most likely to leave?  
• What role does salary growth play in retention?  
• Do stock options influence employee decisions to stay?  
• Are high-performing employees leaving the company?
   
## Dataset Overview

| Field | Detail |
|---|---|
| Source | TDI Data Analysis Community |
| Total Records | 1,470 employees |
| Clean Records | 1,449 |
| Flagged / Under Review | 21 records |
| Employees Who Left | 237 total (217 used in deep analysis) |
| Time Period | 2010-Present |

**Key Columns:**

`ID_employe` `Age` `Attrition` `Department` `Job Role` `Gender` `MaritalStatus` `EmploymentType` `TerminationType` `Salary` `PercentSalaryHike` `StockOption` `JobSatisfaction` `PerformanceRating` `WorkLifeBalance` `OverTime` `TotalWorkingYears` `YearsSinceLastPromotion` `DateBirth` `DateStart` `DateDeparture` `Tenure`

## Data Cleaning Process

The dataset went through a cleaning process before analysis was done. The following checks were performed before analysis:

**Duplicates & Missing Values:**
No duplicates were found, no missing or null values across any column.

**Standardisation:**
Categorical fields (Gender, MaritalStatus, EmploymentType, TerminationType, BusinessTravel) were checked for casing inconsistencies, typos, and mixed formats, then standardized.

**Rating & Scale Validation:**
Columns with fixed scales were validated against their expected ranges:
- JobSatisfaction - range 1 to 5
- PerformanceRating - range 1 to 4

**Updated Column Names:**

`employee_id` `age` `attrition` `business_travel` `department` `education` `environment_satisfaction` `gender` `job_involvement` `job_role` `job_satisfaction_score` `job_satisfaction` `performance_rating_score` `performance_rating` `work_life_balance` `marital_status` `stock_option_level` `overtime` `percent_salary_hike` `num_companies_worked` `total_working_years` `years_since_last_promotion` `years_with_current_manager` `distance_from_home` `hourly_rate` `daily_rate` `monthly_rate` `salary` `training_times_last_year` `birth_date` `start_date` `departure_date` `termination_type` `employment_type`

**Extra Columns added for Analysis:**

`age_work_check` `start_vs_birth_date` `data_quality_flag` `age_bucket` `distance_from_home_bucket` `tenure` `tenure_bucket` `percentage_hike_bucket` `year_of_attrition`

**Logical Checks & Flags:**
Four logical checks were performed and flagged where errors were found:

| Flag Column | Check Performed |
|---|---|
| `age_work_check` | Age vs Total Working Years consistency |
| `start_vs_birth_date` | Start Date must be after Date of Birth |
| `years_with_manager_check` | Years with Manager cannot exceed Total Working Years |
| `promotion_check` | Years Since Last Promotion cannot exceed Total Working Years |

Records failing these checks were flagged **"Needs Review"** and excluded from analyses involving those fields while remaining in overall headcount calculations.

**Tenure:**

Tenure was not available in the raw dataset and was calculated using:

```excel
=IF([@[departure_date]]="", TODAY()-[@[start_date]],[@[departure_date]]-[@[start_date]])/365
```
Active employees calculate their start dates to today's date, while departed employees calculate to their departure date.

**Age Outlier Check:**
Ages below 18 or above 70 were flagged for review as they fall outside the expected range for an active workforce.

**Sample of dataset**
<img width="1899" height="930" alt="image" src="https://github.com/user-attachments/assets/af4354cc-0920-448e-882e-157b0d26d8b3" />

## Key Findings

### 1. The attrition rate is 16.2%:
Based on 1,449 clean records, 237 employees left. 217 of those were used for deeper analysis after excluding flagged records.

### 2. The company is losing its best people and not its worst:
Most exits occurred through resignation or retirement. Very few employees were dismissed, indicating that attrition is primarily driven by employees choosing to leave and not by employment terminations.

The most affected age group is **25 to 34 years**. This group represents high-performing early-career employees leaving the company voluntarily.

### 3. Job satisfaction is not the main driver:
The average job satisfaction scored 3.0 out of 5. Approximately 28.11% rated it low and 19.35% rated medium scores. But many employees who left had decent satisfaction scores. This pointed to something more important:

**Push factors vs Pull factors:**

- Push factors = "something is wrong here, I need to leave"
- Pull factors = "something better is out there and I am going to take it"

The data showed a Pull Factor story. Employees were not leaving because they weren't satisfied, they were leaving for better opportunity.

### Why this conclusion?:

### a. Salary growth is too low to retain early-career talent
- *Over 55% of employees who left had received a salary hike of less than 15%.*

- *88 out of 217 attrition records fell into the under-15% salary hike bracket **and** had a tenure of under 5 years.*

<img width="897" height="276" alt="image" src="https://github.com/user-attachments/assets/e454a41d-d931-45dc-ab7a-95093cdd54e5" />

- *25 to 34 age group showed this pattern which moves to conclude that young, ambitious employees with stagnant salary growth are the highest flight risk.*

<img width="665" height="266" alt="image" src="https://github.com/user-attachments/assets/3b59f7e4-a66f-45d9-a080-1fd3095e6951" />

### b. Stock options are the missing anchor:
- *Majority of employees had **zero to minimal stock options (Level 0 or 1)**. This was accross the full attrition group and remained consistent when filtered to only the under-15% salary hike segment.*

- *Stock options act as a retention incentive by creating a financial benefit tied to long-term employment.*

<img width="773" height="348" alt="image" src="https://github.com/user-attachments/assets/cdb8fc06-646c-40ec-863a-e41881387728" />

**The combination of low salary hikes and no stock options gave early-career, high-performing employees no financial reason to say no to a better offer.**

### 4. The 55+ group is not a concern
Employees above 55 exited mostly with retirement and few dismissed. This is expected and does not represent a retention problem.

## Dashboard & Visuals

**KPI Cards**
- Total Employees
- Total Active employees
- Attrition Rate
- Departures
- Average Job Satisfaction
- Average Performance Rating

**Charts**
- What age group leaves the most? *(Attrition by Age Group)*
- Are salary raises keeping people? *(Attrition by Salary Hike Bracket)*
- What stock options make people leave? *(Attrition by Stock Option Level)*
- How long do people stay in the company? *(Attrition by Tenure Group)*
- How do people leave? *(Attrition by Termination Type)*
- What gender leaves the most? *(Attrition by Gender)*

**Slicers**
- Tenure
- Attrition (Yes / No)
- Department

<img width="1560" height="865" alt="Screenshot 2026-03-07 161742" src="https://github.com/user-attachments/assets/12e88c55-58a5-4217-8124-2f3b44d65e44" />

## Recommendations

**1. Fix salary progression for early-tenure employees:**

The under-5-year, under-15%-hike segment accounts for the most amount of attrition. Structured, and better salary growth plan for the first five years of employment would directly address this.

**2. Introduce meaningful stock options for high performers:**

Allocate stock options to high-performing employees aged 25–34 to create stronger financial incentives for retention.

**3. Build visible career pathways:**

Ambitious employees leave when they can't see where they are going. Clear promotion criteria and career progression structures can reduce the appeal of external offers.

**4. Shift from satisfaction surveys to retention strategy:**

The data showed that satisfaction alone does not predict whether someone stays. The company needs to monitor compensation competitiveness against the external market, not just internal sentiment scores.

**5. Watch the 35 to 55 group:**

This group the next potential to leave for the same reasons as the 25 to 34 years group (no to low stock options, low salary hike). The low job satisfaction within this bracket is also worth monitoring before it becomes the next attrition wave

## Business Impact

The findings highlight a clear retention gap among early-career high-performing employees.

If unaddressed, this pattern can result in:
- increased recruitment and training costs
- loss of experienced mid-level talent pipelines
- reduced organizational stability

Addressing compensation growth and long-term incentives could significantly reduce attrition among the most valuable employee segments.

## Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data cleaning, feature engineering, pivot analysis, dashboard |
| Excel Formulas | Logical checks, tenure calculation, flagging, bucketing |
| Pivot Tables | Aggregations and cross-tabulations for all charts |
| Slicers | Interactive dashboard filtering |

---
**Temidayo Olubayo** &nbsp;|&nbsp; Data Analytics &nbsp;
