# Week 2 – Assignment: Personal Finance Calculator

[← Back to Week 2 Overview](./README.md)

---

## 📋 Assignment Overview

| Item       | Detail                                          |
| ---------- | ----------------------------------------------- |
| Topic      | Variables, data types, conversion, operators     |
| Type       | Mini-project (individual)                        |
| Difficulty | ⭐⭐ Beginner                                   |

---

## 🎯 Objective

Build a **Personal Finance Calculator** — a console application that helps a user understand their monthly finances by calculating income, expenses, savings, and financial health indicators.

This project brings together everything from Week 2: variable declarations, choosing appropriate data types, type conversion from user input, arithmetic operations, and formatted output.

---

## 📝 Requirements

### Part 1 — Income Input

Ask the user for the following information:
- Monthly salary (before tax)
- Tax rate as a percentage (e.g., `22` for 22%)
- Any additional monthly income (freelance, side jobs, etc.)

Calculate:
- Tax amount
- Net salary (salary after tax)
- Total monthly income (net salary + additional income)

### Part 2 — Expense Input

Ask the user for their monthly expenses in these categories:
- Rent / Housing
- Utilities (electricity, water, internet)
- Groceries / Food
- Transportation
- Entertainment / Subscriptions

Calculate:
- Total monthly expenses

### Part 3 — Financial Summary

Calculate and display:
- **Monthly savings** = Total income − Total expenses
- **Savings rate** = (Monthly savings / Total income) × 100
- **Daily budget** = Monthly savings / 30 (how much they can spend per day beyond expenses)

### Part 4 — Formatted Output

Display a clean, formatted financial report. Use string interpolation with format specifiers for all monetary values (`:C`) and percentages (`:F1` or `:P`).

---

## 💻 Expected Output

Here's an example of what a completed program should look like:

```
╔══════════════════════════════════════╗
║     Personal Finance Calculator      ║
╚══════════════════════════════════════╝

--- Income ---
Enter your monthly salary: $5000
Enter your tax rate (%): 22
Enter additional monthly income: $500

--- Expenses ---
Enter rent/housing cost: $1200
Enter utilities cost: $150
Enter groceries/food cost: $400
Enter transportation cost: $200
Enter entertainment cost: $100

══════════════════════════════════════
         FINANCIAL SUMMARY
══════════════════════════════════════

  INCOME
  Gross Salary:      $5,000.00
  Tax (22%):        -$1,100.00
  Net Salary:        $3,900.00
  Additional Income:   $500.00
  ─────────────────────────────
  Total Income:      $4,400.00

  EXPENSES
  Rent/Housing:      $1,200.00
  Utilities:           $150.00
  Groceries:           $400.00
  Transportation:      $200.00
  Entertainment:       $100.00
  ─────────────────────────────
  Total Expenses:    $2,050.00

  SAVINGS
  Monthly Savings:   $2,350.00
  Savings Rate:       53.4%
  Daily Budget:        $78.33

══════════════════════════════════════
```

---

## 🔍 Hints

1. **Choose the right types:** Use `decimal` for all monetary values (why?) and `double` or `int` for percentages.

2. **Reading numeric input:** Remember that `Console.ReadLine()` returns a string. Use `decimal.Parse()` or `double.Parse()` to convert.

3. **Calculating percentages:**
   ```csharp
   decimal taxRate = 22;  // user enters 22
   decimal taxAmount = salary * (taxRate / 100);
   ```

4. **Formatting currency:** Use `:C` in string interpolation:
   ```csharp
   Console.WriteLine($"Total: {total:C}");  // displays as $1,234.56
   ```

5. **Formatting percentages manually:** If your savings rate is a number like `53.4`, display it with:
   ```csharp
   Console.WriteLine($"Savings Rate: {savingsRate:F1}%");
   ```

6. **Alignment in output:** You can use alignment with interpolation to line up columns:
   ```csharp
   Console.WriteLine($"{"Rent:",-18} {rent,10:C}");
   // "Rent:              $1,200.00"
   ```
   The `,−18` means left-align in 18 characters. The `,10` means right-align in 10 characters.

---

## ⭐ Bonus Challenges

If you finish early, try adding these features:

1. **Annual projection:** Display the yearly totals (income × 12, expenses × 12, savings × 12).

2. **Savings goal:** Ask the user for a savings goal (e.g., $10,000) and calculate how many months it will take to reach it at their current savings rate.

3. **Expense breakdown:** Show what percentage of total income each expense category represents.

4. **Input validation:** Use `TryParse` instead of `Parse` to handle invalid input gracefully — if the user enters non-numeric text, display an error message and use a default value of `0`.

---

## ✅ Submission Checklist

Before submitting, make sure:

- [ ] Program compiles and runs without errors
- [ ] All monetary values use `decimal` type
- [ ] User input is read and converted correctly
- [ ] All calculations are correct (tax, totals, savings rate)
- [ ] Output is formatted with currency symbols and aligned columns
- [ ] Code uses meaningful variable names (not `x`, `y`, `z`)
- [ ] Code includes comments explaining each section

---

## 📐 Grading Criteria

| Criteria | Weight |
|----------|--------|
| Correct variable types and declarations | 20% |
| Correct type conversion from user input | 15% |
| Correct arithmetic calculations | 25% |
| Formatted output with string interpolation | 25% |
| Code quality (naming, comments, organization) | 15% |

---

[← Back to Week 2 Overview](./README.md)
