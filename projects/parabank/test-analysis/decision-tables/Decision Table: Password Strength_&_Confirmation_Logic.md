**ID:** DT-02  
**Scope:** Validation of password complexity levels and matching logic to ensure account security and optimal UX during registration.

| Conditions | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Passwords Match?** | No | Yes | Yes | Yes | Yes |
| **Complexity Level** | Any | Invalid/Too Short | Weak | Medium | Strong |
| **Actions** | | | | | |
| **Show "Mismatch" Error** | X | | | | |
| **Indicator Color** | Gray | Red | Orange | Yellow | Green |
| **Show Complexity Warning** | | X (Short) | X (Weak) | X (Medium) | |
| **Submit Button State** | Disabled | Disabled | Disabled | **Enabled** | **Enabled** |
| **Account Creation Allowed** | No | No | No | Yes | Yes |

