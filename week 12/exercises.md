# Week 12 – Exercises: Exception Handling and Defensive Programming

[← Back to Week 12 Overview](./README.md)

---

These exercises progress from basic exception handling to designing robust classes with layered validation. Work through them in order — each section builds on the previous one.

---

## Section A: try-catch Fundamentals (Lecture 1)

### Exercise 1 — Safe Calculator
Write a program that asks the user for two numbers and an operator (+, -, *, /). Perform the calculation inside a try-catch block. Handle:
- `FormatException` — if the user enters a non-numeric value
- `DivideByZeroException` — if dividing by zero

Display a helpful error message for each case and let the user try again.

**Expected Output:**
```
Enter first number: abc
❌ That's not a valid number. Try again.

Enter first number: 10
Enter second number: 0
Enter operator (+, -, *, /): /
❌ Cannot divide by zero. Try again.

Enter first number: 10
Enter second number: 3
Enter operator (+, -, *, /): /
✅ 10 / 3 = 3.33
```

### Exercise 2 — Array Safe Access
Write a method `static string SafeGetElement(string[] array, int index)` that returns the element at the given index. If the index is out of range, catch the `IndexOutOfRangeException` and return `"[Invalid Index]"` instead.

Test with:
```csharp
string[] colors = { "Red", "Green", "Blue" };
Console.WriteLine(SafeGetElement(colors, 1));   // Green
Console.WriteLine(SafeGetElement(colors, 5));   // [Invalid Index]
Console.WriteLine(SafeGetElement(colors, -1));  // [Invalid Index]
```

### Exercise 3 — Exception Details Reporter
Write a program that deliberately triggers three different exceptions. For each one, catch it and display:
- The exception type name
- The error message
- Whether it has an inner exception (true/false)

Suggested exceptions to trigger: `FormatException`, `DivideByZeroException`, `IndexOutOfRangeException`

### Exercise 4 — Multiple Catch Blocks
Write a program that reads a filename from the user and an index number, then tries to:
1. Read all lines from the file (`File.ReadAllLines`)
2. Print the line at the given index

Handle all of these scenarios with separate catch blocks:
- `FileNotFoundException` → "File not found"
- `IndexOutOfRangeException` → "Line number doesn't exist"
- `FormatException` → "Invalid line number format"
- `Exception` → catch-all for anything unexpected

### Exercise 5 — finally Demonstration
Write a program that simulates opening a connection, performing an operation, and closing the connection. Use `Console.WriteLine` to trace the flow. Demonstrate that the `finally` block runs in all three scenarios:
1. No exception occurs
2. An exception is caught
3. An exception is thrown but not caught (wrap in an outer try-catch to prevent crash)

---

## Section B: Throwing Exceptions and Custom Exceptions (Lecture 2)

### Exercise 6 — Temperature Validator
Write a class `Temperature` with a property `Celsius`. In the setter:
- Throw `ArgumentOutOfRangeException` if the value is below -273.15 (absolute zero)
- Throw `ArgumentOutOfRangeException` if the value is above 1000

Add a read-only property `Fahrenheit` that converts Celsius. Test with valid and invalid values, catching exceptions.

### Exercise 7 — Guard Clause Practice
Write a method `static string FormatFullName(string firstName, string lastName)` that:
- Throws `ArgumentNullException` if either parameter is `null`
- Throws `ArgumentException` if either is empty or whitespace
- Returns the formatted name as "LastName, FirstName"

Use guard clauses (check-and-throw at the top). Test with various invalid inputs.

### Exercise 8 — Custom NegativeQuantityException
Create a custom `NegativeQuantityException` class with:
- A `Quantity` property (int)
- A `ProductName` property (string)
- A constructor that builds a descriptive message

Use it in a `ShoppingCart` class with an `AddItem(string product, int quantity)` method that throws this exception when quantity is negative.

### Exercise 9 — Custom Exception Hierarchy
Create an exception hierarchy for an email system:

```
EmailException (base)
├── InvalidEmailFormatException (bad email format)
├── EmailNotFoundException (recipient not found)
└── MailboxFullException (recipient's inbox is full, includes a Capacity property)
```

Write a method `SendEmail(string to, string subject)` that throws different exceptions based on the input:
- Email without "@" → `InvalidEmailFormatException`
- Email to "unknown@test.com" → `EmailNotFoundException`
- Email to "full@test.com" → `MailboxFullException`

Catch each one separately in the calling code.

