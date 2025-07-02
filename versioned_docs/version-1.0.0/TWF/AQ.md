---
sidebar_position: 2
---

# Apply Question

The logic handles an applicant’s response to a store-specific question by first validating the request, identifying the current question in the flow, then saving the answer based on its type (e.g., image, appointment, confirmation), updating the application’s status or resetting it if rejected, and finally sending notifications to the applicant and/or admins as needed.


```mermaid
flowchart TD
  Start(["Start"]) -- Validate Store--> FetchApp["Fetch Application<br/>Details"]
  FetchApp --> ValidApp{"Does Application exists?<br/>Is 'status' of application valid?"}

  ValidApp -- No --> Error1["Error"]
  ValidApp -- Yes --> GetQs["Get store questions &<br/> the current question to be answered"]

  GetQs --> ValidQ{"Is the current question answerable?"}
  ValidQ -- No --> Error1
  ValidQ -- Yes --> HandleType{"Question<br/>Type"}

  HandleType -->|image| ImageAnswer["Save uploaded files<br/>as answer"]
  HandleType -->|applicantConfirm &<br/>the answer is 'reject'|Reset["Reset appointments<br/>& all answers"]
  HandleType -->|appointment| Appointment["Validate &<br/>reserve slot"]
  HandleType -->|other| SaveAnswer["Save answer<br/>content"]

  ImageAnswer --> NextQ["Move to the next question &<br/> Update Application Status"]
  Reset --> NextQ
  Appointment --> NextQ
  SaveAnswer --> NextQ

  NextQ --> Notify["Send Notifications to<br/>Admin & Applicant"]
  Notify --> Save["Save Application"]

  Error1 --> End(["End"])
  Save --> End

  classDef startend fill:#76c7c0,stroke:#333,stroke-width:2px,color:#fff,font-weight:bold
  classDef process fill:#6fa8dc,stroke:#333,stroke-width:1.5px,color:#222,font-weight:bold
  classDef decision fill:#ffb347,stroke:#333,stroke-width:2px,color:#333,font-weight:bold
  classDef error fill:#f44336,stroke:#900,stroke-width:2px,color:#fff,font-weight:bold
  classDef success fill:#4caf50,stroke:#256a2e,stroke-width:2px,color:#fff,font-weight:bold

  class Start,End startend
  class Tx,Parse,FetchApp,GetQs,ImageAnswer,Reset,Appointment,SaveAnswer,NextQ,Notify,AutoComplete,Save,Emit process
  class ValidApp,ValidQ,HandleType,AutoDone decision
  class Error1 error
  class Success success
```