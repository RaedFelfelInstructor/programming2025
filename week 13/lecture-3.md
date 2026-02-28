# Lecture 3: Nullable Types and Null Safety

[← Previous: Lecture 2 – Enums](./lecture-2.md) | [Back to Week 13 Overview](./README.md)

---

## Lecture Overview

| Item | Detail |
|------|--------|
| Duration | 45 minutes |
| Topics | Nullable value types (`int?`, `bool?`), null checking patterns, null-coalescing operators (`??`, `??=`), nullable reference types concept |
| Preparation | Completed Lectures 1–2 this week, comfortable with exception handling from Week 12 |

---

## 1. The Problem: When a Value Might Not Exist

Sometimes, the absence of a value is meaningful. Consider these real-world scenarios:

- A student hasn't taken a test yet — their score isn't `0`, it's **unknown**
- A user profile has an optional middle name — it might not exist at all
- A database query returns a customer's phone number — some customers don't have one
- A sensor reading hasn't arrived yet — the temperature isn't `0`, it's **missing**

In C#, **value types** (`int`, `double`, `bool`) always have a value. An `int` defaults to `0`, a `bool` to `false`. But what if `0` is a legitimate value? How do you distinguish "the score is 0" from "no score exists yet"?

```csharp
int testScore = 0; // Is this "scored zero" or "hasn't taken the test"?
```

---

## 2. Nullable Value Types

C# solves this with **nullable value types** — adding a `?` after the type name:

```csharp
int? score = null;       // "No score yet"
double? temperature = null;  // "No reading yet"
bool? isActive = null;   // "Unknown status"

// You can also assign normal values
score = 95;
temperature = 72.5;
isActive = true;
```

### The `?` Explained

`int?` is shorthand for `Nullable<int>` — a generic struct that wraps a value type and adds the ability to be `null`:

```csharp
// These are equivalent
int? a = null;
Nullable<int> b = null;
```

### Checking for a Value

Every nullable type has two important properties:

```csharp
int? score = 95;

// HasValue — is there a value?
Console.WriteLine(score.HasValue);  // True

// Value — the actual value (throws if null!)
Console.WriteLine(score.Value);     // 95

// You can also compare to null directly
if (score != null)
{
    Console.WriteLine($"Score: {score}");  // Implicit .Value
}

// Or use pattern matching
if (score is int actualScore)
{
    Console.WriteLine($"Score: {actualScore}");
}
```

```csharp
int? empty = null;

Console.WriteLine(empty.HasValue);  // False
// Console.WriteLine(empty.Value);  // 💥 InvalidOperationException!

if (empty == null)
{
    Console.WriteLine("No score available");
}
```

### Common Mistake: Accessing `.Value` Without Checking

```csharp
int? score = null;

// ❌ DANGEROUS — will throw if null
int result = score.Value;

// ✅ SAFE — check first
if (score.HasValue)
{
    int result2 = score.Value;
}

// ✅ SAFE — use pattern matching
if (score is int actualScore)
{
    Console.WriteLine(actualScore);
}
```

---

## 3. The Null-Coalescing Operator (`??`)

The `??` operator provides a **default value** when something is null:

```csharp
int? score = null;
int displayScore = score ?? 0;  // Use 0 if score is null

Console.WriteLine(displayScore); // 0
```

Read `??` as **"if null, use this instead"**:

```csharp
string? name = null;
string displayName = name ?? "Anonymous";
Console.WriteLine(displayName); // Anonymous

int? quantity = 5;
int displayQuantity = quantity ?? 0;
Console.WriteLine(displayQuantity); // 5 (not null, so uses actual value)
```

### Chaining `??`

You can chain multiple `??` operators — it returns the first non-null value:

```csharp
string? firstName = null;
string? nickname = null;
string? email = "alice@example.com";

string display = firstName ?? nickname ?? email ?? "Unknown";
Console.WriteLine(display); // alice@example.com
```

---

## 4. The Null-Coalescing Assignment Operator (`??=`)

The `??=` operator assigns a value **only if the current value is null**:

```csharp
string? name = null;
name ??= "Default";      // name is null, so it becomes "Default"
Console.WriteLine(name);   // Default

name ??= "Another";       // name is NOT null, so nothing happens
Console.WriteLine(name);   // Default (unchanged)
```

This is useful for lazy initialization:

```csharp
class UserSettings
{
    private string? _theme;

    public string Theme
    {
        get
        {
            _theme ??= "Light";  // Set default on first access
            return _theme;
        }
        set { _theme = value; }
    }
}
```

---

## 5. Practical Patterns with Nullable Types

### Pattern 1: Optional Method Parameters

