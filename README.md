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

1. Overall Performance
2. Time Performance
3. Job Posting Performance
4. Interviewer Performance
5. Recruitment Process Funnel
6. Job Vacancy Closing Performance

<img width="1058" height="775" alt="image" src="https://github.com/user-attachments/assets/ad19e75d-627a-46f2-b696-f41d8b9e69aa" />

## Key Findings
1. Recruitment bottleneck
Target/SLA performance
Department/employee-level differences
Source effectiveness
Interviewer performance
Vacancy closing performance

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




