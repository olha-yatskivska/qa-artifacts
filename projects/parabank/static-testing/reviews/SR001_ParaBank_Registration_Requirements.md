
# 📝 Static Review: ParaBank Registration Requirements
> **Identifier:** #SR001  
> **Project:** ParaBank  
> **Focus:** Registration Form Fields & Logic  
> **Status:** Open

---

## 🎯 Objective
The purpose of this static review is to identify potential ambiguities, missing requirements, or logical inconsistencies in the **User Registration** form before starting the test design phase.

## 📋 Field Analysis Table
| ID | Field Name | Mandatory? | Observations & Risks |
| :--- | :--- | :--- | :--- |
| **F-01** | First Name | Yes | Length limit? Special characters support? |
| **F-02** | Last Name | Yes | Same as First Name. |
| **F-03** | Address | Yes | Format validation (Street, House)? |
| **F-04** | City | Yes | Dropdown or free text? |
| **F-05** | State | Yes | Minimum 2 characters? |
| **F-06** | Zip Code | Yes | International support or US only? |
| **F-07** | Phone # | No | Expected format/mask? |
| **F-08** | SSN | Yes | Masking (XXX-XX-XXXX) requirement? |
| **F-09** | Username | Yes | Uniqueness logic? |
| **F-10** | Password | Yes | Complexity rules missing. |
| **F-11** | Confirm | Yes | Match logic requirements. |

## 🚩 Logical & Business Risks Identified
* **SR-RISK-01:** Missing Password Complexity Rules.
* **SR-RISK-02:** SSN Privacy & Encryption.
* **SR-RISK-03:** Zip Code Localization.
* **SR-RISK-04:** Buffer Overflow (Missing Length Validation).
* **SR-RISK-05:** Error Messaging Consistency.
* **SR-RISK-06:** Critical Lack of Data Validation (Symbols/Length).
* **SR-RISK-07:** Undefined Field Formats (Phone/Zip Masks).Username Uniqueness Logic (Current system allows/ambiguous).
* **SR-RISK-09:** Identity Theft (Duplicate SSN): System might allow creating a second account with an already registered SSN.
* **SR-RISK-10:** Contact Info Duplication: No policy on whether multiple users can share the same Phone number.Username Uniqueness Logic.
* **SR-RISK-11: Poor UX due to Late Validation.** Missing real-time (inline) match check for "Confirm Password" field. (Risk: User frustration and repeated data entry if passwords don't match after form submission).
* **SR-RISK-12: Legal Compliance (Age Verification).** The form lacks a "Date of Birth" field. (Risk: Underage users can register, leading to legal and regulatory violations for a financial institution).
* **SR-RISK-13:** Legal Capacity Verification. The system may allow registration for individuals with restricted legal capacity (e.g., legally incapacitated persons). (Risk: Financial contracts signed by such individuals are legally void).
* **SR-RISK-14:** Lack of Representative Registration. System doesn't allow legal guardians to register accounts for their dependents. (Risk: Loss of a huge market segment - children's and trust accounts).
* **SR-RISK-15:** Criminal/AML Risk. Registration of individuals on "Blacklists" (Sanctions, Criminal records). (Result: Regulatory fines).
* **SR-RISK-16:** Duplicate Profile Creation (Legacy Migration). Risk of creating a second ID for a customer who already exists in the old offline database.
* **SR-RISK-17:** Data Inconsistency. Risk that user-provided data doesn't match the bank's existing records for the same SSN.

## 💡 Recommendations:
* **SR-REC-01:** Implement real-time inline validation for the "Confirm Password" field to provide immediate feedback (Addresses SR-RISK-11).
* **SR-REC-02:** Define and document Min/Max character limits for all input fields (Addresses SR-RISK-04 & SR-RISK-06).
* **SR-REC-03:** Add a mandatory "Date of Birth" field with age validation logic (Minimum 18 years) to ensure legal compliance (Addresses SR-RISK-12).