```csharp
static void DisplayStudent(string name, int? age = null, double? gpa = null)
{
    Console.WriteLine($"Name: {name}");
    Console.WriteLine($"Age: {(age.HasValue ? age.Value.ToString() : "Not provided")}");
    Console.WriteLine($"GPA: {(gpa.HasValue ? gpa.Value.ToString("F2") : "Not available")}");
    Console.WriteLine();
}

DisplayStudent("Alice", 20, 3.8);
DisplayStudent("Bob", 22);          // No GPA
DisplayStudent("Charlie");           // No age or GPA
```

**Output:**
```
Name: Alice
Age: 20
GPA: 3.80

Name: Bob
Age: 22
GPA: Not available

Name: Charlie
Age: Not provided
GPA: Not available
```

### Pattern 2: Search That Might Fail

```csharp
static int? FindStudentAge(Dictionary<string, int> students, string name)
{
    if (students.TryGetValue(name, out int age))
    {
        return age;
    }
    return null;  // Student not found — return null instead of -1 or throwing
}

Dictionary<string, int> students = new Dictionary<string, int>
{
    { "Alice", 20 },
    { "Bob", 22 }
};

int? aliceAge = FindStudentAge(students, "Alice");
int? daveAge = FindStudentAge(students, "Dave");

Console.WriteLine($"Alice's age: {aliceAge ?? -1}");  // 20
Console.WriteLine($"Dave's age: {daveAge ?? -1}");     // -1 (not found)
```

### Pattern 3: Nullable in Collections with Enums

Combining what we learned this week:

```csharp
enum TaskStatus
{
    NotStarted,
    InProgress,
    Completed,
    Cancelled
}

class TodoItem
{
    public string Title { get; set; }
    public TaskStatus Status { get; set; }
    public DateTime? CompletedDate { get; set; } // null if not completed

    public override string ToString()
    {
        string dateStr = CompletedDate.HasValue
            ? CompletedDate.Value.ToString("yyyy-MM-dd")
            : "N/A";
        return $"[{Status}] {Title} (Completed: {dateStr})";
    }
}

List<TodoItem> tasks = new List<TodoItem>
{
    new TodoItem
    {
        Title = "Write report",
        Status = TaskStatus.Completed,
        CompletedDate = new DateTime(2025, 3, 15)
    },
    new TodoItem
    {
        Title = "Review PR",
        Status = TaskStatus.InProgress,
        CompletedDate = null  // Not completed yet
    },
    new TodoItem
    {
        Title = "Deploy update",
        Status = TaskStatus.NotStarted,
        CompletedDate = null
    }
};

foreach (TodoItem task in tasks)
{
    Console.WriteLine(task);
}
```

**Output:**
```
[Completed] Write report (Completed: 2025-03-15)
[InProgress] Review PR (Completed: N/A)
[NotStarted] Deploy update (Completed: N/A)
```

---

## 6. The Null-Conditional Operator (`?.`)

The `?.` operator short-circuits to `null` if the left side is `null`, instead of throwing a `NullReferenceException`:

```csharp
string? name = "Alice";
int? length = name?.Length;   // 5

name = null;
length = name?.Length;        // null (not NullReferenceException!)
Console.WriteLine(length ?? 0); // 0
```

This is especially useful with chains:

```csharp
class Address
{
    public string? City { get; set; }
}

class Customer
{
    public string? Name { get; set; }
    public Address? HomeAddress { get; set; }
}

Customer? customer = null;

// Without ?. — need to check every step
string city = "Unknown";
if (customer != null && customer.HomeAddress != null && customer.HomeAddress.City != null)
{
    city = customer.HomeAddress.City;
}

// With ?. — one clean line
string city2 = customer?.HomeAddress?.City ?? "Unknown";
```

### `?.` with Methods

```csharp
List<string>? names = null;

// Without ?.
int count = 0;
if (names != null)
{
    count = names.Count;
}

// With ?.
int count2 = names?.Count ?? 0;

// With method calls
names?.Add("Alice");       // Does nothing if names is null
names?.Clear();            // Does nothing if names is null
```

---

## 7. Nullable Reference Types (Concept)

Starting with C# 8, you can enable **nullable reference types** — a feature that helps the compiler warn you about potential null bugs.

In traditional C#, **all** reference types (`string`, classes) can be `null`:

```csharp
string name = null; // Allowed, but dangerous
Console.WriteLine(name.Length); // 💥 NullReferenceException at runtime
```

With nullable reference types enabled (via `#nullable enable` or project settings), the compiler distinguishes between:
- `string` — **not expected** to be null (compiler warns if you try)
- `string?` — **explicitly nullable** (compiler reminds you to check)

```csharp
#nullable enable

string name = "Alice";     // Non-nullable — should never be null
string? nickname = null;    // Nullable — might be null

// Compiler warning: nickname might be null
Console.WriteLine(nickname.Length);  // ⚠️ Warning

// No warning — you checked first
if (nickname != null)
{
    Console.WriteLine(nickname.Length); // ✅ No warning
}
```

