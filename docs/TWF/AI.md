---
sidebar_position: 2
---

# Apply Consent

The applyIdentity Logic processes the submission of identity verification documents by validating the uploaded files and types, retrieving the related application, and ensuring identity info hasn’t already been completed. It then saves the identity images and updates the LINE rich menu.

```mermaid
flowchart TD
    Start(["Start"]) -->  FetchApp["Fetch Application with<br/> Identity info"]
    FetchApp --> ValidApp{"Does the application <br/>exists & Identity info <br/>not filled?"}
    ValidApp -- No --> Error1["Error"]
    %% ValidApp -- Yes --> ValidatePics{"identity1Pic<br/>is valid?"}
    %% ValidatePics -- No --> Error2["Throw Error:<br/>identity Pic missing"]
    ValidApp -- Yes --> ApplyIdentity["Apply identity info<br/>+ upload pictures"]
    ApplyIdentity --> UpdateMenu["Update Richmenu<br/>for Application"]
    %% UpdateMenu --> Commit["Commit Transaction"]
    %% Commit --> Emit["Emit Application<br/>Update Event"]
    %% Emit --> Success["Send Success Response"]
    UpdateMenu --> End(["End"])

    Error1 --> End
    %% Error2 --> End

    Start:::startend
    %% CheckFiles:::process
    %% StartTx:::process
    FetchApp:::process
    ValidApp:::decision
    Error1:::error
    %% ValidatePics:::decision
    %% Error2:::error
    ApplyIdentity:::process
    UpdateMenu:::process
    %% Commit:::process
    %% Emit:::process
    %% Success:::success
    End:::startend

    classDef startend fill:#76c7c0,stroke:#333,stroke-width:2px,color:#fff,font-weight:bold
    classDef process fill:#6fa8dc,stroke:#333,stroke-width:1.5px,color:#222,font-weight:bold
    classDef decision fill:#ffb347,stroke:#333,stroke-width:2px,color:#333,font-weight:bold
    classDef error fill:#f44336,stroke:#900,stroke-width:2px,color:#fff,font-weight:bold
    classDef success fill:#4caf50,stroke:#256a2e,stroke-width:2px,color:#fff,font-weight:bold




```
