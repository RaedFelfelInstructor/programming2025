# Lecture 1: Static Members and Static Classes

[Back to Week 15 Overview](./README.md) | [Next: Lecture 2 – Introduction to Async/Await and Course Review →](./lecture-2.md)

---

## Lecture Overview

| Item | Detail |
|------|--------|
| Duration | 45 minutes |
| Topics | Static fields, static methods, static classes, utility/helper class patterns |
| Preparation | Comfortable with classes, objects, methods, and properties from Weeks 7–8 |

---

## 1. The Problem: Some Things Don't Belong to an Object

Throughout Weeks 7–11, you learned to create classes and objects. Every field, property, and method you wrote belonged to a **specific object** — an *instance* of a class. You created a `Student` object, a `BankAccount` object, and each one had its own separate data.

But consider this: what if you want a method that converts Celsius to Fahrenheit? That calculation doesn't belong to any particular object. There's no "temperature converter object" that holds state — it's just a utility function. Or think about `Console.WriteLine()` — you never write `new Console()`. You just call the method directly on the class.

This is where **static members** come in.

---

## 2. Instance vs Static: The Core Distinction

### Instance Members (What You Already Know)

Instance members belong to a **specific object**. Each object gets its own copy.

```csharp
public class Student
{
    public string Name { get; set; }   // Each student has their own name
    public double Gpa { get; set; }    // Each student has their own GPA

    public void PrintInfo()            // Called on a specific student
    {
        Console.WriteLine($"{Name} — GPA: {Gpa}");
    }
}
```

```csharp
Student alice = new Student { Name = "Alice", Gpa = 3.8 };
Student bob = new Student { Name = "Bob", Gpa = 3.2 };

alice.PrintInfo();  // Alice — GPA: 3.8
bob.PrintInfo();    // Bob — GPA: 3.2
```

Each `Student` object has its **own** `Name` and `Gpa`. Calling `PrintInfo()` on `alice` gives different results than calling it on `bob`.

### Static Members (New Concept)

Static members belong to the **class itself**, not to any particular object. There's only **one copy**, shared across all instances.

```csharp
public class Student
{
    public string Name { get; set; }
    public double Gpa { get; set; }

    // Static field — shared across ALL students
    public static int TotalStudents { get; private set; } = 0;

    public Student(string name, double gpa)
    {
        Name = name;
        Gpa = gpa;
        TotalStudents++;   // Every new student increments the shared counter
    }

    public void PrintInfo()
    {
        Console.WriteLine($"{Name} — GPA: {Gpa}");
    }

    // Static method — called on the class, not an object
    public static void PrintTotal()
    {
        Console.WriteLine($"Total students created: {TotalStudents}");
    }
}
```

```csharp
Student alice = new Student("Alice", 3.8);
Student bob = new Student("Bob", 3.2);
Student charlie = new Student("Charlie", 3.5);

// Call static members on the CLASS NAME — not on an object
Student.PrintTotal();   // Total students created: 3
Console.WriteLine(Student.TotalStudents);  // 3
```

**Output:**
```
Total students created: 3
3
```

