# Lecture 3: Operators and Expressions

[← Previous: Lecture 2 – Type Conversion and Casting](./lecture-02-type-conversion.md) | [Back to Week 2 Overview](./README.md)

---

## 📋 Lecture Overview

| Item        | Detail                                                                |
| ----------- | --------------------------------------------------------------------- |
| Duration    | 45 minutes                                                            |
| Topics      | Arithmetic operators, assignment operators, precedence, string formatting |
| Preparation | Completed Lectures 1 & 2                                             |

---

## 1. Arithmetic Operators

Arithmetic operators let you perform mathematical calculations. If you've used a calculator, these will feel familiar:

| Operator | Name           | Example      | Result |
|----------|----------------|-------------|--------|
| `+`      | Addition       | `10 + 3`    | `13`   |
| `-`      | Subtraction    | `10 - 3`    | `7`    |
| `*`      | Multiplication | `10 * 3`    | `30`   |
| `/`      | Division       | `10 / 3`    | `3` ⚠️ |
| `%`      | Modulus (remainder) | `10 % 3` | `1`  |

```csharp
int a = 10;
int b = 3;

Console.WriteLine(a + b);   // 13
Console.WriteLine(a - b);   // 7
Console.WriteLine(a * b);   // 30
Console.WriteLine(a / b);   // 3 (not 3.33!)
Console.WriteLine(a % b);   // 1
```

### Integer Division — Watch Out!

When you divide two integers, C# performs **integer division** — it gives you only the whole number part and discards the remainder:

```csharp
int result = 10 / 3;
Console.WriteLine(result);     // Output: 3  (not 3.333...)

int result2 = 7 / 2;
Console.WriteLine(result2);    // Output: 3  (not 3.5)
```

If you want the decimal result, **at least one** of the numbers must be a `double` or `decimal`:

```csharp
double result3 = 10.0 / 3;
Console.WriteLine(result3);    // Output: 3.3333333333333335

double result4 = (double)10 / 3;
Console.WriteLine(result4);    // Output: 3.3333333333333335
```

> 💡 **This is one of the most common beginner mistakes.** Always check: are both sides of the `/` integers? If so, you'll get integer division.

### The Modulus Operator (%)

The modulus operator returns the **remainder** after division. It's more useful than you might think:

```csharp
Console.WriteLine(10 % 3);    // 1  (10 ÷ 3 = 3 remainder 1)
Console.WriteLine(15 % 5);    // 0  (15 ÷ 5 = 3 remainder 0)
Console.WriteLine(7 % 2);     // 1  (7 ÷ 2 = 3 remainder 1)
```

**Common uses of modulus:**

```csharp
// Check if a number is even or odd
int number = 7;
Console.WriteLine(number % 2);  // 1 means odd, 0 means even

// Get the last digit of a number
int value = 1234;
Console.WriteLine(value % 10);  // 4

// Wrap around (e.g., hours on a clock)
int hour = 15;
Console.WriteLine(hour % 12);   // 3 (3 PM on a 12-hour clock)
```

## 2. Operator Precedence

Just like in math, C# follows an order of operations. Multiplication and division happen before addition and subtraction:

| Priority | Operators | Direction |
|----------|-----------|-----------|
| Highest  | `()` Parentheses | — |
| High     | `*`, `/`, `%` | Left to right |
| Low      | `+`, `-` | Left to right |

```csharp
int result1 = 2 + 3 * 4;       // 14  (not 20!)
int result2 = (2 + 3) * 4;     // 20  (parentheses first)
int result3 = 10 - 4 / 2;      // 8   (division first: 10 - 2)
int result4 = (10 - 4) / 2;    // 3   (subtraction first: 6 / 2)
```

> 💡 **When in doubt, use parentheses.** They make your intent clear and prevent mistakes:
> ```csharp
> // Unclear — does the discount apply before or after tax?
> double total = price - discount * taxRate;
> 
> // Clear — discount first, then tax
> double total = (price - discount) * taxRate;
> ```

