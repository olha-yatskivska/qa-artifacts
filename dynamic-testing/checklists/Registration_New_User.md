# 🏦 Test Design Checklist: ParaBank User Registration
**Techniques Applied:** Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Error Guessing.

---

## 🏗 1. Master Validation Grid (Data Integrity & Localization)



| Field | Technical EP / BVA Scenarios | US Market & Localization (L10n) | Business Intelligence (BI) Impact |
| :--- | :--- | :--- | :--- |
| **First/Last Name** | • **BVA:** 1, 2, 50, 51 chars.<br>• **EP:** Latin, Cyrillic, Hyphens, Apostrophes. | **Standard:** O'Donnell, Smith-Jones.<br>**Global:** UTF-8 support (Cyrillic, Hanzi). | **Trimming:** Leading/trailing spaces must be stripped before DB entry. |
| **Date of Birth** | • **EP:** <18, 18, 100+ years.<br>• **Leap Year:** Feb 29th logic.<br>• **BVA:** Current Date + 1 (Future). | **Format:** MM/DD/YYYY (US Standard). | **Age Logic:** Verification of "18+ only" banking policy. |
| **Street Address** | • **BVA:** 5 to 200 chars.<br>• **EP:** Alphanumeric, `#`, `/`, `.`. | **US:** 123 Main St, Apt 4B. P.O. Boxes. | **Normalization:** Atomic storage (Line 1 vs Line 2) for heatmap analytics. |
| **City** | • **EP:** Valid names, names with spaces/hyphens. | **US:** New York, Winston-Salem. | **Standardization:** Check if input matches a verified city database. |
| **State** | • **EP:** Dropdown selection vs manual input. | **US:** 2-letter ISO codes (NY, CA, TX). | **Reporting:** ISO codes are critical for tax and regional reporting. |
| **Zip Code** | • **BVA:** 5 digits vs 9 digits (ZIP+4).<br>• **EP:** Numeric only. | **US:** 12345 or 12345-6789. | **Leading Zeros:** `00501` must stay `00501` (Stored as STRING, not INT). |
| **Phone Number** | • **BVA:** 7, 10, 15 digits.<br>• **EP:** `+`, `( )`, `-`, spaces. | **Standard:** E.164 (International format). | **Cleanliness:** Save raw digits (`1555...`) for CRM/SMS marketing. |
| **SSN** | • **BVA:** Exactly 9 digits.<br>• **EP:** Numeric only. | **US:** Social Security Number (Required for KYC). | **Security:** Encryption at rest (PII). UI masking: `XXX-XX-1234`. |
| **Email Address** | • **BVA:** Max 254 chars (RFC 5322).<br>• **EP:** `prefix@domain.com`, `+alias`. | **Consistency:** Case-insensitive check (User@ = user@). | **Uniqueness:** One email = One Customer Profile. |

---

## 🛡 2. Security & Edge Cases 



### 2.1 Injection Attacks
* [ ] **SQL Injection:** Input `' OR 1=1 --` into Name/Address fields. (Expected: Error or sanitized string).
* [ ] **XSS (Cross-Site Scripting):** Input `<script>alert(1)</script>` into City field. (Expected: String is escaped, no popup).
* [ ] **HTML Injection:** Input `<b>Test</b>` (Expected: No bold text in profile view).

### 2.2 Data Integrity (Legacy & Technical)
* [ ] **Unix Epoch Check:** Set DOB to `01/01/1970`.
* [ ] **Pre-1970 Check:** Set DOB to `01/01/1890` (Common crash point for old DB types).
* [ ] **2038 Problem:** Check if system accepts dates beyond 2038 (32-bit limit).

---

