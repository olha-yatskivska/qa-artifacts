# 📋 Prioritized Test Conditions: User Registration

**Test Basis:** [SR001_ParaBank_Registration_Requirements.md](../static-testing/reviews/SR001_ParaBank_Registration_Requirements.md)  
**Technique:** Atomic Field Decomposition

---

## 👤 1. First & Last Name Fields
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-NAM-01** | SR001.1 | System | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "First/Last Name is required" |
| **TC-NAM-02** | SR001.1 | Unit | 1 Character (Min Boundary - 1) | BVA | P2 | Error message regarding minimum length |
| **TC-NAM-03** | SR001.1 | Unit | 2 Characters (Min Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-04** | SR001.1 | Unit | 50 Characters (Max Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-05** | SR001.1 | System | 51 Characters (Max Boundary + 1) | BVA | P2 | Error or graceful truncation (Risk: Buffer Overflow) |
| **TC-NAM-06** | SR001.1 | System | Special Chars: Hyphen `-` & Apostrophe `'` | L10n | P2 | Success (e.g., O'Donnell, Smith-Jones) |
| **TC-NAM-07** | SR001.1 | System | Non-Latin Chars (UTF-8) | L10n | P3 | Success (Cyrillic, Diacritics, Hanzi) |
| **TC-NAM-08** | SR001.1 | System | Numeric/Special Symbol Rejection | Validation | P2 | Error: Numbers/Symbols not allowed |
| **TC-NAM-09** | SR001.1 | System | HTML/Script Tags Injection | Security | P2 | Tags are escaped or rejected (No XSS execution) |
| **TC-NAM-10** | SR001.1 | Integration | Leading/Trailing Spaces | Integrity | P3 | Spaces are trimmed before DB persistence |

---

## 📮 2. Address & Location (Street, City, State)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ADR-01** | SR001.2 | System | Alphanumeric & Symbols (`#`, `.`, `/`) | Functional | P2 | Success (e.g., Apt. #4, 1/2 St.) |
| **TC-ADR-02** | SR001.2 | System | Address Line 2 Optionality | Business | P2 | Success when left blank |
| **TC-CTY-01** | SR001.2 | System | Multi-word City Names | L10n | P2 | Success (e.g., New York, Los Angeles) |
| **TC-STA-01** | SR001.2 | System | State: 2-letter ISO Code (NY, CA) | Validation | P2 | Success |
| **TC-STA-02** | SR001.2 | Unit | State: Invalid length (1 or 3+ chars) | BVA | P2 | Error: "Use 2-letter state code" |

---

## 🔢 3. Zip Code
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ZIP-01** | SR001.3 | System | Numeric Only Validation | Validation | P1 | Error if letters/symbols are entered |
| **TC-ZIP-02** | SR001.3 | Integration | Leading Zero Preservation (`00501`) | Integrity | P1 | **Critical:** Data stored as "00501", not "501" |
| **TC-ZIP-03** | SR001.3 | Unit | 5-Digit Length (Standard US) | BVA | P1 | Success |
| **TC-ZIP-04** | SR001.3 | Unit | 9-Digit Length (ZIP+4: `12345-6789`) | BVA | P2 | Success |

---

## 📱 4a. Phone Number
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PHN-01** | SR001.4 | System | Optionality Check (Empty field) | Business | P2 | Success - Registration completes |
| **TC-PHN-02** | SR001.4 | Unit | Numeric Only Validation | Validation | P2 | Error if letters are entered |
| **TC-PHN-03** | SR001.4 | Unit | Minimum Length Boundary | BVA | P3 | Error regarding invalid phone length |
| **TC-PHN-04** | SR001.4 | Unit | Maximum Length Boundary | BVA | P3 | Error or graceful truncation |
| **TC-PHN-05** | SR001.4 | System | Special Chars Support (`+`, `-`, `( )`) | L10n | P3 | Success - Support for standard formats |
| **TC-PHN-06** | SR001.4 | Integration | Meaningless Data Rejection (e.g., "0") | Data Quality | P3 | Error: "Please enter a valid phone number" |

---

## 🛡️ 5. Social Security Number (SSN)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-SSN-01** | SR001.5 | System | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "SSN is required" |
| **TC-SSN-02** | SR001.5 | Unit | Numeric Only Validation | Validation | P1 | Error if letters or symbols |
| **TC-SSN-03** | SR001.5 | Unit | Exact Length (Boundary: 9 digits) | BVA | P1 | Success - Data accepted |
| **TC-SSN-04** | SR001.5 | Unit | Invalid Length (< 9 or > 9 digits) | BVA | P1 | Error: "SSN must be 9 digits" |
| **TC-SSN-05** | SR001.5 | System | UI Masking (Privacy) | Security | P1 | Input is masked as user types |
| **TC-SSN-06** | SR001.5 | System | Formatting Support (With/Without Hyphens) | L10n | P2 | Success for both formats |
| **TC-SSN-07** | SR001.5 | Integration | Duplicate SSN Check | Logic | P1 | Error: "SSN already registered" |

---

## 🔑 6. Username Logic
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-USR-01** | SR001.6 | System | Empty Input | Functional | P1 | Inline error: "Username is required" |
| **TC-USR-02** | SR001.6 | Integration | Unique Username Check (DB) | Logic | P1 | Error: "This username already exists" |
| **TC-USR-03** | SR001.6 | Integration | Case-Insensitivity Check | Logic | P2 | Error: Duplicate detected |
| **TC-USR-04** | SR001.6 | Unit | Minimum Length (Boundary: 4 chars) | BVA | P2 | Error if username is too short |
| **TC-USR-05** | SR001.6 | System | Space Handling (No spaces allowed) | Validation | P2 | Error or automatic removal |
| **TC-USR-06** | SR001.6 | System | Special Characters in Username | Security | P2 | Rejection of dangerous symbols (SQLi) |

---

## 🔐 7. Password & Confirmation
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-01** | SR001.7 | System | Empty Password Input | Functional | P1 | Inline error: "Password is required" |
| **TC-PWD-02** | SR001.7 | System | Empty Confirm Input | Functional | P1 | Inline error: "Please confirm password" |
| **TC-PWD-03** | SR001.7 | System | Password & Confirm Match | Logic | P1 | Error if values differ |
| **TC-PWD-04** | SR001.7 | System | UI Masking (Security) | Security | P1 | All characters masked (●●●●●) |
| **TC-PWD-05** | SR001.7 | Unit | Complexity: Minimum Length | BVA | P2 | Error if below minimum |
| **TC-PWD-06** | SR001.7 | Unit | Complexity: Character Types | Security | P2 | Validation of password strength rules |
| **TC-PWD-07** | SR001.7 | System | Copy-Paste Limitation | Security | P3 | (Optional) Prevention of pasting |
| **TC-PWD-08** | SR001.7 | System | SQL Injection in Password | Security | P2 | Input is sanitized/hashed |

---

## 🛡️ 8. Business Integrity & Identity (Cross-Field Logic)
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-INT-01** | SR001.8 | Integration | Duplicate SSN Check | Business | P1 | System blocks registration |
| **TC-INT-02** | SR001.8 | Integration | Duplicate Phone Check | Business | P2 | System flags or blocks if Phone exists |
| **TC-INT-03** | SR001.8 | Integration | Conflict: Same SSN, Diff Username | Business | P1 | Hard block: 1 SSN = 1 User |
| **TC-INT-04** | SR001.8 | Integration | Conflict: Same Phone, Diff SSN | Business | P2 | Verification required |

---

## 🔐 9. Password Strength Conditions
| ID | Traceability | Test Level | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-09** | SR001.7 | Unit | Low Strength: < 8 chars | Security | P3 | Warning/Rejection |
| **TC-PWD-10** | SR001.7 | Unit | Medium Strength | Security | P2 | Success: "Medium password" |
| **TC-PWD-11** | SR001.7 | Unit | Strong Strength | Security | P1 | Success: "Strong password" |

---

