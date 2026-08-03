
Resumint API Documentation

Version: 1.0.0

Document Status: Production Ready

Audience: Developers, Integration Partners, Enterprise Customers

API Type: REST API

Protocol: HTTPS

Data Format: JSON

Authentication: OAuth 2.0 / JWT


---

Table of Contents

1. Introduction


2. API Overview


3. Authentication


4. Request Headers


5. Rate Limits


6. Error Handling


7. Users API


8. Resume API


9. AI Resume Analysis API


10. AI Resume Generation API


11. Job Matching API


12. Recruiter API


13. Candidate Search API


14. AI Career Assistant API


15. Notifications API


16. Webhooks


17. Security


18. Versioning


19. SDKs


20. Changelog




---

1. Introduction

The Resumint API enables developers and enterprise partners to integrate AI-powered recruitment and résumé management capabilities into their own applications.

The API provides services for:

AI résumé analysis

Résumé scoring

AI résumé creation

Job recommendation

Recruiter discovery

Candidate discovery

Skills assessment

Career recommendations

AI interview preparation

Application tracking



---

2. API Overview

Base URL

https://api.resumint.com/v1

Content Type

application/json

All endpoints require authentication.


---

3. Authentication

Resumint uses OAuth 2.0 Bearer Tokens.

Example

Authorization: Bearer YOUR_ACCESS_TOKEN

Expired or invalid tokens return

{
    "status":"error",
    "code":401,
    "message":"Invalid access token."
}


---

4. User Roles

The API supports three user roles.

Recruit

A job seeker.

Capabilities

Upload résumé

Generate résumé

AI evaluation

Find recruiters

Apply for jobs

AI career coaching



---

Recruiter

Capabilities

Search candidates

Create vacancies

Review AI candidate rankings

Contact candidates

Manage hiring pipeline



---

Administrator

Capabilities

Platform management

User moderation

Analytics

Billing

AI monitoring



---

5. Resume API

Upload Resume

POST /resume/upload

Description

Uploads a résumé for AI processing.

Request

{
    "file":"resume.pdf"
}

Response

{
    "resumeId":"RSM-239103",
    "status":"Uploaded"
}


---

Retrieve Resume

GET /resume/{resumeId}

Returns the uploaded résumé.


---

Delete Resume

DELETE /resume/{resumeId}

Deletes the résumé.


---

6. AI Resume Evaluation API

Evaluate Resume

POST /ai/evaluate

Description

Analyses the uploaded résumé using the Resumint AI Engine.

The AI evaluates

Formatting

Grammar

ATS compatibility

Skills

Professional experience

Education

Keyword optimisation

Leadership qualities

Industry relevance


Example Request

{
    "resumeId":"RSM-239103"
}

Example Response

{
    "overallScore":92,
    "ATSScore":95,
    "grammar":98,
    "keywordScore":91,
    "design":84,
    "recommendations":[
        "Add measurable achievements.",
        "Include leadership experience.",
        "Improve technical keywords."
    ]
}


---

7. AI Resume Generation API

POST /ai/generate

Description

Creates a professional résumé for first-time job seekers.

Input
{
  "type": "object",
  "required": ["name", "email"],
  "properties": {
    "name": {
      "type": "string",
      "minLength": 2,
      "maxLength": 100
    },
    "email": {
      "type": "string",
      "format": "email"
    },
    "yearsOfExperience": {
      "type": "integer",
      "minimum": 0
    }
  }
}
Response

{
    "resumeId":"RSM-20113",
    "template":"Modern Professional",
    "downloadUrl":"..."
}


---

8. Resume Templates API

Retrieve available templates.

GET /templates

Response

{
    "templates":[
        "Modern",
        "Executive",
        "Creative",
        "Minimal",
        "Graduate",
        "Corporate"
    ]
}


---

9. Job Matching API

One of Resumint's core services.

POST /jobs/match

Description

Uses AI to compare the recruit's résumé against thousands of vacancies.

Matching considers

Skills

Experience

Education

Personality

Certifications

Languages

Preferred location

Salary expectations


Response

{
    "matches":[
        {
            "jobTitle":"Backend Developer",
            "matchScore":96,
            "company":"TechCrush",
            "location":"Lagos"
        }
    ]
}


---

10. Recruiter API

Find Recruiters

GET /recruiters/search

Filters

Industry

Country

Company

Hiring Status

Skills Needed


Response

{
    "results":[
        {
            "company":"TechNova",
            "recruiter":"Sarah Wilson",
            "industry":"Technology"
        }
    ]
}


---

11. Candidate Discovery API

Recruiters can search candidates.

GET /candidates/search

Search filters

Skills

Experience

Country

Degree

AI Score

ATS Score

Certifications

Availability



---

12. AI Career Assistant API

POST /ai/career-advisor

The assistant can

Improve résumés

Suggest careers

Prepare interview questions

Recommend certifications

Suggest learning paths

Improve LinkedIn profiles

Optimise cover letters


Example

{
    "question":"How can I improve my résumé?"
}


---

13. Notifications API

Supports

Email

SMS

Push Notifications


Triggers include

New recruiter interest

New job matches

Interview invitations

AI recommendations

Profile completion reminders



---

14. Webhooks

Enterprise partners may subscribe to events.

Supported Events

resume.created

resume.updated

job.match.found

candidate.applied

candidate.shortlisted

candidate.hired

interview.scheduled


---

15. Security

Resumint follows enterprise security standards.

Features include

HTTPS encryption

JWT authentication

OAuth 2.0

Rate limiting

Audit logging

Data encryption at rest

Role-based access control

Multi-factor authentication (optional)



---

16. Rate Limits

Plan	Requests per minute

Free	100
Professional	1,000
Enterprise	Unlimited*


*Subject to fair usage policies.


---

17. Error Codes

Code	Description

200	Success
201	Created
400	Bad Request
401	Unauthorised
403	Forbidden
404	Resource Not Found
409	Conflict
422	Validation Error
429	Too Many Requests
500	Internal Server Error



---

18. API Versioning

Current Version

v1

Future versions

v2

v3


---

19. Changelog

Version 1.0.0

Initial release including:

User authentication

AI résumé generation

AI résumé evaluation

ATS scoring

Recruiter search

Candidate search

Job matching

Career assistant

Notifications

Webhook support



---

Future Roadmap

The following features are planned for future API releases:

AI-powered mock interviews with real-time feedback.

Video résumé analysis and optimisation.

Automated cover letter generation tailored to specific job descriptions.

Integration with major job boards and applicant tracking systems (ATS).

Skills verification through assessments and digital badges.

Employer analytics dashboards for recruitment trends.

AI-based salary benchmarking and negotiation insights.

Multilingual résumé generation and analysis.

Real-time collaboration for career coaches and recruiters.

Public developer SDKs for JavaScript, Python, Java, and .NET.


