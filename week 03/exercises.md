# Week 3 – Exercises

[← Back to Week 3 Overview](./README.md)

---

These exercises reinforce the concepts from all three lectures. Work through them in order — they build on each other. Try to solve each one before looking at the hints.

---

## Section A: Comparison & Logical Operators

### Exercise 1 — Number Classifier
Ask the user for a number. Display whether it is:
- Positive, negative, or zero
- Even or odd

**Example output:**
```
Enter a number: -8
-8 is negative.
-8 is even.
```

> 💡 **Hint:** Use `number % 2 == 0` to check even. Use separate `if-else` blocks for each classification.

---

### Exercise 2 — Leap Year Checker
Ask the user for a year. Determine if it is a leap year.

A year is a leap year if:
- It is divisible by 4 **AND**
- It is NOT divisible by 100 **OR** it IS divisible by 400

**Example outputs:**
```
Enter a year: 2024
2024 is a leap year.
```
```
Enter a year: 1900
1900 is NOT a leap year.
```
```
Enter a year: 2000
2000 is a leap year.
```

> 💡 **Hint:** The formula in C# is: `(year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)`

---

### Exercise 3 — Triangle Validator
Ask the user for three side lengths. Determine if they can form a valid triangle.

A triangle is valid if the sum of any two sides is greater than the third side.

**Example outputs:**
```
Enter side 1: 3
Enter side 2: 4
Enter side 3: 5
Valid triangle!
```
```
Enter side 1: 1
Enter side 2: 2
Enter side 3: 10
Not a valid triangle.
```

> 💡 **Hint:** You need to check all three combinations: `a + b > c && a + c > b && b + c > a`

---

## Section B: if, else if, and Nested Conditions

### Exercise 4 — BMI Calculator
Ask the user for their weight (in kg) and height (in meters). Calculate their BMI and display the category.

**Formula:** `BMI = weight / (height * height)`

| BMI Range | Category |
|-----------|----------|
| Below 18.5 | Underweight |
| 18.5 – 24.9 | Normal weight |
| 25.0 – 29.9 | Overweight |
| 30.0 and above | Obese |

**Example output:**
```
Enter your weight (kg): 70
Enter your height (meters): 1.75
Your BMI is 22.86 — Normal weight.
```

---

### Exercise 5 — Electricity Bill Calculator
Ask the user for the number of kilowatt-hours (kWh) consumed. Calculate the bill using tiered pricing:

| Usage (kWh) | Rate per kWh |
|-------------|--------------|
| First 100 | $0.10 |
| Next 200 (101–300) | $0.15 |
| Above 300 | $0.25 |

**Example:** If usage is 350 kWh:
- First 100 kWh: 100 × $0.10 = $10.00
- Next 200 kWh: 200 × $0.15 = $30.00
- Remaining 50 kWh: 50 × $0.25 = $12.50
- Total: $52.50

> 💡 **Hint:** This is a nested problem. Check if usage is above 300 first, then above 100, then handle the rest.

---

### Exercise 6 — Password Strength Checker
Ask the user to enter a password. Check its strength based on length:

| Length | Strength |
|--------|----------|
| Less than 6 | Weak |
| 6 to 9 | Medium |
| 10 to 14 | Strong |
| 15 or more | Very Strong |

Also check if the password contains at least one digit. If it does, add " (contains number)" to the output.

**Example outputs:**
```
Enter a password: hi
Strength: Weak
```
```
Enter a password: MyPassword1
Strength: Strong (contains number)
```

> 💡 **Hint:** To check if a string contains a digit, you can loop through the characters (preview of Week 4) or use `password.Any(char.IsDigit)` — but for now, a simpler approach is `password.Contains("0") || password.Contains("1") || ...` or check the string against each digit character.

---

## Section C: Ternary Operator

### Exercise 7 — Min and Max
Ask the user for two numbers. Use the ternary operator to find and display the minimum and maximum.

**Example output:**
```
Enter first number: 15
Enter second number: 8
Minimum: 8
Maximum: 15
```

---

### Exercise 8 — Pluralization
Ask the user for an item name and a quantity. Display the quantity and item, using correct singular/plural form.

