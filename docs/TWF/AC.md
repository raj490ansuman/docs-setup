---
sidebar_position: 2
---

# Apply Consent

The applyConsent Logic validates the store ID and checks the applicant’s consent status, ensuring consent hasn’t been previously submitted. It converts the submitted base64 signature image into a buffer, creates a new consent record linked to the application, and saves the signature image.

```mermaid
flowchart TD
  classDef startend fill:#76c7c0,stroke:#333,stroke-width:2px,color:#fff,font-weight:bold;
  classDef process fill:#6fa8dc,stroke:#333,stroke-width:1.5px,color:#222,font-weight:bold;
  classDef decision fill:#ffb347,stroke:#333,stroke-width:2px,color:#333,font-weight:bold;
  classDef error fill:#f44336,stroke:#900,stroke-width:2px,color:#fff,font-weight:bold;
  classDef success fill:#4caf50,stroke:#256a2e,stroke-width:2px,color:#fff,font-weight:bold;

  Start(["Start"]):::startend --validate store--> FetchApp["Fetch Application with<br/>Consent info"]:::process
  FetchApp --> ValidApp{"Does the application exists<br/>& consent not provided?"}:::decision
  ValidApp -- No --> Error["Error"]:::error
  ValidApp -- Yes --> CreateConsent["Create User<br/>Consent Record"]:::process
  CreateConsent --> SaveImage["Save Consent Image"]:::process
  SaveImage -->  End(["End"]):::startend

  Error --> End



```
