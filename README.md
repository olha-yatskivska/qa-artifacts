# QA-Artifacts
> Personal QA Library: reusable check-lists,  test documentation templates, bug reporting frameworks
---
## 🛠️ Test Activities & Artifacts Mapping

This mapping demonstrates the alignment between the Software Testing Life Cycle (STLC) activities and the specific **testware** produced in this repository.

| Test Activity | Corresponding Testware (Artifacts) | Folder / Reference |
| :--- | :--- | :--- |
| **Test Planning** | [One-page Test Plan #TP001](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-plans/templates/One_Page_Test_Plan.md) | [📂 test-plans](https://github.com/olha-yatskivska/qa-artifacts/tree/main/test-plans) |
| **Test Analysis** | [Requirements Specification Review Checklist](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/static-testing/reviews/Requirements_Checklist.md)<br>  <br>[Static_Review_No_Requirements](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/static-testing/templates/Static_Review_No_Requirements.md)<br> <br>[Prioritized Test Conditions](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/templates/Prioritized_Test_Conditions.md)<br> <br>[Requirements & Risk Traceability Matrix](https://github.com/olha-yatskivska/qa-artifacts/blob/main/test-analysis/templates/RTM.md)<br>| [📂 test analysis](https://github.com/olha-yatskivska/qa-artifacts/tree/main/test-analysis) |
| **Test Design** |  API & UI Test Scenarios / Checklists <br> Decision Table <br> Diagram <br> Test Charter <br> Prioritized Test Cases <br>  Test Charters<br> Coverage Items<br> Test Data & Test Environment requirements| `📂 test design` |
| **Test implementation** |Test Procedures <br> Automated Test Scripts <br> Test Suites <br> Test Data <br> Test Execution Schedule|`📂 test implementation`|
| **Test Execution: Unit Level** | Python Logic & Data Cleaning Scripts | `📂 basics-and-control-flow` |
| **Test Execution: API Level** | Postman Collections & JSON Validations | `📂 network-programming` |
| **Test Execution: UI Level** | Black-Box Testing on Financial Platforms | `📂 target-platforms` |
| **Test Reporting** | Test Summary Reports <br> Bug Logs | `📂 reports` |

---

## 🎯 Target Platforms for Practice
> I use the following platforms to apply Black-box test design techniques within the Financial and Banking domains:

### 1. [ParaBank (by Parasoft)](https://github.com/olha-yatskivska/qa-artifacts/tree/main/projects/parabank)
* A robust simulation of a real-world bank with complex workflows.
  * **Domain:** Personal Banking & Lending Services.
  * **Testing Focus:** New account opening, Loan Request processing, and customer administration.
  * **Key Techniques:** State Transition Testing (loan application statuses: Pending -> Approved/Denied) and Equivalence Partitioning (interest rates based on deposit amounts).


### 2. [Altoro Mutual (by IBM)](https://demo.testfire.net/)
* A classic demo application representing a retail banking system.
  * **Domain:** Retail Banking.
  * **Testing Focus:** User authentication, fund transfers between accounts, transaction history, and statement search functionality.
  * **Key Techniques:** Ideal for Boundary Value Analysis (transfer limits), Decision Tables (login logic), and Error Guessing.


### 3. [DBank Demo](http://dbankdemo.com/)
* A modern interface that mimics a contemporary digital banking experience.
   * **Domain: Digital/Online Banking.**
   * **Testing Focus:** Creating savings/checking accounts, credit card linking, and user profile management.
   *  **Key Techniques:** Form validation (Regex checks) and functional testing of "Checking vs. Savings" balance logic.
