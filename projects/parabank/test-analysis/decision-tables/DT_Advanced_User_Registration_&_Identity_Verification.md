# 📊 Decision Table: Advanced User Registration & Identity Verification

**ID:** DT-01  
**Scope:** Complex validation of identity across local DB, government registries, and legacy banking systems, including legal capacity checks.

| **CONDITIONS** | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 | Rule 6 | Rule 7 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|Username unique in local DB? | No | Yes | Yes | Yes | Yes | Yes | Yes |
| SSN unique in local DB? | - | No | No | Yes | Yes | Yes | Yes |
| **Is Offline-only Client (Legacy)?**| - | **Yes** | **No** | - | - | - | - |
| **SSN valid in Gov Registry?** | - | Yes | - | **No** | Yes | Yes | Yes |
| **Legal Capacity (Adult/Able)?** | - | - | - | - | **No** | **Yes** | **Yes** |
| Phone unique in local DB? | - | - | - | - | - | No | Yes |
| Form Data Valid? | - | - | - | - | - | - | Yes |
| **ACTION**| --- | --- | --- | --- |  --- |  --- |  --- |
| **Show "Username taken"** | X | | | | | | |
| **Trigger Account Migration Flow** | | X | | | | | |
| **Show "Account exists" (SSN)** | | | X | | | | |
| **Show "Invalid/Fraud SSN"** | | | | X | | | |
| **Require Guardian/Legal Rep** | | | | | X | | |
| **Show "Phone linked"** | | | | | | X | |
| **Create Account & Notify** | | | | | | | X |

---