## 3. Assignment Operators

You already know the basic assignment operator `=`. C# also provides **compound assignment operators** that combine an operation with assignment:

| Operator | Equivalent To | Example |
|----------|---------------|---------|
| `=`      | Assignment     | `x = 10` |
| `+=`     | `x = x + value`  | `x += 5` → adds 5 to x |
| `-=`     | `x = x - value`  | `x -= 3` → subtracts 3 from x |
| `*=`     | `x = x * value`  | `x *= 2` → doubles x |
| `/=`     | `x = x / value`  | `x /= 4` → divides x by 4 |
| `%=`     | `x = x % value`  | `x %= 3` → remainder of x ÷ 3 |

```csharp
int score = 100;

score += 10;    // score is now 110
score -= 25;    // score is now 85
score *= 2;     // score is now 170
score /= 10;    // score is now 17
score %= 3;     // score is now 2

Console.WriteLine(score);  // Output: 2
```

### Increment and Decrement

Two special operators add or subtract 1:

```csharp
int count = 0;

count++;        // count is now 1  (same as count += 1)
count++;        // count is now 2
count--;        // count is now 1  (same as count -= 1)

Console.WriteLine(count);  // Output: 1
```

> 💡 You'll use `++` and `--` heavily in Week 4 when we learn about loops.

## 4. String Concatenation and Interpolation

### String Concatenation with `+`

You can join strings together using the `+` operator:

```csharp
string first = "Alice";
string last = "Smith";
string fullName = first + " " + last;
Console.WriteLine(fullName);   // Output: Alice Smith
```

You can also concatenate strings with non-string values — C# automatically converts them to strings:

```csharp
string name = "Alice";
int age = 25;
string message = name + " is " + age + " years old.";
Console.WriteLine(message);    // Output: Alice is 25 years old.
```

While this works, it gets messy with complex messages.

### String Interpolation with `$""`

String interpolation is a cleaner, more readable way to embed values inside strings. Place a `$` before the opening quote and use `{}` to embed expressions:

```csharp
string name = "Alice";
int age = 25;

string message = $"{name} is {age} years old.";
Console.WriteLine(message);    // Output: Alice is 25 years old.
```

You can put **any expression** inside the curly braces:

```csharp
int a = 10;
int b = 3;

Console.WriteLine($"{a} + {b} = {a + b}");        // 10 + 3 = 13
Console.WriteLine($"{a} / {b} = {(double)a / b}"); // 10 / 3 = 3.3333...
```

### Formatting Numbers

String interpolation supports **format specifiers** to control how numbers are displayed:

| Format | Meaning | Example | Output |
|--------|---------|---------|--------|
| `:F2`  | 2 decimal places | `$"{3.14159:F2}"` | `3.14` |
| `:F0`  | 0 decimal places (rounded) | `$"{3.7:F0}"` | `4` |
| `:C`   | Currency | `$"{19.99:C}"` | `$19.99` |
| `:N0`  | Number with commas | `$"{1500000:N0}"` | `1,500,000` |
| `:P`   | Percentage | `$"{0.85:P}"` | `85.00%` |

```csharp
double price = 49.999;
double taxRate = 0.08;
double total = price * (1 + taxRate);

Console.WriteLine($"Price:    {price:C}");
Console.WriteLine($"Tax Rate: {taxRate:P0}");
Console.WriteLine($"Total:    {total:C}");
```

**Output:**
```
Price:    $50.00
Tax Rate: 8%
Total:    $54.00
```

> 💡 **String interpolation with format specifiers is extremely useful.** It saves you from manually rounding or formatting numbers.

## 5. Putting It Together — A Practical Example

Let's combine everything from this lecture into a meaningful program:

