---
sidebar_position: 2
---

# Introduction

### Purpose

- The purpose of this project is that:
  - Digitalization of recruitment process
  - Integration with LINE for wider commercial exposure
  - Authentication with LIFF app through LINE lowers the bar of entry - no need for email/password registration
  - Persons in charge of recruitment can save time to schedule interview with applicants.
  - Applicants can do a series of tasks related to their recruitment acitivities on LINE: such as interview reservation and submission of resume and Identification.
  - Interview reservations are notified by LINE message
  - Multiple stores can be centralled managed via a single web system.
  - PDF generation of resume.

## Scope

```mermaid
sequenceDiagram
    actor Applicant
    actor Recruiter
    Recruiter->>Applicant: Recruitment information

    rect rgb(119, 136, 153)
    Applicant->>Recruiter: Application<br/>Interview reservation
    Recruiter->>Applicant: Update status<br/>Send message
    Applicant->>Recruiter: Submit<br/>resume & Identification
    Recruiter->>Applicant: Search applicants' information
    opt If there're any defects
    Recruiter-->>Applicant: Ask for revision<br/>Send message
    Applicant-->>Recruiter: Make a revision
    end
    end

    Note over Applicant,Recruiter: Interview

    rect rgb(119, 136, 153)
    Recruiter->>Applicant: Update status<br/>Send message
    Applicant->>Recruiter: Submit bank account information
    opt If there're any defects
    Recruiter-->>Applicant: Ask for revision<br/>Send message
    Applicant-->>Recruiter: Make a revision
    end
    end
