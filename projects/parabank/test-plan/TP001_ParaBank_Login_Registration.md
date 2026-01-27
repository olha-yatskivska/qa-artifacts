# 📋 Test Plan: ParaBank – User Login & Registration
> **Identifier:** #TP001  
> **Project:** ParaBank (Demo Banking System)  
> **Status:** Draft / In Progress  

---

## 🔍 Project Overview
| Attribute | Details |
| :--- | :--- |
| **Project** | [ParaBank](https://parabank.parasoft.com/) |
| **Domain** | Personal Banking & Lending Services |
| **Feature** | User Login & Registration |
| **Owner** | Tester Tester |
| **Sprint** | Winter2026 |

---

## 📖 Introduction
This Test Plan defines the strategy, resources, and schedule for testing the User Authentication and Registration modules of the ParaBank application. The goal is to ensure secure access and valid data entry for new and existing customers.

## 🎯 Goals
1. **Functional Integrity:** Verify that a new user can successfully register with valid data.
2. **Access Control:** Ensure only authorized users can log in to the system.
3. **Error Handling:** Validate that the system correctly rejects invalid login/registration attempts.
4. **Python Practice:** Implement basic automated checks to verify page availability and field requirements.

## 🏗️ Scope
* **In Scope:**
    * **User Registration:** Form validation (mandatory fields, data types).
    * **User Login:** Positive/Negative scenarios, session persistence.
    * **Logout:** Security of the session termination.
* **Out Of Scope:**
    * Database-level testing (direct SQL checks).
    * Performance under high load.
    * Money transfers and loan processing (covered in separate plans).

## ⚠️ Risks
* **Environment Stability:** Since ParaBank is a public demo, data might be reset or the site might be slow.
* **Ambiguous Requirements:** Lack of clear password complexity rules (requires **Error Guessing**).
* **Network Latency:** Potential issues during API-level checks using Python.

## ⚙️ Environments & Tools
* **Browsers:** Chrome, Firefox (latest versions).
* **Tools:** Python 3.x, Requests library, GitHub.
* **Test Design Techniques:** Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Decision Tables.

## 🏁 Criteria
### Entry Criteria
* [ ] Test Environment (ParaBank) is up and running.
* [ ] Requirements for registration fields are analyzed.
* [ ] Python scripts for basic health checks are ready.

### Exit Criteria
* [ ] 100% of Critical and High-priority test cases are executed.
* [ ] **At least 90%** of all scenarios passed.
* [ ] All discovered defects are logged in the Bug Log.

## 📅 Schedule and Estimations
**Timeline:** 27.01.26 – 15.02.26 

| Task | Estimation |
| :--- | :--- |
| Analysis of Login/Reg requirements | 1 day |
| Test Design (Checklist creation) | 2 days |
| Test Execution (Manual + Python) | 3 days |
| Final Reporting & Bug Fix Verification | 1 day |
