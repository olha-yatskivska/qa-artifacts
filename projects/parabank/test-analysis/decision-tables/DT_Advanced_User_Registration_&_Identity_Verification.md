# 📊 Decision Table: Advanced User Registration & Identity Verification

**ID:** DT-01  
**Scope:** Complex validation of identity across local DB, government registries, and legacy banking systems, including legal capacity checks.

| Type | Element | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 | Rule 6 | Rule 7 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Cond.** | Username unique in local DB? | No | Yes | Yes | Yes | Yes | Yes | Yes |
| **Cond.** | SSN unique in local DB? | - | No | No | Yes | Yes | Yes | Yes |
| **Cond.** | **Is Offline-only Client (Legacy)?**| - | **Yes** | **No** | - | - | - | - |
| **Cond.** | **SSN valid in Gov Registry?** | - | Yes | - | **No** | Yes | Yes | Yes |
| **Cond.** | **Legal Capacity (Adult/Able)?** | - | - | - | - | **No** | **Yes** | **Yes** |
| **Cond.** | Phone unique in local DB? | - | - | - | - | - | No | Yes |
| **Cond.** | Form Data Valid? | - | - | - | - | - | - | Yes |
| --- |--- | --- | --- | --- | --- |  --- |  --- |  --- |
| **ACTION** | **Show "Username taken"** | X | | | | | | |
| **ACTION** | **Trigger Account Migration Flow** | | X | | | | | |
| **ACTION** | **Show "Account exists" (SSN)** | | | X | | | | |
| **ACTION** | **Show "Invalid/Fraud SSN"** | | | | X | | | |
| **ACTION** | **Require Guardian/Legal Rep** | | | | | X | | |
| **ACTION** | **Show "Phone linked"** | | | | | | X | |
| **ACTION** | **Create Account & Notify** | | | | | | | X |

---