```csharp
// Tip Calculator
Console.Write("Enter the bill amount: $");
double bill = double.Parse(Console.ReadLine());

Console.Write("Enter tip percentage (e.g., 15 for 15%): ");
double tipPercent = double.Parse(Console.ReadLine());

Console.Write("How many people are splitting the bill? ");
int people = int.Parse(Console.ReadLine());

double tipAmount = bill * (tipPercent / 100);
double total = bill + tipAmount;
double perPerson = total / people;

Console.WriteLine();
Console.WriteLine("===== Tip Calculator =====");
Console.WriteLine($"Bill:        {bill:C}");
Console.WriteLine($"Tip ({tipPercent}%):  {tipAmount:C}");
Console.WriteLine($"Total:       {total:C}");
Console.WriteLine($"Per Person:  {perPerson:C}");
```

**Sample Run:**
```
Enter the bill amount: $85.50
Enter tip percentage (e.g., 15 for 15%): 18
How many people are splitting the bill? 3

===== Tip Calculator =====
Bill:        $85.50
Tip (18%):   $15.39
Total:       $100.89
Per Person:  $33.63
```

This example uses variables, arithmetic operators, type conversion (string to double/int), and string interpolation with currency formatting.

---

## 🏋️ Exercises

### Exercise 1 — Expression Evaluator
Without running the code, predict the output of each expression. Then verify by running it:

```csharp
Console.WriteLine(15 / 4);
Console.WriteLine(15.0 / 4);
Console.WriteLine(15 % 4);
Console.WriteLine(2 + 3 * 4);
Console.WriteLine((2 + 3) * 4);
Console.WriteLine(10 / 3 * 3);
```

### Exercise 2 — Temperature Display
Write a program that asks the user for a temperature in Celsius, converts it to Fahrenheit (`F = C × 9/5 + 32`), and displays both values formatted to 1 decimal place.

> 💡 **Careful:** `9/5` in C# gives `1` (integer division). Use `9.0/5` or `9/5.0` instead.

### Exercise 3 — Compound Assignment Practice
Start with `int value = 100;`. Use compound assignment operators to:
1. Add 50
2. Subtract 30
3. Multiply by 2
4. Divide by 6
5. Get the remainder when divided by 7

Print the value after each operation.

### Exercise 4 — Formatted Receipt
Write a program that asks the user for three item prices, calculates the subtotal, tax (8%), and total, then displays a formatted receipt:

```
===== RECEIPT =====
Item 1:    $12.50
Item 2:    $8.75
Item 3:    $22.00
───────────────────
Subtotal:  $43.25
Tax (8%):  $3.46
Total:     $46.71
```

---

## 📌 Key Takeaways

- C# supports standard arithmetic operators: `+`, `-`, `*`, `/`, `%`
- **Integer division** discards the decimal part — ensure at least one operand is a `double` if you need decimal results
- The **modulus operator** (`%`) gives the remainder and is useful for even/odd checks and wrapping
- **Operator precedence** follows math rules — use parentheses when in doubt
- **Compound assignment** operators (`+=`, `-=`, etc.) are shorthand for updating a variable
- **String interpolation** (`$""`) is the cleanest way to embed values in strings
- **Format specifiers** (`:C`, `:F2`, `:N0`, `:P`) control how numbers display

---

## 📝 Week 2 Summary

Over three lectures, you have learned:

| Lecture | What You Learned |
| ------- | ---------------- |
| 1 | Variables, data types (`int`, `double`, `decimal`, `string`, `bool`, `char`), constants |
| 2 | Type conversion: implicit, explicit casting, `Convert`, `Parse`, `TryParse` |
| 3 | Arithmetic operators, assignment operators, precedence, string interpolation & formatting |

You now have the tools to **store data**, **convert between types**, **perform calculations**, and **format output**. These skills are the foundation for everything ahead.

**Next week** we'll learn about **conditional statements** — how to make your programs make decisions with `if`, `else`, and `switch`.

---

[← Previous: Lecture 2 – Type Conversion and Casting](./lecture-02-type-conversion.md) | [Back to Week 2 Overview](./README.md) | [Next Week: Week 3 – Conditional Statements →](../week-03/README.md)
