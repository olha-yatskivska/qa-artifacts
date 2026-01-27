# ✅ Test Checklist: ParaBank Registration
> **Identifier:** #CL001  
> **Linked Test Plan:** [#TP001](projects/parabank/test-plans/TP001_ParaBank_Login_Registration.md)  
> **Linked Static Review:** [#SR001](static-testing/reviews/SR001_ParaBank_Registration_Requirements.md)

---

## 🟢 1. Positive Scenarios (Happy Path)
*Focus: Verifying that the system works under ideal conditions.*

| ID | Description | Expected Result | Status |
| :--- | :--- | :--- | :--- |
| **REG-POS-01** | Register a new user with all valid fields (standard length) | Account created, redirected to "Welcome" page | [ ] |
| **REG-POS-02** | Register with only mandatory fields (leave Phone empty) | Account created successfully | [ ] |

---

## 🔴 2. Field Validation (Negative)
*Focus: Verifying error handling identified in SR001.*

| ID | Description | Expected Result | Status |
| :--- | :--- | :--- | :--- |
| **REG-NEG-01** | Submit the form with all fields empty | Red error messages appear near every mandatory field | [ ] |
| **REG-NEG-02** | Register with a Username that already exists | Error message: "This username already exists" | [ ] |
| **REG-NEG-03** | Enter different values in "Password" and "Confirm" | Error message indicating password mismatch | [ ] |

---

## 🧪 3. Data Integrity & Edge Cases (Boundary Value Analysis)
*Focus: Testing the limits of the system where no validation was found.*

| ID | Description | Expected Result | Status |
| :--- | :--- | :--- | :--- |
| **REG-DATA-01** | Enter 1 character in "First Name" and "Last Name" | System should reject or ask for a valid name (based on SR001 risk) | [ ] |
| **REG-DATA-02** | Enter 500+ characters in "City" field | System handles long string without 500 Error (Server-side check) | [ ] |
| **REG-DATA-03** | Enter special characters (@#$%) in "SSN" field | System rejects non-numeric input for SSN | [ ] |

---

## 🐍 4. Python Automation Candidates (Optional)
*Focus: Small scripts to speed up testing.*

* [ ] **AUTO-01:** Script to check if Registration page returns 200 OK.
* [ ] **AUTO-02:** Script to attempt registration via API with an existing username.