> **Key rule:** Static members are accessed through the **class name** (`Student.TotalStudents`), never through an object (`alice.TotalStudents` won't compile).

---

## 3. The `static` Keyword — Where You Can Use It

You can apply `static` to fields, properties, methods, and even entire classes:

| Element | Syntax | Meaning |
|---------|--------|---------|
| Static field | `public static int Count;` | One shared variable for the class |
| Static property | `public static int Count { get; set; }` | Shared property with get/set |
| Static method | `public static double Add(double a, double b)` | Method called on the class, not an object |
| Static class | `public static class MathHelper` | Class that can **only** contain static members |

---

## 4. Static Methods — Utility Functions

Static methods are perfect for operations that don't need object state. They take input through parameters, do their work, and return a result.

### Example: A Temperature Converter

```csharp
public class TemperatureConverter
{
    public static double CelsiusToFahrenheit(double celsius)
    {
        return celsius * 9.0 / 5.0 + 32;
    }

    public static double FahrenheitToCelsius(double fahrenheit)
    {
        return (fahrenheit - 32) * 5.0 / 9.0;
    }
}
```

```csharp
double tempF = TemperatureConverter.CelsiusToFahrenheit(100);
Console.WriteLine($"100°C = {tempF}°F");   // 100°C = 212°F

double tempC = TemperatureConverter.FahrenheitToCelsius(72);
Console.WriteLine($"72°F = {tempC:F1}°C");  // 72°F = 22.2°C
```

Notice: no `new TemperatureConverter()`. You call the methods directly on the class.

### Example: Input Validation Helper

```csharp
public class InputHelper
{
    public static int ReadInt(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            if (int.TryParse(Console.ReadLine(), out int result))
                return result;
            Console.WriteLine("Invalid input. Please enter a whole number.");
        }
    }

    public static double ReadDouble(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            if (double.TryParse(Console.ReadLine(), out double result))
                return result;
            Console.WriteLine("Invalid input. Please enter a number.");
        }
    }

    public static string ReadNonEmpty(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            string input = Console.ReadLine()?.Trim() ?? "";
            if (input.Length > 0)
                return input;
            Console.WriteLine("Input cannot be empty.");
        }
    }
}
```

```csharp
// Usage — clean and reusable
string name = InputHelper.ReadNonEmpty("Enter your name: ");
int age = InputHelper.ReadInt("Enter your age: ");
double gpa = InputHelper.ReadDouble("Enter your GPA: ");

Console.WriteLine($"{name}, Age: {age}, GPA: {gpa}");
```

This is exactly the kind of helper you've probably wished you had in earlier assignments! Now you know how to build one.

---

## 5. Static Classes — Enforcing the Pattern

If a class should **only** contain static members and should never be instantiated, mark the entire class as `static`:

```csharp
public static class MathHelper
{
    public static double CircleArea(double radius)
    {
        return Math.PI * radius * radius;
    }

    public static double RectangleArea(double width, double height)
    {
        return width * height;
    }

    public static double TriangleArea(double baseLength, double height)
    {
        return 0.5 * baseLength * height;
    }

    public static int Factorial(int n)
    {
        if (n < 0) throw new ArgumentException("Number must be non-negative.");
        int result = 1;
        for (int i = 2; i <= n; i++)
            result *= i;
        return result;
    }
}
```

```csharp
Console.WriteLine(MathHelper.CircleArea(5));       // 78.53981633974483
Console.WriteLine(MathHelper.RectangleArea(4, 6)); // 24
Console.WriteLine(MathHelper.Factorial(5));        // 120

// This won't compile — you can't instantiate a static class:
// MathHelper helper = new MathHelper();  ❌ Compile error
```

### Why Use a Static Class?

- **Makes intent clear** — this class is a collection of utilities, not a blueprint for objects
- **Prevents mistakes** — no one can accidentally create an instance
- **Familiar pattern** — `Math`, `Console`, and `Convert` are all static classes in .NET

---

## 6. Static Fields — Shared State

Static fields are useful when all objects of a class need to share a common value.

### Example: Auto-Incrementing IDs

```csharp
public class Order
{
    private static int _nextId = 1;   // Shared counter

    public int Id { get; }
    public string Product { get; set; }
    public int Quantity { get; set; }

    public Order(string product, int quantity)
    {
        Id = _nextId++;   // Each order gets the next ID
        Product = product;
        Quantity = quantity;
    }

    public override string ToString()
    {
        return $"Order #{Id}: {Product} x{Quantity}";
    }
}
```

```csharp
Order order1 = new Order("Laptop", 1);
Order order2 = new Order("Mouse", 3);
Order order3 = new Order("Keyboard", 2);

Console.WriteLine(order1);  // Order #1: Laptop x1
Console.WriteLine(order2);  // Order #2: Mouse x3
Console.WriteLine(order3);  // Order #3: Keyboard x2
```

The `_nextId` field is shared — every `Order` object reads and increments the same counter.

---

## 7. Mixing Static and Instance Members

A class can have **both** static and instance members. This is common and useful:

```csharp
public class BankAccount
{
    // Static members — shared across all accounts
    private static int _nextAccountNumber = 1001;
    private static decimal _totalDeposits = 0;

    public static int TotalAccounts { get; private set; } = 0;

    public static void PrintBankSummary()
    {
        Console.WriteLine($"Total accounts: {TotalAccounts}");
        Console.WriteLine($"Total deposits across all accounts: {_totalDeposits:C}");
    }

    // Instance members — unique to each account
    public int AccountNumber { get; }
    public string Owner { get; set; }
    public decimal Balance { get; private set; }

    public BankAccount(string owner, decimal initialDeposit)
    {
        AccountNumber = _nextAccountNumber++;
        Owner = owner;
        Balance = initialDeposit;
        _totalDeposits += initialDeposit;
        TotalAccounts++;
    }

    public void Deposit(decimal amount)
    {
        if (amount <= 0) throw new ArgumentException("Deposit must be positive.");
        Balance += amount;
        _totalDeposits += amount;
    }

    public override string ToString()
    {
        return $"Account #{AccountNumber} ({Owner}): {Balance:C}";
    }
}
```

```csharp
var acc1 = new BankAccount("Alice", 1000);
var acc2 = new BankAccount("Bob", 2500);
acc1.Deposit(500);

Console.WriteLine(acc1);   // Account #1001 (Alice): $1,500.00
Console.WriteLine(acc2);   // Account #1002 (Bob): $2,500.00

BankAccount.PrintBankSummary();
// Total accounts: 2
// Total deposits across all accounts: $4,000.00
```

> **Important rule:** Static methods **cannot** access instance members directly. A static method doesn't know which object you mean — there might be thousands of them. If you try to use `this` or access an instance field inside a static method, you'll get a compile error.

---

## 8. The Rules of Static

Here's a quick reference for what can access what:

| From \ To | Instance members | Static members |
|-----------|-----------------|----------------|
| **Instance method** | ✅ Yes | ✅ Yes |
| **Static method** | ❌ No (no `this`) | ✅ Yes |

In plain English:
- Instance methods can access **everything** (both instance and static members)
- Static methods can **only** access other static members

```csharp
public class Demo
{
    private int instanceValue = 10;
    private static int staticValue = 20;

    public void InstanceMethod()
    {
        Console.WriteLine(instanceValue);   // ✅ OK
        Console.WriteLine(staticValue);     // ✅ OK — instance can access static
    }

    public static void StaticMethod()
    {
        // Console.WriteLine(instanceValue); // ❌ Compile error!
        Console.WriteLine(staticValue);      // ✅ OK
    }
}
```

---

## 9. Static Members You've Already Used

You've been using static members throughout this course without realizing it:

| Usage | What's Static |
|-------|---------------|
| `Console.WriteLine("Hi")` | `Console` is a static class; `WriteLine` is a static method |
| `Math.PI` | `PI` is a static field on the static `Math` class |
| `Math.Max(a, b)` | `Max` is a static method |
| `int.TryParse(s, out n)` | `TryParse` is a static method on `int` |
| `Convert.ToDouble(x)` | `Convert` is a static class |
| `string.IsNullOrEmpty(s)` | `IsNullOrEmpty` is a static method on `string` |

Now you understand *why* these work differently from the instance methods you call on objects (like `myList.Add()` or `student.PrintInfo()`).

---

## 10. When to Use Static vs Instance

Here's a decision guide:

```
Does this data/behavior belong to a SPECIFIC OBJECT?
├── YES → Use INSTANCE members
│         Examples: student's name, account balance, order total
│
└── NO  → Does it belong to the CLASS AS A WHOLE?
          ├── YES → Use STATIC members on a regular class
          │         Examples: student count, next ID, bank totals
          │
          └── Is it a standalone UTILITY with no state?
              └── YES → Use a STATIC CLASS
                        Examples: MathHelper, InputHelper, Converter
```

### Common Use Cases for Static

- **Counters and IDs** — tracking how many objects have been created
- **Utility/helper methods** — conversions, calculations, validation
- **Factory methods** — static methods that create and return objects
- **Constants and configuration** — values shared across all instances
- **Extension of built-in functionality** — your own `StringHelper`, `DateHelper`, etc.

---

## Summary

| Concept | Description |
|---------|-------------|
| `static` field | One shared variable for the entire class |
| `static` property | Shared property accessed via the class name |
| `static` method | Method that belongs to the class, not an object |
| `static` class | Class that can **only** contain static members; cannot be instantiated |
| Instance → static | Instance methods **can** access static members |
| Static → instance | Static methods **cannot** access instance members |

**Key takeaway:** Use static for things that don't belong to any particular object — shared counters, utility functions, and helper classes. Use instance members for everything that's unique to each object.

---

[Back to Week 15 Overview](./README.md) | [Next: Lecture 2 – Introduction to Async/Await and Course Review →](./lecture-2.md)
