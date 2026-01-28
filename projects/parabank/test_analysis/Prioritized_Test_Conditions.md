# 📋 Prioritized Test Conditions: User Registration
**Test Basis:** [SR001_ParaBank_Registration_Requirements.md](../static-testing/reviews/SR001_ParaBank_Registration_Requirements.md)  
**Technique:** Atomic Field Decomposition

---

## 👤 1. First & Last Name Fields
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-NAM-01** | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "First/Last Name is required" |
| **TC-NAM-02** | 1 Character (Min Boundary - 1) | BVA | P2 | Error message regarding minimum length |
| **TC-NAM-03** | 2 Characters (Min Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-04** | 50 Characters (Max Boundary) | BVA | P2 | Success - Data accepted |
| **TC-NAM-05** | 51 Characters (Max Boundary + 1) | BVA | P2 | Error or graceful truncation (Risk: Buffer Overflow) |
| **TC-NAM-06** | Special Chars: Hyphen `-` & Apostrophe `'` | L10n | P2 | Success (e.g., O'Donnell, Smith-Jones) |
| **TC-NAM-07** | Non-Latin Chars (UTF-8) | L10n | P3 | Success (Cyrillic, Diacritics, Hanzi) |
| **TC-NAM-08** | Numeric/Special Symbol Rejection | Validation | P2 | Error: Numbers/Symbols not allowed |
| **TC-NAM-09** | HTML/Script Tags Injection | Security | P2 | Tags are escaped or rejected (No XSS execution) |
| **TC-NAM-10** | Leading/Trailing Spaces | Integrity | P3 | Spaces are trimmed before DB persistence |

---

## 📮 2. Address & Location (Street, City, State)
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-ADR-01** | Alphanumeric & Symbols (`#`, `.`, `/`) | Functional | P2 | Success (e.g., Apt. #4, 1/2 St.) |
| **TC-ADR-02** | Address Line 2 Optionality | Business | P2 | Success when left blank |
| **TC-CTY-01** | Multi-word City Names | L10n | P2 | Success (e.g., New York, Los Angeles) |
| **TC-STA-01** | State: 2-letter ISO Code (NY, CA) | Validation | P2 | Success |
| **TC-STA-02** | State: Invalid length (1 or 3+ chars) | BVA | P2 | Error: "Use 2-letter state code" |

---

## 🔢 3. Zip Code
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-ZIP-01** | Numeric Only Validation | Validation | P1 | Error if letters/symbols are entered |
| **TC-ZIP-02** | Leading Zero Preservation (`00501`) | Integrity | P1 | **Critical:** Data stored as "00501", not "501" |
| **TC-ZIP-03** | 5-Digit Length (Standard US) | BVA | P1 | Success |
| **TC-ZIP-04** | 9-Digit Length (ZIP+4: `12345-6789`) | BVA | P2 | Success |

---
## 📱 4a. Phone Number
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-PHN-01** | Optionality Check (Empty field) | Business | P2 | Success - Registration completes without phone |
| **TC-PHN-02** | Numeric Only Validation | Validation | P2 | Error if letters are entered |
| **TC-PHN-03** | Minimum Length Boundary | BVA | P3 | Error regarding invalid phone length |
| **TC-PHN-04** | Maximum Length Boundary | BVA | P3 | Error or graceful truncation (Risk: Data Overflow) |
| **TC-PHN-05** | Special Chars Support (`+`, `-`, `( )`) | L10n | P3 | Success - Support for standard US or E.164 formats |
| **TC-PHN-06** | Meaningless Data Rejection (e.g., "0") | Data Quality | P3 | Error: "Please enter a valid phone number" |

---
## 🛡️ 5. Social Security Number (SSN)
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-SSN-01** | Empty Input (Mandatory Check) | Functional | P1 | Inline error: "Social Security Number is required" |
| **TC-SSN-02** | Numeric Only Validation | Validation | P1 | Error if letters or symbols (other than hyphens) are entered |
| **TC-SSN-03** | Exact Length (Boundary: 9 digits) | BVA | P1 | Success - Data accepted |
| **TC-SSN-04** | Invalid Length (< 9 or > 9 digits) | BVA | P1 | Error: "SSN must be 9 digits" |
| **TC-SSN-05** | UI Masking (Privacy) | Security | P1 | Input is masked as user types (●●●-●●-●●●●) |
| **TC-SSN-06** | Formatting Support (With/Without Hyphens) | L10n | P2 | Success for both `123456789` and `123-45-6789` |
| **TC-SSN-07** | Duplicate SSN Check | Logic | P1 | Error: "SSN already registered" (Banking KYC rule) |

## 🔑 6. Username Logic
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-USR-01** | Empty Input | Functional | P1 | Inline error: "Username is required" |
| **TC-USR-02** | Unique Username Check (Existing in DB) | Logic | P1 | Error: "This username already exists" |
| **TC-USR-03** | Case-Insensitivity Check (`Admin` vs `admin`) | Logic | P2 | Error: Duplicate detected (System should normalize case) |
| **TC-USR-04** | Minimum Length (Boundary: e.g., 4 chars) | BVA | P2 | Error if username is too short |
| **TC-USR-05** | Space Handling (No spaces allowed) | Validation | P2 | Error or automatic removal of spaces |
| **TC-USR-06** | Special Characters in Username | Security | P2 | Rejection of dangerous symbols (SQLi risk) |

## 🔐 7. Password & Confirmation
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-01** | Empty Password Input | Functional | P1 | Inline error: "Password is required" |
| **TC-PWD-02** | Empty Confirm Input | Functional | P1 | Inline error: "Please confirm your password" |
| **TC-PWD-03** | Password & Confirm Match | Logic | P1 | Error if values differ |
| **TC-PWD-04** | UI Masking (Security) | Security | P1 | All characters masked in both fields (●●●●●) |
| **TC-PWD-05** | Complexity: Minimum Length | BVA | P2 | Error if below system minimum (e.g., 8 chars) |
| **TC-PWD-06** | Complexity: Character Types (A-z, 0-9, !@#) | Security | P2 | Validation of password strength rules |
| **TC-PWD-07** | Copy-Paste Limitation | Security | P3 | (Optional) Prevention of pasting into "Confirm" field |
| **TC-PWD-08** | SQL Injection in Password | Security | P2 | Input is sanitized/hashed, not executed |

---
## 🛡️ 8. Business Integrity & Identity (Cross-Field Logic)
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-INT-01** | Duplicate SSN Check | Business | P1 | System blocks registration if SSN exists in DB |
| **TC-INT-02** | Duplicate Phone Check | Business | P2 | System flags or blocks if Phone exists |
| **TC-INT-03** | Conflict: Same SSN, Different Username | Business | P1 | Hard block: Identity must be unique (1 SSN = 1 User) |
| **TC-INT-04** | Conflict: Same Phone, Different SSN | Business | P2 | Verification required (Risk: Multiple users per phone) |

## 🔐 9. Password Strength Conditions
| ID | Test Condition (Atomic Check) | Category | Priority | Expected Behavior |
| :--- | :--- | :--- | :--- | :--- |
| **TC-PWD-09** | Low Strength: < 8 chars or only letters | Security | P3 | Warning/Rejection: "Weak password" |
| **TC-PWD-10** | Medium Strength: 8+ chars, mixed case + numbers | Security | P2 | Success: "Medium password" |
| **TC-PWD-11** | Strong Strength: 10+ chars, mixed case, numbers, special symbols | Security | P1 | Success: "Strong password" |

---