**Example outputs:**
```
Enter item name: apple
Enter quantity: 1
You have 1 apple.
```
```
Enter item name: apple
Enter quantity: 5
You have 5 apples.
```

> 💡 **Hint:** Use the ternary operator inside string interpolation: `$"You have {qty} {item}{(qty == 1 ? "" : "s")}."`

---

## Section D: Switch Statements

### Exercise 9 — Simple Calculator (Switch)
Build a calculator that asks for two numbers and an operation. Use a `switch` statement to perform the calculation.

Supported operations: `add`, `subtract`, `multiply`, `divide`

Handle division by zero and unknown operations.

**Example output:**
```
Enter first number: 20
Enter second number: 4
Enter operation (add/subtract/multiply/divide): divide
20 / 4 = 5
```

---

### Exercise 10 — Roman Numeral Converter
Ask the user for a number between 1 and 10. Use a `switch` expression to convert it to a Roman numeral and display the result.

| Number | Roman |
|--------|-------|
| 1 | I |
| 2 | II |
| 3 | III |
| 4 | IV |
| 5 | V |
| 6 | VI |
| 7 | VII |
| 8 | VIII |
| 9 | IX |
| 10 | X |

---

### Exercise 11 — Day Planner
Ask the user for a day of the week (as text: "Monday", "Tuesday", etc.). Use a `switch` statement to display a schedule:

- Monday, Wednesday, Friday → "Gym day! Workout at 6 PM."
- Tuesday, Thursday → "Study group at 5 PM."
- Saturday → "Free day — relax!"
- Sunday → "Meal prep for the week."
- Anything else → "Invalid day."

Use grouped cases where appropriate.

---

## Section E: Combined Challenges

### Exercise 12 — Tax Calculator
Ask the user for their annual income. Calculate the tax using progressive brackets:

| Income Range | Tax Rate |
|-------------|----------|
| $0 – $10,000 | 0% |
| $10,001 – $40,000 | 10% |
| $40,001 – $85,000 | 20% |
| Above $85,000 | 30% |

The rates are **progressive** — meaning only the portion within each bracket is taxed at that rate (similar to the electricity bill in Exercise 5).

**Example:** Income of $50,000:
- First $10,000: $0
- Next $30,000 (10,001–40,000): $3,000
- Next $10,000 (40,001–50,000): $2,000
- Total tax: $5,000

---

### Exercise 13 — Zodiac Sign Finder
Ask the user for their birth month and day. Determine their zodiac sign using the following dates:

| Sign | Date Range |
|------|-----------|
| Capricorn | Dec 22 – Jan 19 |
| Aquarius | Jan 20 – Feb 18 |
| Pisces | Feb 19 – Mar 20 |
| Aries | Mar 21 – Apr 19 |
| Taurus | Apr 20 – May 20 |
| Gemini | May 21 – Jun 20 |
| Cancer | Jun 21 – Jul 22 |
| Leo | Jul 23 – Aug 22 |
| Virgo | Aug 23 – Sep 22 |
| Libra | Sep 23 – Oct 22 |
| Scorpio | Oct 23 – Nov 21 |
| Sagittarius | Nov 22 – Dec 21 |

> 💡 **Hint:** Use a combination of `switch` on the month and `if-else` on the day within each case. Alternatively, use `else if` chains with combined conditions.

---

## Bonus Challenge

### Exercise 14 — Rock, Paper, Scissors (vs Computer)
Build a Rock, Paper, Scissors game where the user plays against the computer.

Requirements:
1. Ask the user to enter "rock", "paper", or "scissors"
2. The computer always picks "rock" for now (we will add randomness in a later week)
3. Determine the winner using conditions
4. Display the result: Win, Lose, or Draw

**Example output:**
```
Enter your choice (rock/paper/scissors): paper
You chose: paper
Computer chose: rock
You win! Paper covers rock.
```

> 💡 **Hint:** Use a `switch` on the user's choice and `if-else` inside each case to compare with the computer's choice, or use a series of conditions with `&&`.

---

[← Back to Week 3 Overview](./README.md)
