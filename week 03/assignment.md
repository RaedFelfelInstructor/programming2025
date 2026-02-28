# Week 3 – Assignment: Student Grade Report Generator

[← Back to Week 3 Overview](./README.md)

---

## 🎯 Project Brief

Build a **Student Grade Report Generator** — an interactive console program that collects student information and course scores, then generates a formatted report with grades, pass/fail status, and honor roll eligibility.

This project brings together everything from Week 3: comparison operators, logical operators, `if-else` chains, nested conditions, the ternary operator, and `switch` statements.

---

## Requirements

### Part 1 — Student Information

1. Ask for the student's name
2. Ask for their student ID
3. Ask for their program ("CS", "IT", "DS" for Computer Science, Information Technology, Data Science)
4. Use a `switch` statement or expression to display the full program name

### Part 2 — Course Scores

Ask the user to enter scores (0–100) for **four courses**:
1. Programming
2. Mathematics
3. English
4. Elective

For each score, validate that it is between 0 and 100. If the input is invalid, display a message and use a default score of 0.

### Part 3 — Grade Calculation

Convert each numeric score to a letter grade using an `else if` chain:

| Score Range | Letter Grade |
|-------------|-------------|
| 90 – 100 | A |
| 80 – 89 | B |
| 70 – 79 | C |
| 60 – 69 | D |
| 0 – 59 | F |

### Part 4 — Analysis

Calculate and determine:
1. **Average score** across all four courses
2. **Overall grade** (letter grade for the average)
3. **Pass/Fail status**: The student passes if **all** individual scores are 50 or above
4. **Honor roll**: The student is on the honor roll if the average is 85 or above **and** no individual score is below 70
5. **Highest and lowest scoring courses** (use nested conditions or comparisons)

### Part 5 — Report Display

Display a formatted report card that includes all the information above.

---

## Expected Output Example

```
╔══════════════════════════════════════════════╗
║          STUDENT GRADE REPORT                ║
╠══════════════════════════════════════════════╣

  Student Name:    Alice Johnson
  Student ID:      STU-2025-001
  Program:         Computer Science

╠══════════════════════════════════════════════╣
║              COURSE GRADES                   ║
╠══════════════════════════════════════════════╣

  Programming      92     A
  Mathematics      78     C
  English          85     B
  Elective         88     B

╠══════════════════════════════════════════════╣
║              SUMMARY                         ║
╠══════════════════════════════════════════════╣

  Average Score:   85.75
  Overall Grade:   B
  Status:          PASSED
  Honor Roll:      No (Mathematics below 70 threshold)
  Best Subject:    Programming (92)
  Weakest Subject: Mathematics (78)

╚══════════════════════════════════════════════╝
```

---

## Grading Criteria

| Criteria | Points |
|----------|--------|
| Program compiles and runs without errors | 10 |
| Correctly reads all user input | 10 |
| Uses `switch` for program name lookup | 10 |
| Validates score input (0–100 range) | 10 |
| Correctly calculates letter grades using `else if` | 15 |
| Correctly calculates average score | 10 |
| Correctly determines pass/fail status using logical operators | 10 |
| Correctly determines honor roll eligibility using combined conditions | 10 |
| Finds highest and lowest scoring courses | 10 |
| Clean, formatted output with clear labels | 5 |
| **Total** | **100** |

---

## Hints & Tips

- Declare your letter grade variables as `string` and assign them inside `if-else` chains
- For pass/fail, use `&&` to check that **all** scores meet the minimum
- For honor roll, combine the average check with a minimum score check using `&&`
- To find the highest score, compare pairs of values using nested conditions or a series of comparisons:
  ```csharp
  // One approach — compare step by step
  int highest = score1;
  if (score2 > highest) highest = score2;
  if (score3 > highest) highest = score3;
  if (score4 > highest) highest = score4;
  ```
- Use the ternary operator for simple status strings:
  ```csharp
  string status = passed ? "PASSED" : "FAILED";
  ```
- You can use `$"{score,5}"` to right-align numbers in your output (the `,5` means "pad to 5 characters")

---

## Bonus Challenges

1. **GPA Calculation:** Assign GPA points (A=4.0, B=3.0, C=2.0, D=1.0, F=0.0) and calculate the GPA
2. **Dean's List:** Add a Dean's List check — the student qualifies if their GPA is 3.5 or above
3. **Course Credits:** Ask for the credit hours of each course (e.g., Programming = 4 credits) and calculate a weighted average instead of a simple average
4. **Multiple Students:** After generating one report, ask "Generate another report? (yes/no)" and repeat if the user says yes (preview of Week 4 loops — try it if you are up for a challenge!)

---

[← Back to Week 3 Overview](./README.md)