### Exercise 10 — Exception Propagation Chain
Write four methods: `Main` → `ProcessPayment` → `ValidateCard` → `CheckCardNumber`

- `CheckCardNumber` throws `ArgumentException` if the card number isn't exactly 16 digits
- `ValidateCard` calls `CheckCardNumber` (no try-catch — lets it propagate)
- `ProcessPayment` catches the exception, wraps it in an `InvalidOperationException` with the original as `InnerException`, and re-throws
- `Main` catches the `InvalidOperationException` and prints both the outer and inner exception messages

---

## Section C: Validation and Defensive Programming (Lecture 3)

### Exercise 11 — TryParse Toolkit
Write the following validation methods using TryParse (not try-catch):
- `static int GetValidInt(string prompt)` — loops until valid int
- `static double GetValidDouble(string prompt, double min, double max)` — loops until valid double in range
- `static DateTime GetValidDate(string prompt)` — loops until valid date

Test all three in a program that collects: an age (int), a salary (double between 0 and 1,000,000), and a birthdate.

### Exercise 12 — Robust Menu System
Create a `MenuSystem` class with:
- A `List<string>` of menu options (added via `AddOption`)
- A `ShowMenu()` method that displays options and returns the user's valid choice
- Use TryParse for input validation, not try-catch
- Handle edge cases: empty menu (throw `InvalidOperationException`), valid range checking

### Exercise 13 — Validated Employee Class
Create an `Employee` class with these validated properties:
- `Name` — not null/empty, max 100 characters
- `Email` — must contain "@" and "." after the "@"
- `Salary` — must be between 0 and 10,000,000
- `Department` — must be one of: "Engineering", "Marketing", "Sales", "HR", "Finance"

Use guard clauses that throw appropriate exception types. Write a console program that uses TryParse and string validation at the UI level before constructing the Employee.

### Exercise 14 — Safe File Operations
Write a program that:
1. Asks the user for a filename
2. Uses `using` to write 5 lines of text to the file
3. Uses `using` to read the file back and display its contents
4. Handles `IOException` and `UnauthorizedAccessException`
5. Has a `finally` block that confirms the operation is complete

---

## Section D: Combined Challenges

### Exercise 15 — Robust Product Catalog
Create a complete mini-system with:
- `Product` class (Name, Price, Stock — all validated with guard clauses)
- Custom `OutOfStockException` with `Requested` and `Available` properties
- A `Catalog` class with `AddProduct`, `RemoveProduct`, `SellProduct` methods
- Console UI with TryParse input validation
- Handle: duplicate products, selling more than available, negative prices/quantities

**Required functionality:**
```
=== Product Catalog ===
1. Add Product
2. Sell Product
3. View Catalog
4. Exit
```

### Exercise 16 — Grade Book with Exceptions
Build a grade management system:
- `Grade` class with `StudentName`, `Subject`, `Score` (0-100) — all validated
- Custom `InvalidGradeException` (thrown when score is out of range)
- `GradeBook` class that stores grades and provides:
  - `AddGrade(Grade grade)` — throws if duplicate (same student + subject)
  - `GetAverage(string studentName)` — throws `InvalidOperationException` if student has no grades
  - `GetTopStudent(string subject)` — throws `InvalidOperationException` if no grades for subject
- Console program with full input validation

### Exercise 17 — Layered Validation Demo
Write a program that demonstrates the two-layer validation approach:

1. **Create an `Order` class** with: `CustomerId` (string, required), `ProductName` (string, required), `Quantity` (int, 1-1000), `UnitPrice` (decimal, > 0). All validated with guard clauses.
2. **Create a console UI** that collects order information using TryParse and string checks.
3. **Show that both layers work:**
   - Enter obviously bad format input (letters for numbers) → UI catches it
   - Enter valid format but bad business values (quantity of 5000) → class throws exception
   - Enter valid data → order created successfully

Display a clear message at each step showing which layer caught the error.

---

## Difficulty Guide

| Exercises | Difficulty | Concepts |
|-----------|-----------|----------|
| 1–5 | ⭐ Basic | try-catch, finally, multiple catches |
| 6–10 | ⭐⭐ Intermediate | throw, guard clauses, custom exceptions, propagation |
| 11–14 | ⭐⭐ Intermediate | TryParse, validation patterns, using statement |
| 15–17 | ⭐⭐⭐ Challenging | Full integration, layered validation, robust design |

---

[← Back to Week 12 Overview](./README.md)
