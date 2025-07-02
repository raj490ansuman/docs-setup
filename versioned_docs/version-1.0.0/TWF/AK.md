---
sidebar_position: 2
---

# Apply Koza

The applyKoza logic validates the store ID and bank account (koza) information, including a required image, then fetches the related application and ensures the koza data is not already completed. It applies the submitted koza details and image to the application, updates the LINE rich menu accordingly.

```mermaid
flowchart TD
  classDef startend fill:#76c7c0,stroke:#333,stroke-width:2px,color:#fff,font-weight:bold;
  classDef process fill:#6fa8dc,stroke:#333,stroke-width:1.5px,color:#222,font-weight:bold;
  classDef decision fill:#ffb347,stroke:#333,stroke-width:2px,color:#333,font-weight:bold;
  classDef error fill:#f44336,stroke:#900,stroke-width:2px,color:#fff,font-weight:bold;
  classDef success fill:#4caf50,stroke:#256a2e,stroke-width:2px,color:#fff,font-weight:bold;

  Start(["Start"]):::startend --Validate store--> ValidateKoza["Validate bank information<br/>(provider, branch,<br/>accId, accName)"]:::process
  ValidateKoza --> CheckImage{"Is the Bank image<br/>uploaded?"}:::decision
  CheckImage -- No --> Error1["Error"]:::error
  CheckImage -- Yes --> FetchApp["Fetch Application with<br/> bank info"]:::process
  FetchApp --> ValidApp{"Does the application<br/> exists & bank info <br/>not filled?"}:::decision
  ValidApp -- No --> Error1:::error
  ValidApp -- Yes --> FillKoza["Fill Bank Info"]:::process
  FillKoza --> UpdateMenu["Update Richmenu"]:::process
  %% UpdateMenu --> Emit["Emit Application<br/>Update Event"]:::process
  %% Emit --> Commit["Commit Transaction"]:::process
  %% Commit --> Success["Send Success Response"]:::success
  UpdateMenu --> End(["End"]):::startend

  Error1 --> End
  %% Error2 --> End

```
