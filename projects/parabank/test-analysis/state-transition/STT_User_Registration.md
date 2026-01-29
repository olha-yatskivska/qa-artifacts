# 📋 State Transition Table: User Registration

**ID:** STT-01  
**Scope:** Detailed definition of valid transitions, triggers, and system responses during the registration process.

| ID | From State | Event / Condition | To State | System Action |
| :--- | :--- | :--- | :--- | :--- |
| **TR-01** | `Draft` | User clicks "Register" | `Validating (Local)` | Show Loading Spinner, Lock Form fields |
| **TR-02** | `Validating (Local)` | Username OR Phone exists in DB | `Rejected` | Show "User/Phone Taken" Error, Unlock Form |
| **TR-03** | `Validating (Local)` | SSN matches Offline Client | `Migration Pending` | Redirect to Identity Verification Screen |
| **TR-04** | `Validating (Local)` | All Local Checks Pass | `Validating (Gov)` | Send API Request to Gov Registry |
| **TR-05** | `Validating (Gov)` | Gov API returns "Invalid SSN" | `Rejected` | Log Fraud Attempt, Show Generic Error |
| **TR-06** | `Validating (Gov)` | Gov API returns "Minor/Incapacitated" | `Guardian Approval` | Send Request to Guardian Contact Info |
| **TR-07** | `Validating (Gov)` | Gov API returns "Valid Adult" | `Active` | Create Account, Send Welcome SMS |
| **TR-08** | `Migration Pending` | User confirms Legacy Data (e.g., Contract ID) | `Active` | Link Web Account to Legacy ID |
| **TR-09** | `Guardian Approval` | Guardian approves request (via Link/SMS) | `Active` | Unblock Account, Notify User |
| **TR-10** | `Guardian Approval` | Timer expires (24h) OR Denial | `Rejected` | Delete Temporary Data, Notify User |

---
