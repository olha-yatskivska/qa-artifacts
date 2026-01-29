# 🔄 State Transition Diagram: User Registration Lifecycle

**ID:** STD-01  
**Scope:** Lifecycle of a user registration request, handling local validation, external government checks, legacy migration, and guardian approval flows.

### 1. Visual Diagram (Mermaid)

```mermaid
stateDiagram-v2
    [*] --> Draft
    
    state "Validating (Local)" as V_Loc
    state "Validating (External/Gov)" as V_Gov
    state "Migration Pending" as Mig_Pend
    state "Guardian Approval" as Guard_App
    state "Active (Registered)" as Active
    state "Rejected/Error" as Rejected

    Draft --> V_Loc : Click "Register"
    
    %% Local Validation Logic
    V_Loc --> Rejected : Username/Phone Exists
    V_Loc --> Mig_Pend : Offline Client Found (Legacy Match)
    V_Loc --> V_Gov : Data Unique & Valid
    
    %% External Validation Logic
    V_Gov --> Rejected : SSN Invalid / Fraud Flag
    V_Gov --> Guard_App : Age < 18 / Incapacitated
    V_Gov --> Active : Validation Success (Adult)
    V_Gov --> V_Gov : Timeout (Retry)

    %% Complex Flows
    Mig_Pend --> Active : Identity Verified (Contract #)
    Mig_Pend --> Rejected : Verification Failed

    Guard_App --> Active : Guardian Confirmed
    Guard_App --> Rejected : Guardian Denied / Timeout

    Rejected --> Draft : User Corrects Data
    Active --> [*]
