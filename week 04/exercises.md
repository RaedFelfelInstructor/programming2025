# Week 4 – Exercises

[← Back to Week 4 Overview](./README.md)

---

These exercises cover all the loop concepts from this week. Work through them in order — they build on each other. Try each exercise on your own before looking at hints.

---

## Section 1: `while` and `do-while` Loops

### Exercise 1 — Count to N
Ask the user for a positive number `n`. Use a `while` loop to print all numbers from 1 to `n`.

**Example:**
```
Enter a number: 6
1 2 3 4 5 6
```

### Exercise 2 — Sum Until Zero
Keep asking the user for numbers. When they enter `0`, stop and display the total sum of all numbers entered.

**Example:**
```
Enter a number: 10
Enter a number: 25
Enter a number: 5
Enter a number: 0
Total: 40
```

### Exercise 3 — Guess the Magic Number
Set a "magic number" in your code (e.g., `int magic = 42;`). Use a `do-while` loop to keep asking the user to guess. After each wrong guess, tell them if the magic number is higher or lower. Display how many attempts it took.

**Example:**
```
Guess the number: 50
Too high!
Guess the number: 30
Too low!
Guess the number: 42
Correct! You got it in 3 attempts.
```

### Exercise 4 — Input Validation
Ask the user for a test score between 0 and 100. Use a `do-while` loop to keep asking until they enter a valid score. Then display the corresponding letter grade (A: 90+, B: 80–89, C: 70–79, D: 60–69, F: below 60).

### Exercise 5 — Powers of 2
Use a `while` loop to print all powers of 2 that are less than 1000. Start with 1 and keep doubling.

**Expected output:**
```
1 2 4 8 16 32 64 128 256 512
```

---

## Section 2: `for` Loops

### Exercise 6 — Factorial Calculator
Ask the user for a number `n`. Calculate `n!` (n factorial = 1 × 2 × 3 × ... × n) using a `for` loop.

**Example:**
```
Enter a number: 5
5! = 120
```

> 💡 **Hint:** Start with `long result = 1;` and multiply in each iteration. Use `long` instead of `int` because factorials get very large.

### Exercise 7 — Custom Multiplication Table
Ask the user for a number. Print its multiplication table from 1 to 12 in a formatted way.

**Example:**
```
Enter a number: 8
8 x  1 =   8
8 x  2 =  16
8 x  3 =  24
...
8 x 12 =  96
```

### Exercise 8 — Fibonacci Sequence
Print the first 20 numbers of the Fibonacci sequence. Each number is the sum of the two before it: 0, 1, 1, 2, 3, 5, 8, 13, ...

> 💡 **Hint:** You need three variables: `a = 0`, `b = 1`, and a `temp` variable for swapping.

### Exercise 9 — Sum of Digits
Ask the user for a positive integer. Calculate the sum of its digits using a loop.

**Example:**
```
Enter a number: 1234
Sum of digits: 10
```

> 💡 **Hint:** Use `number % 10` to get the last digit and `number / 10` to remove it.

### Exercise 10 — Star Bar Chart
Ask the user for 5 numbers (between 1 and 20). For each number, print a bar of stars.

**Example:**
```
Enter value 1: 5
Enter value 2: 3
Enter value 3: 8
Enter value 4: 2
Enter value 5: 6

*****
***
********
**
******
```

---

## Section 3: `foreach` and Arrays

### Exercise 11 — Average Temperature
Create an array of 7 temperature values (doubles) representing daily temperatures for a week. Use `foreach` to calculate and display the average temperature.

### Exercise 12 — Count Vowels
Create a string array of 5 words entered by the user. Use `foreach` to count the total number of vowels across all words.

> 💡 **Hint:** You can iterate through characters of a string with `foreach (char c in word)`.

### Exercise 13 — Largest and Smallest
Create an integer array with at least 8 values. Use `foreach` to find and display both the largest and smallest values.

---

## Section 4: `break`, `continue`, and Nested Loops

### Exercise 14 — First Negative
Given an array of numbers, use a loop with `break` to find and print the first negative number. If there are no negative numbers, print "All positive."

```csharp
int[] data = { 5, 12, 8, -3, 7, -9, 4 };
```

### Exercise 15 — Skip Multiples of 3
Print numbers 1 through 30, but skip any number that is a multiple of 3. Use `continue`.

**Expected output:**
```
1 2 4 5 7 8 10 11 13 14 16 17 19 20 22 23 25 26 28 29
```

### Exercise 16 — Rectangle Pattern
Ask the user for a width and height. Print a rectangle of `*` characters using nested loops.

**Example (width=6, height=3):**
```
******
******
******
```

### Exercise 17 — Hollow Rectangle
Same as Exercise 16, but make the rectangle hollow — only the border is `*`, the inside is spaces.

**Example (width=6, height=4):**
```
******
*    *
*    *
******
```

> 💡 **Hint:** Print `*` when `row` is 0, `row` is last, `col` is 0, or `col` is last. Otherwise print a space.

### Exercise 18 — Number Pyramid
Print this number pyramid using nested loops:

```
        1
      2 3 2
    3 4 5 4 3
  4 5 6 7 6 5 4
5 6 7 8 9 8 7 6 5
```

---

## Section 5: Combined Challenges

### Exercise 19 — FizzBuzz
Print numbers 1 to 100. For multiples of 3, print "Fizz". For multiples of 5, print "Buzz". For multiples of both, print "FizzBuzz". Otherwise print the number.

### Exercise 20 — Simple Calculator Loop
Create a calculator that keeps running until the user chooses to quit. Each iteration:
1. Ask for two numbers
2. Ask for an operation (+, -, *, /)
3. Display the result
4. Ask "Continue? (yes/no)"

Include input validation for the operation and handle division by zero.

### Exercise 21 — Password Generator
Ask the user how many random numbers to generate (1–100). Generate that many random numbers between 1 and 999 and display them. Also show the largest, smallest, and average.

> 💡 **Hint:** Use `Random rand = new Random();` and `rand.Next(1, 1000);` to generate random numbers.

### Exercise 22 — Number Guessing Game (Warm-up for Assignment)
Generate a random number between 1 and 50. Give the user 7 attempts to guess it. After each guess, say "higher" or "lower". After 7 wrong guesses, reveal the number.

---

[← Back to Week 4 Overview](./README.md)
