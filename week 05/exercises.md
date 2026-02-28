# Week 5 – Exercises: Methods and Modular Code

[← Back to Week 5 Overview](./README.md)

---

## How to Use These Exercises

Work through each section after completing the corresponding lecture. Start with the basics and work your way up. The **Challenge** problems combine multiple concepts and require more thought.

All methods in these exercises should be `static` and written outside of `Main()`.

---

## Section 1: Defining and Calling Methods (After Lecture 1)

### Exercise 1.1 — Greeting Method
Write a method called `PrintGreeting()` that prints:
```
***********************
*   Welcome, Student! *
***********************
```
Call it **three times** from `Main()`.

---

### Exercise 1.2 — Personalized Greeting
Write a method `GreetByName(string name)` that prints:
```
Hello, [name]! Nice to meet you.
```
Call it with at least 3 different names.

---

### Exercise 1.3 — Rectangle Area
Write a method `CalculateRectangleArea(double length, double width)` that **returns** the area as a `double`.

Test it in `Main()`:
```csharp
double area = CalculateRectangleArea(5.0, 3.0);
Console.WriteLine($"Area: {area}");  // Area: 15
```

---

### Exercise 1.4 — Max of Two
Write a method `GetMax(int a, int b)` that returns the larger of two integers.

Test cases:
```
GetMax(10, 20) → 20
GetMax(7, 3) → 7
GetMax(5, 5) → 5
```

---

### Exercise 1.5 — Is Even?
Write a method `IsEven(int number)` that returns `true` if the number is even, `false` otherwise.

Use it in `Main()` to check numbers 1 through 10 and print which are even.

---

### Exercise 1.6 — Temperature Converter
Write two methods:
- `CelsiusToFahrenheit(double celsius)` — returns the Fahrenheit value
- `FahrenheitToCelsius(double fahrenheit)` — returns the Celsius value

Formulas:
- F = C × 9/5 + 32
- C = (F - 32) × 5/9

Test with: 0°C, 100°C, 32°F, 212°F

---

## Section 2: Parameters and Return Values (After Lecture 2)

### Exercise 2.1 — Full Name Formatter
Write a method `FormatFullName(string firstName, string lastName)` that returns the full name with proper capitalization.

```
FormatFullName("john", "doe") → "John Doe"
```

> Hint: Use `Substring()` and `ToUpper()` / `ToLower()`.

---

### Exercise 2.2 — Discount Calculator
Write a method `CalculateFinalPrice(double originalPrice, double discountPercent)` that returns the discounted price.

Add a guard clause: if `originalPrice` is negative or `discountPercent` is outside 0–100, return the original price unchanged.

Test cases:
```
CalculateFinalPrice(100, 20) → 80.0
CalculateFinalPrice(49.99, 10) → 44.991
CalculateFinalPrice(-50, 20) → -50 (invalid, return original)
CalculateFinalPrice(100, 150) → 100 (invalid percent, return original)
```

---

### Exercise 2.3 — Tip Calculator
Write a method `CalculateTip(double billAmount, double tipPercent)` that returns the tip amount.

Write a second method `CalculateTotal(double billAmount, double tipPercent)` that calls `CalculateTip` and adds it to the bill.

```
Bill: $85.00, Tip: 18%
Tip amount: $15.30
Total: $100.30
```

---

### Exercise 2.4 — Password Validator
Write a method `IsValidPassword(string password)` that returns `true` only if:
- Length is at least 8 characters
- Contains at least one digit
- Contains at least one uppercase letter

Test with: `"Hello1"` (false), `"password123"` (false), `"Hello123"` (true), `"Ab1cdefg"` (true)

---

### Exercise 2.5 — Number Classifier
Write these boolean methods:
- `IsPositive(int n)` — returns true if n > 0
- `IsNegative(int n)` — returns true if n < 0
- `IsZero(int n)` — returns true if n == 0
- `IsOdd(int n)` — returns true if n is odd

Write a `ClassifyNumber(int n)` method that uses all four to print a description:
```
ClassifyNumber(7)  → "7 is positive and odd"
ClassifyNumber(-4) → "-4 is negative and even"
ClassifyNumber(0)  → "0 is zero and even"
```

---

### Exercise 2.6 — Shipping Cost Calculator
Write a method `CalculateShippingCost(double weight, string destination)` that returns the shipping cost:

| Destination | Base Cost | Per kg |
|------------|-----------|--------|
| "local" | $5.00 | $0.50 |
| "national" | $10.00 | $1.00 |
| "international" | $25.00 | $2.50 |

If the destination is unknown, return -1.

