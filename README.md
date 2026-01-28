# QA-Artifacts
> Personal QA Library: reusable check-lists,  test documentation templates, bug reporting frameworks
---
## 🛠️ Test Activities & Artifacts Mapping

This mapping demonstrates the alignment between the Software Testing Life Cycle (STLC) activities and the specific **testware** produced in this repository.

| Test Activity | Corresponding Testware (Artifacts) | Folder / Reference |
| :--- | :--- | :--- |
| **Test Planning** | [One-page Test Plan #TP001](./test-plans/templates/one-page-test-plan.md) | [📂 test-plans](./test-plans/) |
| **Test Analysis** |  [Requirements Specification Review Checklist](./static-testing/reviews/requirements-checklist.md)  [Static_Review_No_Requirements](./static-testing/templates/Static_Review_No_Requirements.md)| [📂 checklists](./static-testing/) |
| **Test Design** | [API & UI Test Scenarios / Checklists]() | `📂 checklists` |
| **Test Execution: Unit Level** | [Python Logic & Data Cleaning Scripts]() | `📂 basics-and-control-flow` |
| **Test Execution: API Level** | [Postman Collections & JSON Validations]() | `📂 network-programming` |
| **Test Execution: UI Level** | [Black-Box Testing on Financial Platforms](.) | `📂 target-platforms` |
| **Test Reporting** | [Test Summary Reports & Bug Logs]() | `📂 reports` |

---

## 🎯 Target Platforms for Practice
> I use the following platforms to apply Black-box test design techniques within the Financial and Banking domains:

### 1. [Altoro Mutual (by IBM)](https://demo.testfire.net/)
* A classic demo application representing a retail banking system.
  * **Domain:** Retail Banking.
  * **Testing Focus:** User authentication, fund transfers between accounts, transaction history, and statement search functionality.
  * **Key Techniques:** Ideal for Boundary Value Analysis (transfer limits), Decision Tables (login logic), and Error Guessing.

### 2. [ParaBank (by Parasoft)](https://parabank.parasoft.com/parabank/index.htm)
* A robust simulation of a real-world bank with complex workflows.
  * **Domain:** Personal Banking & Lending Services.
  * **Testing Focus:** New account opening, Loan Request processing, and customer administration.
  * **Key Techniques:** State Transition Testing (loan application statuses: Pending -> Approved/Denied) and Equivalence Partitioning (interest rates based on deposit amounts).

### 3. [DBank Demo](http://dbankdemo.com/)
* A modern interface that mimics a contemporary digital banking experience.
   * **Domain: Digital/Online Banking.**
   * **Testing Focus:** Creating savings/checking accounts, credit card linking, and user profile management.
   *  **Key Techniques:** Form validation (Regex checks) and functional testing of "Checking vs. Savings" balance logic.
