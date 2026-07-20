# Intelligent Recruitment Pipeline

An AI-powered, serverless recruitment pipeline built on AWS that automates resume parsing, candidate-job matching, scoring, and ranking using Natural Language Processing (NLP).

The system is designed to reduce manual CV screening by extracting structured information from resumes and comparing candidate profiles against job requirements using an explainable weighted scoring model.

## Overview

Recruiters can upload job descriptions and candidate resumes to the system. The recruitment pipeline processes these documents using AWS AI services, extracts relevant candidate information, calculates candidate-job compatibility scores, and presents ranked candidates through a recruiter dashboard.

The project uses Amazon Textract for document text extraction and Amazon Comprehend for NLP-based entity analysis.

## Architecture

The target architecture uses:

* **Amazon S3** — Resume and job description storage
* **AWS Lambda** — Serverless document processing and scoring
* **Amazon Textract** — Text extraction from uploaded documents
* **Amazon Comprehend** — NLP-based entity extraction
* **Amazon DynamoDB** — Candidate, job, and processing data storage
* **Amazon SQS** — Asynchronous candidate scoring
* **Amazon API Gateway** — REST API layer
* **Amazon Cognito** — Recruiter authentication and authorization
* **Amazon SES** — Candidate interview notifications
* **React + Vite** — Recruiter dashboard

### Processing Flow

```text
Recruiter
    │
    ▼
React Dashboard
    │
    ├── Upload Job Description
    └── Upload Resume
             │
             ▼
        Amazon S3
             │
             ▼
        AWS Lambda
             │
       ┌─────┴─────┐
       ▼           ▼
   Textract    Comprehend
       │           │
       └─────┬─────┘
             ▼
        DynamoDB
             │
             ▼
      Matching Engine
             │
             ▼
       Candidate Score
             │
             ▼
    Recruiter Dashboard
```

## Candidate Matching

Candidate-job compatibility is calculated using an explainable weighted scoring model:

| Matching Factor     | Weight |
| ------------------- | -----: |
| Skills Match        |    50% |
| Job Title Alignment |    30% |
| Experience Match    |    20% |

The final score is calculated as:

```text
Final Score =
    (Skills Match × 0.50)
  + (Title Alignment × 0.30)
  + (Experience Match × 0.20)
```

The score breakdown allows recruiters to understand why a candidate received a particular ranking rather than relying on an opaque ranking system.

## MVP Scope

The initial MVP focuses on demonstrating the core recruitment workflow:

* Upload job descriptions and resumes
* Store documents in Amazon S3
* Extract resume text using Amazon Textract
* Analyze document content using Amazon Comprehend
* Extract structured candidate information
* Store candidate records in DynamoDB
* Calculate candidate-job matching scores
* Rank candidates based on compatibility
* Display candidates through a recruiter dashboard

## Planned Enhancements

The architecture is designed to support additional capabilities, including:

* Amazon Comprehend Custom Entity Recognition for domain-specific skills
* Amazon SQS-based asynchronous processing
* Dead-Letter Queue (DLQ) handling for failed processing jobs
* Amazon Cognito authentication and role-based access
* Amazon SES interview invitation emails
* CSV shortlist export
* Advanced semantic similarity scoring
* Resume processing audit trails
* Multi-job candidate matching
* Recruiter-controlled scoring weights

## Project Structure

```text
f13-intelligent-recruitment/
├── backend/
│   └── processing-lambda/
│       └── lambda_function.py
│
├── frontend/
│
├── sample-data/
│   ├── resumes/
│   └── job-descriptions/
│
├── docs/
│   ├── architecture/
│   └── screenshots/
│
├── .gitignore
├── LICENSE
└── README.md
```

## Development Status

🚧 **Under Active Development**

The project is currently being developed as a functional MVP. Additional reliability, security, and NLP capabilities will be introduced incrementally.

## License

This project is intended for educational and demonstration purposes.