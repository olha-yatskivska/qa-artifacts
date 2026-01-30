# 📋 Prioritized Test Conditions: User Registration

**Test Basis:** [SR001_ParaBank_Registration_Requirements.md](../static-testing/reviews/SR001_ParaBank_Registration_Requirements.md)  
**Technique:** Atomic Field Decomposition

---

## 👤 1. First & Last Name Fields
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-NAM-01** | SR001.F-01,  SR001.F-02 | System | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "First/Last Name is required" |
| **TC-NAM-02** | SR001.F-01,  SR001.F-02 | Unit | 1 Character (Min Boundary - 1) | BVA | P2 | Error message regarding minimum length |
| **TC-NAM-03** | SR001.F-01,  SR001.F-02 | Unit | 2 Characters (Min Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-04** | SR001.F-01,  SR001.F-02 | Unit | 50 Characters (Max Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-05** | SR001.F-01,  SR001.F-02, SR-RISK-04 | System | 51 Characters (Max Boundary + 1) | BVA | P2 | Error or graceful truncation |
| **TC-NAM-06** | SR001.F-01, SR001.F-02, SR-RISK-06 | System | Non-Latin Chars (UTF-8) | L10n | P3 | Success (Cyrillic, Diacritics, Hanzi) |
| **TC-NAM-08** | SR001.F-01,  SR001.F-02, SR-RISK-06 | System | Numeric/Special Symbol Rejection | Validation | P2 | Error: Numbers/Symbols not allowed |
| **TC-NAM-09** | SR001.F-01,  SR001.F-02 | System | HTML/Script Tags Injection | Security | P2 | Tags are escaped or rejected (No XSS execution) |
| **TC-NAM-10** | SR001.F-01,  SR001.F-02| Integration | Leading/Trailing Spaces | Integrity | P3 | Spaces are trimmed before DB persistence |

---

## 📮 2. Address & Location (Street, City, State)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ADR-01** | SR001.F-03, SR-RISK-06 | System | Alphanumeric & Symbols (`#`, `.`, `/`) | Functional | P2 | Success (e.g., Apt. #4, 1/2 St.) |
| **TC-ADR-02** | SR001.F-03 | System | Address Line 2 Optionality | Business | P2 | Success when left blank |
| **TC-ADR-03** | SR001.F-03 | Unit | 50 Characters (Max Boundary) | BVA | P2 | Success - Data accepted |
| **TC-ADR-04** | SR001.F-03, SR-RISK-04 | System | 51 Characters (Max Boundary + 1) | BVA | P2 | Error or graceful truncation |
| **TC-CTY-01** | SR001.F-04 | System | Multi-word City Names | L10n | P2 | Success (e.g., New York, Los Angeles) |
| **TC-STA-01** | SR001.F-05 | System | State: 2-letter ISO Code (NY, CA) | Validation | P2 | Success |
| **TC-STA-02** | SR001.F-05 | Unit | State: Invalid length (1 or 3+ chars) | BVA | P2 | Error: "Use 2-letter state code" |
---

## 🔢 3. Zip Code
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ZIP-01** | SR001.F-06 | System | Numeric Only Validation | Validation | P1 | Error if letters/symbols are entered |
| **TC-ZIP-02** | SR001.F-06 | Integration | Leading Zero Preservation (`00501`) | Integrity | P1 | **Critical:** Data stored as "00501", not "501" |
| **TC-ZIP-03** | SR001.F-06 | Unit | 5-Digit Length (Standard US) | BVA | P1 | Success |
| **TC-ZIP-04** | SR001.F-06 | Unit | 9-Digit Length (ZIP+4: `12345-6789`) | BVA | P2 | Success |
| **TC-ZIP-05** | SR001.F-06 | Unit | 9-Digit Length (ZIP+4: `12345-6789`) | BVA | P2 | Success |
| **TC-ZIP-06** | SR001.F-06, SR-RISK-07 | System | Zip mask | UX | P3 | 5-Digit Mask: 00000 (e.g., 12345), or ZIP+4 Mask: 00000-0000 (e.g., 12345-6789)  |
---

## 📱 4. Phone Number
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PHN-01** | SR001.F-07 | System | Optionality Check (Empty field) | Business | P2 | Success - Registration completes |
| **TC-PHN-02** | SR001.F-07, SR-RISK-06  | Unit | Numeric Only Validation | Validation | P2 | Error if letters are entered |
| **TC-PHN-03** | SR001.F-07, SR-RISK-06 | Unit | Minimum Length Boundary | BVA | P3 | Error regarding invalid phone length |
| **TC-PHN-04** | SR001.F-07, SR-RISK-06 | Unit | Maximum Length Boundary | BVA | P3 | Error or graceful truncation |
| **TC-PHN-05** | SR001.F-07, SR-RISK-06 | System | Special Chars Support (`+`, `-`, `( )`) | L10n | P3 | Success - Support for standard formats |
| **TC-PHN-06** | SR001.F-07, SR-RISK-05| Integration | Meaningless Data Rejection (e.g., "0") | Data Quality | P3 | Error: "Please enter a valid phone number" |
| **TC-PHN-07** | SR001.F-07, SR-RISK-07 | System | Phone mask | UX | P3 | expected format (e.g., in a placeholder) before the user starts typing, but ensure the mask itself (e.g., (___) ___-____) appears upon interaction to guide them.  |

---

## 🛡️ 5. Social Security Number (SSN)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-SSN-01** | SR001.F-08 | System | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "SSN is required" |
| **TC-SSN-02** | SR001.F-08, SR-RISK-06 | Unit | Numeric Only Validation | Validation | P1 | Error if letters or symbols |
| **TC-SSN-03** | SR001.F-08, SR-RISK-06 | Unit | Exact Length (Boundary: 9 digits) | BVA | P1 | Success - Data accepted |
| **TC-SSN-04** | SR001.F-08, SR-RISK-06 | Unit | Invalid Length (< 9 or > 9 digits) | BVA | P1 | Error: "SSN must be 9 digits" |
| **TC-SSN-05** | SR001.F-08, SR-RISK-02 | System | UI Masking (Privacy) | Security | P1 | Input is masked as user types |
| **TC-SSN-06** | SR001.F-08 | System | Formatting Support (With/Without Hyphens) | L10n | P2 | Success for both formats |
| **TC-SSN-07** | SR001.F-08, SR-RISK-09 | Integration | Duplicate SSN Check | Logic | P1 | Error: "SSN already registered" |
| **TC-SSN-08** | SR001.F-08 | System | UI Masking (Security) | Security | P1 | All characters masked (●●●●●) |

---

## 🔑 6. Username Logic
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-USR-01** | SR001.F-09 | System | Empty Input | Functional | P1 | Inline error: "Username is required" |
| **TC-USR-02** | SR001.F-09, SR-RISK-08 | Integration | Unique Username Check (DB) | Logic | P1 | Error: "This username already exists" |
| **TC-USR-03** | SR001.F-09 | Integration | Case-Insensitivity Check | Logic | P2 | Error: Duplicate detected |
| **TC-USR-04** | SR001.F-09 | Unit | Minimum Length (Boundary: 4 chars) | BVA | P2 | Error if username is too short |
| **TC-USR-04** | SR001.F-09, SR-RISK-04 | System | 51 Characters (Max Boundary + 1) | BVA | P2 | Error or graceful truncation |
| **TC-USR-05** | SR001.F-09 | System | Space Handling (No spaces allowed) | Validation | P2 | Error or automatic removal |
| **TC-USR-06** | SR001.F-09 | System | Special Characters in Username | Security | P2 | Rejection of dangerous symbols (SQLi) |

---

## 🔐 7. Password & Confirmation
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-01** | SR001.F-10, SR-RISK-05 | System | Empty Password Input | Functional | P1 | Inline error: "Password is required" |
| **TC-CMF-02** | SR001.F-11, SR-RISK-05 | System | Empty Confirm Input | Functional | P1 | Inline error: "Please confirm password" |
| **TC-PWD-03** | SR001.F-10, SR001.F-11, SR-RISK-05 | System | Password & Confirm Match | Logic | P1 | Error if values differ |
| **TC-PWD-04** | SR001.F-10, SR001.F-11, SR-RISK-01 | System | UI Masking (Security) | Security | P1 | All characters masked (●●●●●) |
| **TC-PWD-05** | SR001.F-10, SR001.F-11, SR-RISK-01 | Unit | Complexity: Minimum Length | BVA | P2 | Error if below minimum |
| **TC-PWD-06** | SR001.F-10, SR001.F-11, SR-RISK-01 | Unit | Complexity: Character Types | Security | P2 | Validation of password strength rules |
| **TC-PWD-07** | SR001.F-10, SR001.F-11, SR-RISK-01 | System | Copy-Paste Limitation | Security | P3 | (Optional) Prevention of pasting |
| **TC-PWD-08** | SR001.F-10, SR001.F-11 | System | SQL Injection in Password | Security | P2 | Input is sanitized/hashed |

---

## 🛡️ 8. Business Integrity & Identity (Cross-Field Logic)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-INT-01** | SR001.F-08, SR-RISK-09 | Integration | Duplicate SSN Check | Business | P1 | System blocks registration |
| **TC-INT-02** | SR001.F-07, SR-RISK-10 | Integration | Duplicate Phone Check | Business | P2 | System flags or blocks if Phone exists |
| **TC-INT-03** | SR001.F-08, SR001.F-09, SR-RISK-09 | Integration | Conflict: Same SSN, Diff Username | Business | P1 | Hard block: 1 SSN = 1 User |
| **TC-INT-04** | SR001.F-08, SR001.F-08 | Integration | Conflict: Same Phone, Diff SSN | Business | P2 | Verification required |

---

## 🔐 9. Password Strength Conditions
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-09** | SR001.F-10, SR001.F-11, SR-RISK-01 | Unit | Low Strength: < 8 chars | Security | P3 | Warning/Rejection |
| **TC-PWD-10** | SR001.F-10, SR001.F-11, SR-RISK-01  | Unit | Medium Strength | Security | P2 | Success: "Medium password" |
| **TC-PWD-11** | SR001.F-10, SR001.F-11, SR-RISK-01  | Unit | Strong Strength | Security | P1 | Success: "Strong password" |

---
## 10 Non-Functional
| ID | Traceability | Test Level | Test Condition | Category | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ACC-01** | Legal/Risk | System | Keyboard navigation support (WCAG compliance) | Accessibility | P2 |
| **TC-PERF-01** | UX/Risk | System | Loading state/Spinner display after submit | Performance | P3 |
| **TC-DT-01** | SR001.8 | Integration | Decision Table: User/SSN/Phone uniqueness check | Logic/Data | P1 |
| **TC-LOAD-01** | Risk-04 | System | System stability under 110% of peak load | Load | P2 |
| **TC-STRESS-01** | Risk-05 | System | Data integrity check after forced service restart | Stress/Recovery | P1 |
| **TC-CAP-01** | Scalability | System | Identify max concurrent registration requests | Performance | P3 |
| **TC-SEC-08** | GDPR/PII | Integration | Sensitive data masking in Server/Console Logs | Security | P1 |
| **TC-SEC-09** | Security | System | Session timeout and automatic logout | Security | P2 |
| **TC-COMP-01** | Compatibility | System | Registration form rendering on mobile/desktop | Portability | P2 |
| **TC-REL-01** | Reliability | System | Error handling during network disconnect | Reliability | P2 |
| **TC-L10N-01** | Business | System | Support for international characters/date formats | L10n | P3 |
| **TC-REC-02** | Risk-06 | System | Successful data restoration from backup | Recovery | P1 |
| **TC-SEC-10** | Compliance | System | Audit logging for registration (Timestamp, IP) | Security | P2 |
| **TC-PRIV-02** | GDPR | System | "Right to be forgotten" (Full user data deletion) | Privacy | P2 |

---

