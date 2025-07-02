---
sidebar_position: 2
---

# Functional Design

## Use Case Diagram

```mermaid
flowchart LR

A{Applicant}
B{Recruiter}
MI{Miraic}

MI --creates-->ST[stores]
ST--each store has-->SRC[Recruitment system]

A -- apply --> C[Application]
B -. set up the flow<br>get notification<br>search<br>delete .-> C
A -- make<br>get reminder --> D[Reservation]
B -. set up slots<br>browse<br>send reminder<br>ask for reschedule<br>cancel .-> D
A -- upload<br>revise --> E[Resume<br>Identification<br>Bank account]
B -. ask for resubmission .-> E
A -- send message --> F[Chat]
B -. send message<br>make template<br>set up image as message<br>set up account profile .-> F
B -..-> G[Audience]
B -. assign recruiter to store<br>edit<br>browse<br>delete.-> H[Manager management]

subgraph Recruitment system
  C
  D
  E
  F
  G
  H
end
```

### [Click here](https://miraic1201.backlog.com/document/DI_SYSTEM_TEAM_SPACE/01979b9105cd74c1908a8091bed0ee1b) to know how to add a store

## Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Marketing
    actor Recruiter
    actor Applicant
    participant Recruitment system

    Recruiter->>Marketing: Expose LINE OA
    Marketing->>Applicant: Introduce LINE OA
    Applicant->>Recruitment system: Apply for job<br>Reserve interview
    Recruiter->>Recruitment system: Update interview status
    Recruitment system->>Applicant: Send notification<br>Proceed to next step
    Applicant->>Recruitment system: Submit resume & identification
    Recruiter->>Recruitment system: Search and browse applicants' information
    opt If there're any defects
    Recruitment system->>Applicant: Ask for revision
    Applicant->>Recruitment system: Revise
    end
    Recruiter<<->>Applicant: Interview
    Recruiter->>Recruitment system: Update recruitment status
    Recruitment system->>Applicant: Send notification<br>Proceed to next step
    alt Adopted
        Applicant->>Recruitment system: Send bank account information
        Recruiter->>Recruitment system: Search and browse applicants' information
        opt If there're any defects
        Recruitment system->>Applicant: Ask for revision
        Applicant->>Recruitment system: Revise
        end
    end
```

##　Screen Design

### List of Screens

#### Current screen design; https://www.figma.com/design/SeWAdyYpt4HuiHaliaVqy6/RecruitmentSystem?node-id=0-1&p=f&t=YeKk98j8cqk6rrh4-0

## Sample Table

| Name of Screen  | Description                      | Date of of latest update    |
|-----------------|----------------------------------|-----------|
| Mermaid Support | Render diagrams inside MDX files | Working   |
| Tables          | Standard Markdown tables support | Works fine|
| Blog            | Blogging with reading time       | Enabled   |
