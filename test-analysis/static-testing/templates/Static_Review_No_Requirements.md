# 📝 Static Analysis Template: Requirements Reconstruction (No Docs)
**Context:** Used when official documentation is missing or insufficient. 
**Objective:** Establish a "Test Basis" based on industry standards, technical constraints, and business logic.

---

## 🏗 1. System Logic & Business Rules (Inferred)



| Feature Area | Industry Standard / "Best Practice" | Business Goal (Assumed) |
| :--- | :--- | :--- |
| **User Onboarding** | Registration should be friction-less but secure (KYC compliant). | Increase conversion while maintaining data quality. |
| **Data Integrity** | Use of atomic fields (Street, City, Zip separately). | Enable accurate marketing and regional analytics. |
| **Error Handling** | Generic messages for Security (Login), Specific for UX (Registration). | Prevent account enumeration while helping users fix errors. |
| **Accessibility** | WCAG 2.1 Compliance (Contrast, Tab order, Aria-labels). | Broaden user base and ensure legal compliance (ADA). |

---

## 🔍 2. Field-Level Specification (Reconstructed)



*Since requirements are missing, the following technical constraints are assumed as the "Truth":*

### 2.1 Name & Identity
* **First/Last Name:** Must support UTF-8 (International names). Minimum 2 chars.
* **Date of Birth:** Banking rule: Must be 18+. Format: `MM/DD/YYYY`.
* **SSN:** Exactly 9 digits. Must be encrypted in the Database.

### 2.2 Address & Location
* **State:** Must be a dropdown to ensure **Data Normalization**.
* **Zip Code:** Must be a `String` to preserve leading zeros (e.g., New Jersey `07001`).
* **Normalization:** Street addresses must be split into Line 1 and Line 2.

---

## 🛡 3. Non-Functional Assumptions

### 3.1 Security Standards
* **Data in Transit:** All registration data must be sent over HTTPS (TLS 1.2+).
* **Data at Rest:** PII (SSN, Passwords) must be hashed/encrypted in the DB.
* **Input Sanitization:** Global filter for SQL Injection and XSS characters.

### 3.2 Performance
* **Response Time:** Registration submission should process in < 2 seconds.
* **Availability:** 99.9% uptime for the registration service.

---


## 🎓 Importance for a Test Analyst (ISTQB Perspective)

1.  **Establishing a Test Basis:** According to ISTQB, testing cannot happen without a basis. This document *becomes* that basis.
2.  **Early Defect Detection:** By "writing the requirements" yourself, you find logical gaps (e.g., "Wait, we forgot about Zip codes with zeros!") before a single line of code is tested.
3.  **Risk Mitigation:** You identify **Non-Functional risks** (Security, Performance) that developers might overlook without formal docs.
4.  **Stakeholder Management:** Presenting this to a PM/Developer changes the conversation from "I think this is a bug" to "This deviates from the industry standards we've established here."
