## 1. Password Strength Checker

### Description

Checks how strong a password is by examining it character-by-character using **string manipulation functions** — no external libraries or regex involved. The password is scored out of 5 based on five criteria, mapped to a strength label, and returned with detailed pass/fail feedback for each rule.

### Flowchart

```mermaid
flowchart TD
    A([Start]) --> B[/Input Password/]
    B --> C{Password Empty?}
    C -- Yes --> B
    C -- No --> D[Set Score = 0]
    D --> E{Length >= 8 ?}
    E -- Yes --> E1[Score += 1]
    E -- No --> F
    E1 --> F{Has Uppercase Letter?}
    F -- Yes --> F1[Score += 1]
    F -- No --> G
    F1 --> G{Has Lowercase Letter?}
    G -- Yes --> G1[Score += 1]
    G -- No --> H
    G1 --> H{Has Digit?}
    H -- Yes --> H1[Score += 1]
    H -- No --> I
    H1 --> I{Has Special Character?}
    I -- Yes --> I1[Score += 1]
    I -- No --> J
    I1 --> J{Is Common Password?}
    J -- Yes --> J1[Label = Very Weak]
    J -- No --> J2[Label = Map Score to Label]
    J1 --> K[/Display Strength and Feedback/]
    J2 --> K
    K --> L{Check Another Password?}
    L -- Yes --> B
    L -- No --> M([End])
```

### Algorithm

1. **Start**
2. Prompt the user to input a password.
3. If the input is empty, display an error and return to Step 2.
4. Initialize `score = 0`.
5. Check length: if `len(password) >= 8`, increment `score` by 1.
6. Check for at least one uppercase letter using `isupper()`; if present, increment `score`.
7. Check for at least one lowercase letter using `islower()`; if present, increment `score`.
8. Check for at least one digit using `isdigit()`; if present, increment `score`.
9. Check for at least one special character (from a predefined set) using the `in` operator; if present, increment `score`.
10. Compare the password, converted to lowercase, against a list of common weak passwords.
11. Assign a strength label:
    - If it matches a common password → `Very Weak (Common Password)`
    - Otherwise map the score → `0–1: Very Weak`, `2: Weak`, `3: Moderate`, `4: Strong`, `5: Very Strong`
12. Display the strength label, the numeric score (`X/5`), and a checklist (OK/X) showing which criteria were met.
13. Ask the user whether they want to check another password.
14. If yes, repeat from Step 2; otherwise terminate the loop.
15. **Stop**

### Features

- Pure string manipulation — no `re` module used
- Score-based strength rating out of 5
- Checks the password against a list of common weak passwords
- Detailed OK/X feedback showing exactly which rule is missing
- Keeps running until the user types `exit`

### Sample Output

```
Enter a password to check (or 'exit' to quit): P@ssw0rd123

Password Strength: Very Strong  (Score: 5/5)

----- Detailed Feedback -----
[OK] At least 8 characters long
[OK] Contains an uppercase letter (A-Z)
[OK] Contains a lowercase letter (a-z)
[OK] Contains a digit (0-9)
[OK] Contains a special character (!@#$ etc.)
```

---
## Author

RAJIB MALDAS

BWU/BTS/25/032
