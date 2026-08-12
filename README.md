# Talent-Acquisition-Performance-Dashboard
Talent Acquisition Performance Dashboard

Talent Acquisition Performance Dashboard Analysis has a comprehensive outlook about end-to-end Recruitment Process. This dashboard has 6 pages which serves and answers different point of view of business questions. 

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

<img width="1058" height="775" alt="image" src="https://github.com/user-attachments/assets/ad19e75d-627a-46f2-b696-f41d8b9e69aa" />

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
3. Interview 1 has the longest average days

## Recommendations
Berdasarkan findings, bukan recommendation generik.
Prioritize berdasarkan impact.

## Limitations
Dummy/manual dataset
Small sample
Assumed targets
Tidak merepresentasikan perusahaan nyata
Beberapa metric sensitif terhadap sample size — referral 100% kamu itu contoh bagus 😂

## Conclusion




