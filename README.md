# 📋 QA-Artifacts

> **Personal QA Library:** Reusable checklists, test documentation templates, and bug reporting frameworks.

---

## 🛠️ Test Activities & Artifacts Mapping

This mapping demonstrates the alignment between the Software Testing Life Cycle (STLC) activities and the specific **testware** produced in this repository.

| Test Activity | Corresponding Testware (Artifacts) | Folder / Reference |
| :--- | :--- | :--- |
| **Test Planning** | [One-page Test Plan #TP001](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-plans/templates/One_Page_Test_Plan.md) | `📂 test-plans` |
| **Test Analysis** | [Requirements Review Checklist](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/static-testing/reviews/Requirements_Checklist.md)<br>[Static Review (No Requirements)](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/static-testing/templates/Static_Review_No_Requirements.md)<br>[Prioritized Test Conditions](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/templates/Prioritized_Test_Conditions.md)<br>[Traceability Matrix (RTM)](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/templates/RTM.md) | `📂 test-analysis` |
| **Test Design** | Prioritized Test Cases <br> API & UI Scenarios<br>Decision Tables<br>Test Charters<br>Coverage Items<br>Test Data Requirements | `📂 test-design` |
| **Test Implementation** | Test Procedures<br>Automated Test Scripts<br>Test Suites<br>Execution Schedule | `📂 test-implementation` |
| **Test Execution** | **Unit:** Python Logic Scripts<br>**API:** Postman Collections (JSON Validation)<br>**UI:** Black-Box on Financial Platforms | `📂 execution` |
| **Test Reporting** | Test Summary Reports (TSR)<br>Bug Logs / Defect Reports | `📂 reports` |

---

## 🎯 Target Platforms for Practice

### 1. [ParaBank](https://parabank.parasoft.com/) | [My Project Files](https://github.com/olha-yatskivska/qa-artifacts/tree/main/projects/parabank)
* **Domain:** Personal Banking & Lending.
* **Testing Focus:** Account opening, Loan processing.
* **Techniques:** State Transition (Loan Status), Equivalence Partitioning (Interest Rates).

### 2. [Altoro Mutual](https://demo.testfire.net/)
* **Domain:** Retail Banking.
* **Testing Focus:** Authentication, Fund transfers, Transaction history.
* **Techniques:** BVA (Transfer limits), Decision Tables (Login), Error Guessing.

### 3. [DBank Demo](http://dbankdemo.com/)
* **Domain:** Digital/Online Banking.
* **Testing Focus:** Savings/Checking accounts, User profile management.
* **Techniques:** Form Validation (Regex), Logic Testing (Balance checks).
