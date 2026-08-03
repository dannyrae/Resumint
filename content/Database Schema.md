Resumint Database Schema

1. Users

Stores all user accounts.

Column	Type	Constraints

user_id	UUID	Primary Key
first_name	VARCHAR(100)	NOT NULL
last_name	VARCHAR(100)	NOT NULL
email	VARCHAR(255)	UNIQUE
password_hash	TEXT	NOT NULL
phone_number	VARCHAR(20)	
account_type	ENUM('Candidate','Recruiter','Admin')	
profile_picture	TEXT	
country	VARCHAR(100)	
city	VARCHAR(100)	
created_at	TIMESTAMP	
updated_at	TIMESTAMP	



---

2. Candidate Profiles

Column	Type

candidate_id	UUID (PK)
user_id	UUID (FK Users)
headline	VARCHAR(255)
summary	TEXT
years_experience	INTEGER
desired_salary	DECIMAL
availability	ENUM
linkedin_url	TEXT
portfolio_url	TEXT
github_url	TEXT



---

3. Recruiter Profiles

Column	Type

recruiter_id	UUID
user_id	UUID
company_id	UUID
job_title	VARCHAR
department	VARCHAR



---

4. Companies

Column	Type

company_id	UUID
company_name	VARCHAR
logo	TEXT
website	TEXT
industry	VARCHAR
size	VARCHAR
description	TEXT
headquarters	VARCHAR



---

5. Skills

Column	Type

skill_id	UUID
skill_name	VARCHAR
category	VARCHAR


Examples

Java

Python

React

Project Management

UI Design



---

6. Candidate Skills

Many-to-many relationship.

Column	Type

id	UUID
candidate_id	UUID
skill_id	UUID
proficiency	ENUM(Beginner, Intermediate, Advanced, Expert)
years_used	INTEGER



---

7. Resumes

Stores uploaded or AI-generated resumes.

Column	Type

resume_id	UUID
candidate_id	UUID
resume_name	VARCHAR
file_url	TEXT
ai_generated	BOOLEAN
version	INTEGER
created_at	TIMESTAMP



---

8. Resume Scores

AI evaluation.

Column	Type

score_id	UUID
resume_id	UUID
overall_score	DECIMAL
formatting_score	DECIMAL
grammar_score	DECIMAL
keyword_score	DECIMAL
ats_score	DECIMAL
readability_score	DECIMAL
feedback	TEXT



---

9. Resume Sections

Column	Type

section_id	UUID
resume_id	UUID
section_type	ENUM
content	JSON


Section Types

Education

Experience

Skills

Certifications

Projects

Awards



---

10. Job Listings

Column	Type

job_id	UUID
recruiter_id	UUID
company_id	UUID
title	VARCHAR
description	TEXT
salary_min	DECIMAL
salary_max	DECIMAL
employment_type	ENUM
experience_required	INTEGER
location	VARCHAR
remote	BOOLEAN
status	ENUM(Open, Closed)
created_at	TIMESTAMP



---

11. Job Requirements

Column	Type

requirement_id	UUID
job_id	UUID
skill_id	UUID
required_level	ENUM
mandatory	BOOLEAN



---

12. Job Applications

Column	Type

application_id	UUID
candidate_id	UUID
job_id	UUID
resume_id	UUID
application_status	ENUM
ai_match_score	DECIMAL
submitted_at	TIMESTAMP


Status

Applied

Viewed

Shortlisted

Interview

Rejected

Hired



---

13. AI Job Recommendations

Column	Type

recommendation_id	UUID
candidate_id	UUID
job_id	UUID
match_score	DECIMAL
explanation	TEXT
generated_at	TIMESTAMP



---

14. Interviews

Column	Type

interview_id	UUID
application_id	UUID
interview_type	ENUM
interview_date	TIMESTAMP
meeting_link	TEXT
notes	TEXT



---

15. Messages

Column	Type

message_id	UUID
sender_id	UUID
receiver_id	UUID
message	TEXT
read_status	BOOLEAN
created_at	TIMESTAMP



---

16. Notifications

Column	Type

notification_id	UUID
user_id	UUID
title	VARCHAR
body	TEXT
type	VARCHAR
read_status	BOOLEAN
created_at	TIMESTAMP



---

17. AI Conversations

Tracks interactions with the résumé assistant.

Column	Type

conversation_id	UUID
user_id	UUID
prompt	TEXT
response	TEXT
created_at	TIMESTAMP



---

18. Saved Jobs

Column	Type

saved_job_id	UUID
candidate_id	UUID
job_id	UUID
saved_at	TIMESTAMP



---

19. Education

Column	Type

education_id	UUID
candidate_id	UUID
institution	VARCHAR
degree	VARCHAR
field_of_study	VARCHAR
start_date	DATE
end_date	DATE



---

20. Work Experience

Column	Type

experience_id	UUID
candidate_id	UUID
company	VARCHAR
position	VARCHAR
start_date	DATE
end_date	DATE
description	TEXT



---

Entity Relationship Summary

Users
 ├── Candidate Profile
 │     ├── Skills
 │     ├── Education
 │     ├── Experience
 │     ├── Resume
 │     │      ├── Resume Sections
 │     │      └── Resume Scores
 │     ├── Saved Jobs
 │     └── Applications
 │              ├── Interviews
 │              └── AI Match Score
 │
 └── Recruiter Profile
        └── Company
              └── Job Listings
                     └── Job Requirements

Users
 ├── Messages
 ├── Notifications
 └── AI Conversations

