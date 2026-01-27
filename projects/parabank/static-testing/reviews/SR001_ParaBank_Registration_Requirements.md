
# 📝 Static Review: ParaBank Registration Requirements
> **Identifier:** #SR001  
> **Project:** ParaBank  
> **Focus:** Registration Form Fields & Logic  
> **Status:** Open

---

## 🎯 Objective
The purpose of this static review is to identify potential ambiguities, missing requirements, or logical inconsistencies in the **User Registration** form before starting the test design phase.

## 📋 Field Analysis Table
| Field Name | Mandatory? | Expected Data Type / Constraints | Observations & Risks (Ambiguities) |
| :--- | :--- | :--- | :--- |
| **First Name** | Yes | String (Alpha) | What is the length limit? Are special characters allowed? |
| **Last Name** | Yes | String (Alpha) | Same as First Name. |
| **Address** | Yes | String (Alphanumeric) | Is there a format validation (e.g. Street, House)? |
| **City** | Yes | String (Alpha) | Is there a dropdown or free text? |
| **State** | Yes | String (Alpha) | Minimum 2 characters? |
| **Zip Code** | Yes | Numeric / Alphanumeric | Only US format (5 digits) or international? |
| **Phone #** | No? | Numeric / Special chars | Is it mandatory? What format is expected? |
| **SSN** | Yes | Numeric | Social Security Number format (XXX-XX-XXXX)? |
| **Username** | Yes | String (Unique) | What happens if the username already exists? |
| **Password** | Yes | String (Masked) | Complexity rules (digits, caps, length) are not specified. |
| **Confirm** | Yes | String (Masked) | Must exactly match "Password". |

---

## 🚩 Logical & Business Risks Identified
1. **Missing Complexity Rules:** No instructions for password strength (Risk: Weak passwords).
2. **SSN Privacy:** Registration asks for SSN (Social Security Number). Is this encrypted? (Security Risk).
3. **Zip Code Localization:** If the bank is international, 5-digit zip might be too restrictive.
4. **Error Messaging:** No information on where error messages appear (top of form or under fields).

## 💡 Recommendations
* Define Min/Max character limits for each field.
* Add real-time validation (Inline validation) for the "Confirm Password" field.
* Clarify if the Phone number is mandatory (it's often a source of confusion).
