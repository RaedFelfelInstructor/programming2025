# Week 1 – Assignment: Trip Cost Calculator

[← Back to Week 1 Overview](./README.md)

---

## Overview

Build an interactive **Trip Cost Calculator** — a console program that asks the user about a planned trip and calculates the estimated total cost. This assignment brings together everything from Week 1: output, input, type conversion, string interpolation, and comments.

---

## Requirements

Your program must:

1. Display a welcome header
2. Ask the user for the following information:
   - Destination (text)
   - Number of days (whole number)
   - Hotel cost per night in dollars (whole number)
   - Estimated food cost per day in dollars (whole number)
3. Calculate:
   - Total hotel cost = days × cost per night
   - Total food cost = days × food cost per day
   - Overall total cost = hotel total + food total
4. Display the results in a clear, formatted summary
5. Include **at least 3 comments** explaining parts of your code

---

## Example Output

```
╔═══════════════════════════════════╗
║      TRIP COST CALCULATOR         ║
╚═══════════════════════════════════╝

Where are you traveling to? Paris
How many days? 5
Hotel cost per night ($)? 120
Food budget per day ($)? 45

───── Trip Summary ─────────────────
Destination:    Paris
Duration:       5 days
Hotel total:    $600
Food total:     $225
─────────────────────────────────────
TOTAL COST:     $825
─────────────────────────────────────
Have a great trip to Paris!
```

---

## Starter Template

If you need help getting started, here is a skeleton:

```csharp
// Trip Cost Calculator
// Week 1 - Assignment

// Display welcome header
Console.WriteLine("=== Trip Cost Calculator ===");
Console.WriteLine();

// Get destination
Console.Write("Where are you traveling to? ");
string destination = Console.ReadLine();

// Get number of days
Console.Write("How many days? ");
int days = int.Parse(Console.ReadLine());

// TODO: Ask for hotel cost per night

// TODO: Ask for food cost per day

// TODO: Calculate totals

// TODO: Display the summary using string interpolation
```

---

## Grading Criteria

| Criteria | Points |
|----------|--------|
| Program compiles and runs without errors | 20 |
| Correctly reads all 4 inputs from the user | 20 |
| Correctly calculates hotel total, food total, and overall total | 25 |
| Displays a clear, formatted summary using string interpolation | 20 |
| Code includes at least 3 meaningful comments | 10 |
| Code is clean and readable | 5 |
| **Total** | **100** |

---

## Bonus Challenges

If you finish early, try extending your program. These are optional and will not affect your grade, but they are excellent practice.

### Bonus 1 — Transport Cost
Add a one-time transport cost (flights, train, etc.) and include it in the total.

### Bonus 2 — Daily Spending Money
Add a daily spending/entertainment budget and include it in the calculations.

### Bonus 3 — Cost Per Day
Calculate and display the **average cost per day** (total ÷ days).

### Bonus 4 — Fancy Formatting
Make your output look polished with box-drawing characters, alignment, and spacing. See the example output above for inspiration.

---

## Submission

Submit your `Program.cs` file. Make sure:
- Your program runs without errors
- You have tested it with at least two different sets of input
- Your comments are meaningful (not just "this prints a line")

---

## Tips

- Use `Console.Write()` (not `WriteLine`) for prompts so the user types on the same line
- Use `int.Parse(Console.ReadLine())` to read whole numbers
- Use string interpolation (`$"text {variable}"`) for the summary
- Test with different numbers to make sure your calculations are correct
- Read through your code one more time before submitting — pretend you're seeing it for the first time

---

[← Back to Week 1 Overview](./README.md)
