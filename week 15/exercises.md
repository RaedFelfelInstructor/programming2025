# Week 15 – Exercises

[Back to Week 15 Overview](./README.md)

---

## Section A: Static Members and Static Classes (Lecture 1)

---

### Exercise 1 — Counter Class

Create a class called `Counter` that tracks how many instances have been created.

**Requirements:**
- A `static` field `TotalCreated` that increments each time a `Counter` is instantiated
- An instance property `Id` that gets assigned the current count at creation time
- A `static` method `PrintTotal()` that displays the total count

**Test it:**
```csharp
Counter c1 = new Counter();
Counter c2 = new Counter();
Counter c3 = new Counter();

Console.WriteLine($"c1 ID: {c1.Id}");  // c1 ID: 1
Console.WriteLine($"c2 ID: {c2.Id}");  // c2 ID: 2
Console.WriteLine($"c3 ID: {c3.Id}");  // c3 ID: 3
Counter.PrintTotal();                   // Total counters created: 3
```

---

### Exercise 2 — StringHelper Static Class

Create a `static class StringHelper` with the following static methods:

| Method | Description |
|--------|-------------|
| `Capitalize(string s)` | Returns the string with the first letter capitalized |
| `WordCount(string s)` | Returns the number of words in the string |
| `Reverse(string s)` | Returns the string reversed |
| `IsPalindrome(string s)` | Returns `true` if the string reads the same forwards and backwards (case-insensitive, ignoring spaces) |

**Expected behavior:**
```csharp
Console.WriteLine(StringHelper.Capitalize("hello world"));  // Hello world
Console.WriteLine(StringHelper.WordCount("The quick brown fox")); // 4
Console.WriteLine(StringHelper.Reverse("Hello"));          // olleH
Console.WriteLine(StringHelper.IsPalindrome("racecar"));   // True
Console.WriteLine(StringHelper.IsPalindrome("A man a plan a canal Panama")); // True
```

---

### Exercise 3 — Scoreboard with Static Tracking

Create a `Player` class for a simple game:

**Requirements:**
- Instance properties: `Name`, `Score` (starts at 0)
- Instance method: `AddPoints(int points)` — adds to the player's score
- Static property: `HighScore` — tracks the highest score across all players
- Static property: `HighScoreHolder` — the name of the player with the highest score
- Static method: `PrintLeaderboard()` — displays the high score information

**Test it:**
```csharp
Player p1 = new Player("Alice");
Player p2 = new Player("Bob");

p1.AddPoints(150);
p2.AddPoints(200);
p1.AddPoints(100);  // Alice now has 250

Player.PrintLeaderboard();
// High Score: 250 by Alice
```

---

### Exercise 4 — Configuration Manager

Create a `static class AppConfig` that simulates application settings:

**Requirements:**
- Static properties: `AppName` (string), `Version` (string), `MaxRetries` (int), `IsDebugMode` (bool)
- A static constructor that sets default values (`"MyApp"`, `"1.0.0"`, `3`, `false`)
- A `static` method `PrintConfig()` that displays all settings
- A `static` method `EnableDebug()` that sets `IsDebugMode` to `true` and `MaxRetries` to `10`

> **Note:** A static constructor runs automatically the first time the class is used. Syntax: `static AppConfig() { ... }`

---

## Section B: Async/Await Concepts (Lecture 2)

---

### Exercise 5 — Identify Sync vs Async

For each scenario below, state whether it should be **synchronous** or **asynchronous**, and explain why in one sentence:

1. Calculating the sum of numbers in an array
2. Downloading a file from the internet
3. Sorting a list of strings alphabetically
4. Reading a large CSV file from disk
5. Querying a database for all users
6. Converting Celsius to Fahrenheit
7. Sending an email
8. Counting the vowels in a string

---

### Exercise 6 — Read the Async Code

Look at the following code and answer the questions below it:

```csharp
public class WeatherService
{
    public async Task<string> GetForecastAsync(string city)
    {
        Console.WriteLine($"Fetching forecast for {city}...");
        await Task.Delay(2000);
        return $"Sunny, 25°C in {city}";
    }
}

class Program
{
    static async Task Main(string[] args)
    {
        var service = new WeatherService();
        
        Console.WriteLine("Starting...");
        string forecast = await service.GetForecastAsync("Amsterdam");
        Console.WriteLine(forecast);
        Console.WriteLine("Done!");
    }
}
```

**Questions:**
1. What is the return type of `GetForecastAsync`?
2. Why is `Main` marked as `async Task` instead of `void`?
3. What does `await Task.Delay(2000)` simulate?
4. In what order do the four `Console.WriteLine` calls execute?
5. If we removed the `await` keyword before `service.GetForecastAsync`, what type would `forecast` be?

---

## Section C: Integration Exercises (Lecture 3)

---

### Exercise 7 — Product Inventory (Mini Integration)

Build a small **Product Inventory** system that uses multiple course concepts.

**Step 1 — Create an enum:**
```csharp
public enum Category { Electronics, Clothing, Food, Books, Other }
```

**Step 2 — Create a `Product` class:**
- Properties: `Id` (auto-incrementing using a static counter), `Name`, `Category`, `Price`, `Quantity`
- Validation: name cannot be empty, price must be positive, quantity must be non-negative
- `ToString()` override: `"[ID] Name — Category — $Price (Qty: N)"`

