# Week 2 – Exercises

[← Back to Week 2 Overview](./README.md)

---

Practice exercises to reinforce the concepts from each lecture. Try to solve them on your own before looking at hints.

---

## Lecture 1 Exercises — Variables and Data Types

### Exercise 1.1 — Variable Declarations
Declare variables with appropriate types for each of the following, then print them all:

- Your full name
- Your age
- Your GPA (e.g., 3.75)
- The balance in your bank account (e.g., 1250.50)
- Whether you own a car (yes/no)
- Your first initial (single letter)
- The number of siblings you have

### Exercise 1.2 — Type Exploration
Write a program that declares one variable of each type (`int`, `double`, `decimal`, `float`, `char`, `string`, `bool`, `long`) and prints each one with a label. Example output:

```
int:     42
double:  3.14159
decimal: 19.99
float:   2.5
char:    A
string:  Hello, World!
bool:    True
long:    9876543210
```

### Exercise 1.3 — Constants in Action
Create a program that calculates the area and circumference of a circle. Declare `Pi` as a constant (`3.14159`). Ask the user for the radius, then display:

```
Radius:        5
Area:          78.54
Circumference: 31.42
```

> 💡 **Formulas:** Area = π × r² and Circumference = 2 × π × r. To square a number in C#, use `radius * radius` (we don't have an exponent operator).

### Exercise 1.4 — Swap Without a Temp Variable (Challenge)
You already know how to swap two variables using a third temporary variable. Can you swap two `int` variables using **only arithmetic** — no third variable?

> 💡 **Hint:** Think about addition and subtraction. If `a = 5` and `b = 10`, what does `a = a + b` give you?

---

## Lecture 2 Exercises — Type Conversion

### Exercise 2.1 — Conversion Experiments
Write a program that demonstrates each type of conversion. For each one, print the before and after values:

```csharp
// 1. Implicit: int → double
// 2. Explicit cast: double → int
// 3. Convert: double → int (show rounding vs truncation)
// 4. Parse: string → int
// 5. TryParse: string → int (test with valid and invalid input)
```

### Exercise 2.2 — Input Validator
Write a program that asks the user to enter:
1. Their age (must be a valid integer)
2. Their height in meters (must be a valid decimal number)

Use `TryParse` for both inputs. If either input is invalid, display a specific error message. If both are valid, display:

```
Age: 25 years
Height: 1.75 meters
```

### Exercise 2.3 — Precision Comparison
Write a program that demonstrates the precision difference between `float`, `double`, and `decimal`:

```csharp
float  f = 1.0f / 3.0f;
double d = 1.0 / 3.0;
decimal m = 1.0m / 3.0m;
```

Print each result and count how many decimal places each shows. Which is most precise?

### Exercise 2.4 — Casting Chain
Start with `double value = 9876.54321;` and perform the following conversions, printing the result at each step:

1. Cast to `int`
2. Cast the `int` to `short` (note: `short` holds values up to 32,767)
3. Convert the `short` to `string`
4. Parse the `string` back to `double`

How does the final `double` compare to the original?

---

## Lecture 3 Exercises — Operators and Expressions

### Exercise 3.1 — Integer Division Investigation
Write a program that asks the user for two integers and displays:
- Integer division result (`/`)
- Remainder (`%`)
- Decimal division result (cast to `double` first)

Example:
```
Enter first number: 17
Enter second number: 5
Integer division: 17 / 5 = 3
Remainder:        17 % 5 = 2
Decimal division:  17 / 5 = 3.40
```

### Exercise 3.2 — Time Converter
Ask the user for a total number of seconds (e.g., `3661`). Convert and display the equivalent hours, minutes, and remaining seconds.

**Example:**
```
Enter total seconds: 3661
That is: 1 hour(s), 1 minute(s), and 1 second(s)
```

> 💡 **Hint:** Use integer division (`/`) and modulus (`%`).
> - Hours = totalSeconds / 3600
> - Remaining = totalSeconds % 3600
> - Minutes = remaining / 60
> - Seconds = remaining % 60

### Exercise 3.3 — Money Breakdown
Write a program that asks for an amount of money (as an integer number of cents) and breaks it down into the fewest bills and coins.

**Example:**
```
Enter amount in cents: 2847
$20 bills: 1
$10 bills: 0
$5 bills:  1
$1 bills:  3
Quarters:  1
Dimes:     2
Nickels:   0
Pennies:   2
```

> 💡 **Hint:** Use `/` to find how many of each denomination, then `%` to find what's left.

### Exercise 3.4 — BMI Calculator with Formatting
Write a program that calculates Body Mass Index (BMI). Ask the user for their weight in kilograms and height in meters. Calculate and display the BMI formatted to 1 decimal place.

**Formula:** BMI = weight / (height × height)

```
Enter weight (kg): 70
Enter height (m): 1.75
Your BMI is: 22.9
```

### Exercise 3.5 — Formatted Student Report
Write a program that asks for a student's name and three test scores, then displays a formatted report:

```
╔══════════════════════════════╗
║     Student Report Card      ║
╠══════════════════════════════╣
║ Student: Alice Smith         ║
║ Test 1:  85                  ║
║ Test 2:  92                  ║
║ Test 3:  78                  ║
║ ─────────────────────────    ║
║ Average: 85.0                ║
║ Total:   255                 ║
╚══════════════════════════════╝
```

---

## Mixed Exercises (Combining All Lectures)

### Exercise M.1 — Unit Price Comparison
Write a program that helps a shopper compare two products. For each product, ask for the name, total price, and quantity. Calculate and display the unit price for each, formatted as currency, and indicate which is the better deal.

### Exercise M.2 — Paycheck Calculator
Ask the user for:
- Hourly wage
- Hours worked this week
- Tax rate (as a percentage)

Calculate and display:
- Gross pay
- Tax amount
- Net pay

Format all monetary values with currency formatting.

### Exercise M.3 — Distance Converter (Challenge)
Create a program that converts distances between metric and imperial. Ask the user for a distance in kilometers and display the equivalent in:
- Miles (1 km = 0.621371 miles)
- Feet (1 km = 3280.84 feet)
- Yards (1 km = 1093.61 yards)

Display all values formatted to 2 decimal places.

---

[← Back to Week 2 Overview](./README.md)
