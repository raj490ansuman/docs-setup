---
sidebar_position: 2
---

# Apply Resume

The applyResume Logic validates the store ID and resume data, fetches the application with resume and identity info, and ensures the resume is still editable. It then processes the resume picture (uploading or reusing), fills in resume details, updates the status, creates identity info if missing, sets work position descriptions from templates, and lastly updates the LINE rich menu based on the status of the resume.

```mermaid
flowchart TD
    Start(["Start"]) -- validate store --> FetchApp["Fetch Application with<br>resume &amp; applicant identity info"]
    FetchApp --> ValidApp{"Is it a valid and new resume?"}
    ValidApp -- No --> Error1["Error"]
    ValidApp -- Yes --> FillResume["Fill Resume &<br/> update the status"]
    FillResume --> IdentityCheck{"Does the applicant<br/> Identity info exists?"}
    IdentityCheck -- No --> CreateIdentity["Create new Identity<br>record"]
    IdentityCheck -- Yes --> SkipIdentity["Skip identity<br>creation"]
    CreateIdentity --> SetWorkPos["Set Work Position Description<br>from Templates"]
    SkipIdentity --> SetWorkPos
    SetWorkPos --> UpdateMenu["Update Richmenu"]
    UpdateMenu --> End(["End"])
    Error1 --> End

    FillResume@{ shape: rect}
     Start:::startend
     FetchApp:::process
     ValidApp:::decision
     Error1:::error
     FillResume:::process
     IdentityCheck:::decision
     CreateIdentity:::process
     SkipIdentity:::process
     SetWorkPos:::process
     UpdateMenu:::process
     End:::startend
    classDef startend fill:#76c7c0,stroke:#333,stroke-width:2px,color:#fff,font-weight:bold
    classDef process fill:#6fa8dc,stroke:#333,stroke-width:1.5px,color:#222,font-weight:bold
    classDef decision fill:#ffb347,stroke:#333,stroke-width:2px,color:#333,font-weight:bold
    classDef error fill:#f44336,stroke:#900,stroke-width:2px,color:#fff,font-weight:bold
    classDef success fill:#4caf50,stroke:#256a2e,stroke-width:2px,color:#fff,font-weight:bold



```
