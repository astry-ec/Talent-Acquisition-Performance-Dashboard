# Talent-Acquisition-Performance-Dashboard
Talent Acquisition Performance Dashboard

Talent Acquisition Performance Dashboard Analysis has a comprehensive outlook about end-to-end Recruitment Process. This dashboard has 6 pages which serves and answers different point of view of business questions. 

Below is the table of content for this Data Analytics Reporting
[- Dataset Overview](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#dataset-overview)
[- Problem Statement](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#problem-statement)
[- Business Questions](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#business-questions)
[- Dataset Overview](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#data-modelling-approach)
[- Dashboard Analysis](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#dashboard-analysis)
[- Recommendations](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#key-findings)
[- Recommendations](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#recommendations)
[- Limitations](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#limitations)
[- Conclusion](https://github.com/astry-ec/Talent-Acquisition-Performance-Dashboard/blob/main/README.md#conclusion)

## Dataset Overview
Dataset used by this project is manually created with dummy information, the data and output of the analysis is not related or depicted any company/institution's performance.

## Problem Statement
The process time of finding new employee is varied, some of job vacations are able to get new hire within targeted time but some are exceeded the target.

## Business Questions
1. How long does it take each stages of recruitment process in average?
2. How long does it take to hire someone from the moment a job vacancy opens?
3. What is the most resourceful job posting place?
4. Which stage acts as a bottleneck in the recruitment process?
5. How did the interviewers perform during the recruitment process?

## Data Modelling Approach
The dataset originates from an Excel file containing 6 distinct sheets. Each sheet holds specific data, detailed as follows:
1. Candidates Sheet: comprehensive personal data of candidates
2. Jobs Sheet: comprehensive job vacancy data (covering both open and closed positions)
3. Applications Sheet: candidate application data and current recruitment process status
4. StatusHistory Sheet: status history for each candidate's application
5. Source Sheet: source ID and name data
6. Interview Sheet: interviewer ID and name data

## Relationship Diagram
<img width="1170" height="821" alt="image" src="https://github.com/user-attachments/assets/fec2ca95-b43a-4f29-8e75-4735f2e67755" />

## Key Metrics & DAX
1. Total Candidates, Total Application, Total Hired
   ```text
   Total Candidates = DISTINCTCOUNT(Candidate[CandidateID])
   Total Application = DISTINCTCOUNT('Application'[ApplicationID])
   Total Hired = 
      CALCULATE (
          DISTINCTCOUNT ( 'Application'[ApplicationID] ),
          'Application'[FinalOutcome] = "Hired"
      )
   ```
2. Average Time to Hire
   
   Calculated time to hire days
   ```text
   Time to Hire Days = 
      VAR AppliedDate = 'Application'[Applied Date]
      VAR HiredDate = 'Application'[Hired Date]
      RETURN
         IF (
              NOT ISBLANK ( AppliedDate )
                  && NOT ISBLANK ( HiredDate ),
              DATEDIFF ( AppliedDate, HiredDate, DAY ),
              BLANK ()
    )
   ```
   
   Calculated average time to hire
   ```text
   Avg Time to Hire = 
      AVERAGEX (
          FILTER (
              'Application',
              NOT ISBLANK ( 'Application'[Time to Hire Days] )
          ),
          'Application'[Time to Hire Days]
      )
   ```
   
3. Average Days in Stage Process

   Calculated days in stage
   ```text
   Total Hired = 
      CALCULATE (
          DISTINCTCOUNT ( 'Application'[ApplicationID] ),
          'Application'[FinalOutcome] = "Hired"
      )
   ```

   Calculated average days in stage
   ```text
   Avg Days in Stage = 
      AVERAGE ( 'StatusHistory'[Days in Stage] )
   ```
   
7. Average Interview Days
   ```text
   Avg Interview Days = 
      CALCULATE (
          AVERAGE ( 'StatusHistory'[Days in Stage] ),
          'StatusHistory'[Status] IN {
              "Interview 1",
              "Interview 2",
              "Interview 3"
          }
      )
   ```
## Dashboard Analysis

The dashboard was developed using Power BI. However, since I don't have access to Power BI Service for public sharing, I have attached a PDF containing all pages of the Talent Acquisition Performance Dashboard.

[TA Performance Dashboard v2.pdf](https://github.com/user-attachments/files/30965922/TA.Performance.Dashboard.v2.pdf)

1. Overall Performance
A brief summary of Talent Acquisition's KPI.

2. Time Performance
an in-depth analysis of the time spent at each stage of the recruitment process across dimensions such as Employee Level and Department.

3. Job Posting Performance
an analysis of recruitment sources that attract more candidates and result in more hires.

4. Interviewer Performance
an analysis of interviewer performance based on interview volume and average interview duration compared against predefined target.

5. Recruitment Process Funnel
an analysis of candidate progression across recruitment stages to identify potential bottlenecks and significant candidate drop-offs.

6. Job Vacancy Closing Performance
an analysis of job vacancy opening and closing trends over time to monitor recruitment demand and vacancy closure performance.

## Key Findings
The data source contains four months data of candidates. April, May, June and July. This report is created in the middle of August.

### Recruitment Overview
1. The IT sector recorded the highest number of applicants, despite there being only six job openings during that four-month period. The next position was held by applicants with a background in Finance, with seven job openings available.
2. The result indicates that hire rate is 4.55%. It shows that the recruitment process may indicate that the recruitment process is highly selective, with a large candidate pool.
3. The number of applicants rose significantly in June. This increase coincided with a rise in the number of new job vacancies opened during the same month.
4. As of August 12, 2026, Screening contains the largest number of active applicants. This stage may require closer monitoring to determine whether candidates are progressing as expected or experiencing delays. - Go to recomendations

### Time Performance Dashboard
1. Employee Level GG03 is the only employee level that has an average time to hire below the predefined target. On other hand, Employee Level GG08 has the longest average time to hire.
2. Average time to hire for all departments exceeded the predefined target. - Go to recommendations
3. Interview 1 has the highest average Days in Stage among all recruitment process stages. A similar pattern is observed across departments, with Interview 1 showing relatively high processing times in each department. This is particularly notable in the Legal department, where Interview 1 reaches 15 days, substantially exceeding the 7-day target.
4. The Legal department shows the most significant delays during the interview process stages. A similar pattern is observed across departments, with Interview 1 consistently showing relatively high processing times.
5. In contrast, the IT department demonstrates relatively stable processing times across recruitment stages, with most stages remaining close to their respective targets.

### Job Posting Performance
1. LinkedIn generated the highest number of applications, with 60 out 88 total applicants, making it the largest source candidates.
2. Despite generating the highest application volume, LinkedIn recorded a relatively low overall hire rate of 33.3%, with only two candidates hired
3. Referral recorded a 100% hire rate, but this result is based on only on application. Therefore, the high conversion rate should be interpreted cautiously due to the very small sample size.
4. Sources effectiveness varies across departments.
   a. LinkedIn generated 37 applications for IT but resulted in only one hire (2.70%).
   b. JobStreet generated 11 IT applications and also resulted in one hire (9.09%).

### Interviewer Performance
1. Sanji handled the highest interview volume, conducting six Interview 1 sessions, followed by Chooper with four Interview 1 sessions.
2. Sanji and Rina recorded the longest average interview duration at 12.8 and 12.3 days, respectively, substantially exceeding the 7-day target for their respective interview stages.
3. Most other interviewers remained close to or below their predefined targets. However, Chooper slightly exceeded the 7-day target, with an average interview duration of 7.8 days.
4. Among hiring managers with successful hires, Justin Andersen recorded the longest average Time to Hire at 47 days, while Levi Ackermann recorded the shortest at 29 days, slightly below the 30-day target.

### Recruitment Process Funnel
1. The recruitment funnel narrowed from 88 applications to four hires, resulting in an overall hire rate of 4.55%.
2. The largest drop occurred between Screening and Interview 1, where the number of candidates decreased from 56 to 14, representing a 75% reduction.
3. Candidate volume continued to decline throughout the interview stages, from 14 candidates at Interview 1 to nine at Interview 2 and six at Interview 3.
4. All four candidates who reached the Offer stage were eventually hired, resulting in a 100% conversion rate from Offer to Hire in this dataset.

### Job Closing Performance
1. A total of 20 job vacancies were opened during the observed period, while only three were closed, leaving 17 positions currently open.
2. Recruitment demand peaked in June, when 17 new job vacancies were opened, accounting for 85% of all vacancies opened during the period.
3. All three job closures occurred in July, while only one new vacancy was opened during the same month.
4. The overall job closing rate was 15%, indicating that the majority of vacancies opened during the observed period remained open at the time of analysis.

## Recommendations
1. Review the transition from Screening to Interview 1, as this stage shows the largest candidate drop in the recruitment funnel. Further analysis should determine whether the decline is caused by candidate quality, screening criteria, candidate withdrawal, or other factors.
2. Review the Interview 1 and Interview 2 processes, particularly for departments with processing times above the predefined targets. The Legal department should receive particular attention due to its substantially longer interview duration.
3. Evaluate recruitment sources based on both application volume and hiring outcomes rather than application volume alone. LinkedIn generates the largest candidate pool but has a relatively low hire rate, while smaller sources should be evaluated with caution due to limited sample sizes.
4. Monitor interviewer workload and processing time together. Interviewers with high interview volumes or above-target processing times may require workload redistribution or further investigation to identify the causes of delays.
5. Monitor the 17 currently open vacancies, particularly those that remain open beyond the expected hiring timeline, to identify positions that may require additional sourcing or process improvements.

## Limitations
1. The dataset used in this project is manually created dummy data and does not represent the recruitment performance of any actual company or organization.
2. The dataset contains only 88 applications, 75 candidates, and 20 job vacancies across a four-month period. Therefore, the findings should not be generalized to a larger recruitment population.
3. Some categories contain very small sample sizes. For example, the 100% Referral hire rate is based on only one application and should not be interpreted as evidence that Referral is the most effective recruitment source.
4. The dashboard primarily measures recruitment volume, conversion, and processing time. It does not include other factors such as candidate quality, withdrawal reasons, recruitment costs, interviewer availability, or candidate experience that could explain the observed results.

## Conclusion
The analysis highlights several areas of the recruitment process that may require further attention. Although 88 applications were received, only four candidates were hired, resulting in a 4.55% hire rate. The largest candidate drop occurred between Screening and Interview 1, while the interview stages also showed some processing times above their predefined targets. In addition, recruitment sources with high application volumes did not necessarily produce higher hire rates. These findings demonstrate the importance of evaluating recruitment performance through multiple dimensions, including candidate conversion, processing time, sourcing effectiveness, and job vacancy closure.



