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
   '''text
3. Average Time to Hire
4. Average Days in Stage Process
5. Average Interview Days