Use `destination.ToLower()` to handle case differences.

---

## Section 3: Overloading and Organization (After Lecture 3)

### Exercise 3.1 — Overloaded Print
Create overloaded versions of a `Print` method:
- `Print(string message)` — prints the message
- `Print(string message, int times)` — prints the message N times
- `Print(string message, int times, string border)` — prints with a border character

```csharp
Print("Hello");                    // Hello
Print("Hi", 3);                    // Hi  Hi  Hi
Print("Hey", 2, "* ");            // * Hey * Hey *
```

---

### Exercise 3.2 — Overloaded Area
Create overloaded `CalculateArea` methods:
- `CalculateArea(double side)` — square (side × side)
- `CalculateArea(double length, double width)` — rectangle (length × width)
- `CalculateArea(double radius, bool isCircle)` — circle (π × r²)

Test each version and print the results.

---

### Exercise 3.3 — Refactor This Code
Refactor the following code into at least 4 well-named methods:

```csharp
static void Main(string[] args)
{
    Console.Write("Enter product name: ");
    string product = Console.ReadLine();
    Console.Write("Enter price: ");
    double price = Convert.ToDouble(Console.ReadLine());
    Console.Write("Enter quantity: ");
    int quantity = int.Parse(Console.ReadLine());

    double subtotal = price * quantity;
    double tax = subtotal * 0.10;
    double total = subtotal + tax;

    Console.WriteLine("\n--- Receipt ---");
    Console.WriteLine($"Product:  {product}");
    Console.WriteLine($"Price:    {price:C}");
    Console.WriteLine($"Quantity: {quantity}");
    Console.WriteLine($"Subtotal: {subtotal:C}");
    Console.WriteLine($"Tax (10%): {tax:C}");
    Console.WriteLine($"Total:    {total:C}");
    Console.WriteLine("---------------");
}
```

Your refactored `Main()` should be about 6–8 lines.

---

### Exercise 3.4 — Method Tracing
Without running the code, trace through and predict the output:

```csharp
static void Main(string[] args)
{
    int result = Mystery(5);
    Console.WriteLine($"Result: {result}");
}

static int Mystery(int n)
{
    if (n <= 1)
        return 1;

    return n * Mystery(n - 1);
}
```

Draw the call stack at the point when `Mystery(1)` is called.

> **Note:** This is an example of **recursion** — a method calling itself. We won't focus on recursion in this course, but it's good to recognize the pattern.

---

### Exercise 3.5 — Build a Unit Converter
Build a unit converter program with the following methods:
- `KmToMiles(double km)` — returns miles (km × 0.621371)
- `MilesToKm(double miles)` — returns km (miles × 1.60934)
- `KgToLbs(double kg)` — returns pounds (kg × 2.20462)
- `LbsToKg(double lbs)` — returns kg (lbs × 0.453592)
- `DisplayConversion(double value, string fromUnit, double result, string toUnit)` — prints the conversion

Create a menu-driven program that lets the user choose a conversion, enter a value, and see the result. Use a loop to keep the menu running until the user quits.

---

## Challenge Problems

### Challenge 1: Mini Math Library
Create a set of math utility methods:
- `Power(double baseNum, int exponent)` — calculate power using a loop (don't use `Math.Pow`)
- `Factorial(int n)` — calculate n! (n × (n-1) × ... × 1)
- `IsPrime(bool n)` — returns true if n is prime
- `Fibonacci(int n)` — returns the nth Fibonacci number

Use them together to create a "Math Toolkit" program with a menu.

---

### Challenge 2: Text Analysis Tool
Write methods to analyze a string:
- `CountWords(string text)` — returns word count
- `CountVowels(string text)` — returns vowel count
- `CountConsonants(string text)` — returns consonant count
- `ReverseString(string text)` — returns the reversed string
- `IsPalindrome(string text)` — returns true if the text reads the same forwards and backwards (ignore spaces and case)

Build a program that reads a sentence and displays all analysis results.

---

### Challenge 3: Payroll Calculator
Build a payroll program using methods:
- `CalculateGrossPay(double hoursWorked, double hourlyRate)` — include overtime: hours over 40 are paid at 1.5× rate
- `CalculateTaxes(double grossPay)` — use brackets: 0% on first $500, 10% on $500–$1500, 20% on everything above $1500
- `CalculateNetPay(double grossPay, double taxes)` — returns gross minus taxes
- `PrintPayStub(string employeeName, double hours, double rate, double gross, double taxes, double net)` — formatted output

Process 3 employees and display their pay stubs.

---

[← Back to Week 5 Overview](./README.md)