**Step 3 — Create a static `InventoryReporter` class** with these static methods:
- `PrintAll(List<Product> products)` — displays all products
- `TotalValue(List<Product> products)` — returns the sum of (price × quantity) for all products
- `FindMostExpensive(List<Product> products)` — returns the product with the highest price
- `GetByCategory(List<Product> products, Category cat)` — returns a filtered list

**Step 4 — Test it in `Main`:**

```csharp
var products = new List<Product>
{
    new Product("Laptop", Category.Electronics, 999.99m, 5),
    new Product("T-Shirt", Category.Clothing, 19.99m, 50),
    new Product("C# in Depth", Category.Books, 45.00m, 10),
    new Product("Headphones", Category.Electronics, 79.99m, 20),
    new Product("Coffee Beans", Category.Food, 12.50m, 100)
};

InventoryReporter.PrintAll(products);
Console.WriteLine($"\nTotal inventory value: {InventoryReporter.TotalValue(products):C}");
Console.WriteLine($"Most expensive: {InventoryReporter.FindMostExpensive(products)}");

Console.WriteLine("\nElectronics:");
foreach (var p in InventoryReporter.GetByCategory(products, Category.Electronics))
    Console.WriteLine($"  {p}");
```

---

### Exercise 8 — Shape Calculator with LINQ

Create a system with an abstract `Shape` class, concrete shapes, and use LINQ to analyze them.

**Step 1 — Create the hierarchy:**
- `abstract class Shape` with abstract `Area()` and abstract `Perimeter()` methods, plus a `Name` property
- `Circle` (with `Radius`)
- `Rectangle` (with `Width` and `Height`)
- `Triangle` (with `SideA`, `SideB`, `SideC` — perimeter is sum; area uses Heron's formula)

**Step 2 — Create a `List<Shape>` with at least 6 shapes (mix of types).**

**Step 3 — Use LINQ to:**
1. Find the shape with the largest area
2. Calculate the average area of all shapes
3. Get all shapes with area greater than 50, sorted by area descending
4. Group shapes by type name and show count per type
5. Calculate the total perimeter of all rectangles

> **Heron's formula:** `Area = √(s(s-a)(s-b)(s-c))` where `s = (a+b+c)/2`

---

### Exercise 9 — Student Report with Exception Handling

Build a `StudentGradeService` that manages students and their grades.

**Step 1 — Create a `Student` class:**
- Properties: `Name`, `Grades` (a `List<double>`)
- Methods: `AddGrade(double grade)` (throws `ArgumentException` if grade is not 0–100), `Average()`, `HighestGrade()`, `LowestGrade()`

**Step 2 — Create a custom exception:**
```csharp
public class StudentNotFoundException : Exception
{
    public StudentNotFoundException(string name)
        : base($"Student '{name}' not found.") { }
}
```

**Step 3 — Create a `StudentGradeService` class:**
- `AddStudent(Student student)`
- `GetStudent(string name)` — throws `StudentNotFoundException` if not found
- `GetClassAverage()` — average of all student averages
- `GetTopStudent()` — student with highest average
- `PrintClassReport()` — formatted report of all students with their grades and averages

**Step 4 — In `Main`, demonstrate:**
- Adding students and grades (with valid and invalid grades wrapped in try-catch)
- Searching for a student that doesn't exist (catching `StudentNotFoundException`)
- Printing a full class report

---

## Section D: Challenge Exercises

---

### Exercise 10 — Generic Repository

Create a generic class `Repository<T>` where `T : class` that manages a collection of any reference type.

**Requirements:**
- Methods: `Add(T item)`, `GetAll()`, `Find(Func<T, bool> predicate)`, `Remove(Func<T, bool> predicate)`, `Count`
- Use LINQ internally

**Test with multiple types:**
```csharp
var studentRepo = new Repository<Student>();
studentRepo.Add(new Student("Alice", 3.8));
studentRepo.Add(new Student("Bob", 3.2));

var honors = studentRepo.Find(s => s.Gpa >= 3.5);
Console.WriteLine($"Honor students: {honors.Count}");

var productRepo = new Repository<Product>();
productRepo.Add(new Product("Laptop", 999.99m));
// ... same methods work with any type
```

---

### Exercise 11 — Command Pattern (Bonus)

Create a simple command system using interfaces and polymorphism.

**Step 1 — Define an interface:**
```csharp
public interface ICommand
{
    string Name { get; }
    string Description { get; }
    void Execute();
}
```

**Step 2 — Create several command classes** that implement `ICommand`:
- `GreetCommand` — prints a greeting
- `TimeCommand` — prints the current date and time
- `MathQuizCommand` — asks the user a random math question
- `JokeCommand` — tells a random programming joke from a list

**Step 3 — Create a `CommandRunner`** that stores a `List<ICommand>`, displays a menu of available commands, and lets the user choose which to run. Include a try-catch for each command execution.

This exercise demonstrates: interfaces, polymorphism, `List<T>` of interface types, exception handling, and the open/closed principle (you can add new commands without changing `CommandRunner`).

---

## How to Approach These Exercises

| Section | Difficulty | Estimated Time |
|---------|-----------|----------------|
| A (Static) | ⭐⭐ Moderate | 30–40 min |
| B (Async concepts) | ⭐ Easy | 10–15 min |
| C (Integration) | ⭐⭐⭐ Challenging | 60–90 min |
| D (Challenges) | ⭐⭐⭐⭐ Advanced | 45–60 min |

Start with Section A, work through B, and tackle C exercises as mini-projects. Section D is for students who want an extra challenge.

---

[Back to Week 15 Overview](./README.md)