> **Note:** This is a compile-time feature only — it doesn't prevent null at runtime. Think of it as the compiler helping you catch bugs before they happen.

---

## 8. Complete Example: Student Roster with Optional Fields

```csharp
enum EnrollmentStatus
{
    Active,
    OnLeave,
    Graduated,
    Withdrawn
}

class Student
{
    public string Name { get; set; }
    public EnrollmentStatus Status { get; set; }
    public int? Age { get; set; }
    public double? Gpa { get; set; }
    public DateTime? GraduationDate { get; set; }

    public string GetSummary()
    {
        string ageStr = Age.HasValue ? $"{Age}" : "Not provided";
        string gpaStr = Gpa.HasValue ? $"{Gpa:F2}" : "N/A";
        string gradStr = GraduationDate?.ToString("yyyy-MM-dd") ?? "N/A";

        return $"{Name} | Status: {Status} | Age: {ageStr} | GPA: {gpaStr} | Graduated: {gradStr}";
    }
}

class Roster
{
    private List<Student> _students = new List<Student>();

    public void Add(Student student)
    {
        _students.Add(student);
    }

    public double? GetAverageGpa()
    {
        List<double> gpas = new List<double>();
        foreach (Student s in _students)
        {
            if (s.Gpa.HasValue)
            {
                gpas.Add(s.Gpa.Value);
            }
        }

        if (gpas.Count == 0) return null;

        double sum = 0;
        foreach (double g in gpas)
        {
            sum += g;
        }
        return sum / gpas.Count;
    }

    public void PrintRoster()
    {
        Console.WriteLine("=== Student Roster ===");
        foreach (Student s in _students)
        {
            Console.WriteLine(s.GetSummary());
        }

        double? avgGpa = GetAverageGpa();
        Console.WriteLine($"\nAverage GPA: {avgGpa?.ToString("F2") ?? "No data"}");
    }
}
```

```csharp
// Program.cs
Roster roster = new Roster();

roster.Add(new Student
{
    Name = "Alice",
    Status = EnrollmentStatus.Active,
    Age = 20,
    Gpa = 3.8
});

roster.Add(new Student
{
    Name = "Bob",
    Status = EnrollmentStatus.OnLeave,
    Age = 22,
    Gpa = null  // On leave, GPA not available
});

roster.Add(new Student
{
    Name = "Charlie",
    Status = EnrollmentStatus.Graduated,
    Age = null, // Didn't provide age
    Gpa = 3.5,
    GraduationDate = new DateTime(2025, 5, 15)
});

roster.Add(new Student
{
    Name = "Dana",
    Status = EnrollmentStatus.Active,
    Age = 19,
    Gpa = 3.9
});

roster.PrintRoster();
```

**Output:**
```
=== Student Roster ===
Alice | Status: Active | Age: 20 | GPA: 3.80 | Graduated: N/A
Bob | Status: OnLeave | Age: 22 | GPA: N/A | Graduated: N/A
Charlie | Status: Graduated | Age: Not provided | GPA: 3.50 | Graduated: 2025-05-15
Dana | Status: Active | Age: 19 | GPA: 3.90 | Graduated: N/A

Average GPA: 3.73
```

---

## Key Takeaways

- **Nullable value types** (`int?`, `double?`, `bool?`) allow value types to represent "no value" with `null`
- Check with `.HasValue` or `!= null` before accessing `.Value`
- The **null-coalescing operator** (`??`) provides a default when something is null: `score ?? 0`
- The **null-coalescing assignment** (`??=`) sets a value only if currently null: `name ??= "Default"`
- The **null-conditional operator** (`?.`) safely navigates chains that might be null: `obj?.Property?.Method()`
- **Nullable reference types** (`string?`) are a compile-time feature that helps catch null bugs early
- Returning `null` from a method (instead of `-1` or throwing) is often cleaner for "not found" scenarios
- Combine nullable types with enums and generics for expressive, type-safe data models

---

## Hands-On Exercises

### Exercise 1 — Null-Coalescing Practice
Create variables: `int? a = 10`, `int? b = null`, `int? c = null`. Use `??` to create a chain that returns the first non-null value for different combinations.

### Exercise 2 — Safe Navigation
Create a `Company` class with a nullable `Address` property. The `Address` class has a nullable `ZipCode` (string). Use `?.` and `??` to safely get the zip code, defaulting to "N/A".

### Exercise 3 — Nullable Search Method
Write a method `FindHighestScore(List<int?> scores)` that returns the highest non-null score as `int?`. Return `null` if no non-null scores exist.

---

[← Previous: Lecture 2 – Enums](./lecture-2.md) | [Back to Week 13 Overview](./README.md)
