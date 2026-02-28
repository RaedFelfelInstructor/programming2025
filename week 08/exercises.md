# Week 8 – Practice Exercises

[← Back to Week 8 Overview](./README.md)

---

These exercises reinforce the concepts from all three lectures this week. Work through them in order — they build in complexity from basic encapsulation to multi-class design.

---

## Section A: Access Modifiers and Encapsulation Basics

### Exercise 1 — Access Modifier Identification

For each class member below, state whether the access is **allowed** or **will cause a compiler error** when accessed from `Main`:

```csharp
class Employee
{
    private int employeeId;
    public string Name { get; set; }
    public decimal Salary { get; private set; }
    protected string Department;
    internal string Office { get; set; }

    public Employee(int id, string name, decimal salary)
    {
        employeeId = id;
        Name = name;
        Salary = salary;
    }

    private void CalculateBonus() { }
    public void PrintInfo() { }
}

// In Main:
Employee emp = new Employee(1, "Alice", 50000m);
Console.WriteLine(emp.Name);          // a)
Console.WriteLine(emp.employeeId);    // b)
emp.Salary = 60000m;                  // c)
emp.PrintInfo();                      // d)
emp.CalculateBonus();                 // e)
Console.WriteLine(emp.Department);    // f)
emp.Office = "Room 302";             // g)
```

---

### Exercise 2 — Encapsulate a Rectangle

Transform this class to use proper encapsulation:

```csharp
class Rectangle
{
    public double Width;
    public double Height;
}
```

Requirements:
- Both `Width` and `Height` must be greater than 0
- Use warning messages for invalid values (keep the old value)
- Add computed properties: `Area`, `Perimeter`, `IsSquare`
- Add a constructor that takes width and height
- Add `ToString()` that returns: `"Rectangle: 5.0 x 3.0 (Area: 15.0)"`

Test:
```csharp
Rectangle r = new Rectangle(5, 3);
Console.WriteLine(r);            // Rectangle: 5.0 x 3.0 (Area: 15.0)
Console.WriteLine(r.Perimeter);  // 16
Console.WriteLine(r.IsSquare);   // False
r.Width = -2;                    // Warning message
Console.WriteLine(r.Width);      // 5 (unchanged)
```

---

### Exercise 3 — Password-Protected Class

Create a `SecureNote` class with:
- `Title` (public get/set, cannot be empty)
- Private `content` field
- Private `password` field (set in constructor, never changeable)
- `SetContent(string password, string newContent)` — only works with correct password
- `GetContent(string password)` — returns content if password matches, otherwise returns `"Access Denied"`
- `ToString()` — shows title but NOT the content

```csharp
SecureNote note = new SecureNote("My Diary", "secret123");
note.SetContent("secret123", "Today was a good day.");
Console.WriteLine(note.GetContent("wrong"));       // Access Denied
Console.WriteLine(note.GetContent("secret123"));   // Today was a good day.
Console.WriteLine(note);                            // SecureNote: "My Diary" [Protected]
```

---

### Exercise 4 — Counter Class

Create an encapsulated `Counter` class with:
- `Value` property (read-only from outside, starts at 0)
- `Increment()` method — adds 1
- `Decrement()` method — subtracts 1, but cannot go below 0
- `Reset()` method — sets value back to 0
- `ToString()` — returns `"Counter: 5"`

Test all methods, including trying to decrement below 0.

---

## Section B: Validation and Behavior

### Exercise 5 — Email Validator

Create a `UserAccount` class with:
- `Username` — 3 to 20 characters, letters and numbers only
- `Email` — must contain exactly one `@` and at least one `.` after the `@`
- `IsActive` — boolean, defaults to `true`
- `Deactivate()` and `Activate()` methods
- Validation messages for invalid inputs
- `ToString()` showing username, email, and status

```csharp
UserAccount user = new UserAccount("alice_j", "alice@email.com");
Console.WriteLine(user);  // alice_j (alice@email.com) [Active]

user.Email = "invalid";   // Warning: Invalid email format
user.Username = "ab";     // Warning: Username must be 3-20 characters
user.Deactivate();
Console.WriteLine(user);  // alice_j (alice@email.com) [Inactive]
```

> **Note:** The email validation here is simplified for learning. Real email validation is far more complex!

---

### Exercise 6 — Stopwatch Class

Create a `Stopwatch` class that simulates a stopwatch:
- `IsRunning` property (read-only from outside)
- `ElapsedSeconds` property (read-only from outside)
- `Start()` — records the start time (use `DateTime.Now`)
- `Stop()` — calculates elapsed time, adds to total
- `Reset()` — clears elapsed time (must be stopped first)
- `ToString()` — shows formatted time like `"00:05:23"` (hours:minutes:seconds)

Validation: Can't start if already running. Can't stop if not running. Can't reset while running.

```csharp
Stopwatch sw = new Stopwatch();
sw.Start();
Thread.Sleep(2000);  // Wait 2 seconds (add: using System.Threading;)
sw.Stop();
Console.WriteLine(sw);  // Approximately 00:00:02
```

---

### Exercise 7 — Grade Calculator

Create a `CourseGrade` class with:
- `StudentName` (validated)
- Private list of scores (each between 0 and 100)
- `AddScore(double score)` — validates and adds
- `Average` — computed property
- `HighestScore` and `LowestScore` — computed properties
- `LetterGrade` — computed from average (A/B/C/D/F)
- `ToString()` — `"Alice — Average: 87.5% (B)"`

Test with at least 5 scores, including an attempt to add an invalid score.

---

### Exercise 8 — Task Tracker

Create a `Task` class with:
- `Title`, `Description`, `Priority` (1-5, with validation clamping)
- `IsComplete` (read-only, changed via `Complete()` method)
- `CreatedDate` (read-only, set automatically in constructor to `DateTime.Now`)
- `ToString()` showing all info with a checkbox: `"[✓] Buy groceries (Priority: 3)"`

Create 5 tasks, complete some, and print them all.

---

## Section C: Object Interaction

### Exercise 9 — Wallet and Money

Create a `Money` class with `Amount` (decimal, must be ≥ 0) and `Currency` (string, e.g., "USD"). Add `ToString()`.

Create a `Wallet` class with:
- Owner name
- Private `List<Money>` for different currencies
- `AddMoney(Money money)` — adds to existing amount if same currency, or adds new entry
- `GetBalance(string currency)` — returns amount for that currency
- `PrintContents()` — shows all money in the wallet

```csharp
Wallet wallet = new Wallet("Alice");
wallet.AddMoney(new Money(50.00m, "USD"));
wallet.AddMoney(new Money(30.00m, "EUR"));
wallet.AddMoney(new Money(20.00m, "USD"));  // Should combine with existing USD
wallet.PrintContents();
// Alice's Wallet:
//   USD: $70.00
//   EUR: €30.00
```

---

### Exercise 10 — Restaurant Order

Create a `MenuItem` class (name, price, category like "Appetizer"/"Main"/"Dessert"/"Drink").

Create an `Order` class with:
- `TableNumber` (int)
- Private `List<MenuItem>` for items ordered
- `AddItem(MenuItem item)` method
- `RemoveItem(string itemName)` method
- `GetSubtotal()`, `GetTax()` (8%), `GetTotal()` methods
- `PrintBill()` — formatted receipt grouped by category

Test: Create a menu of at least 8 items. Build an order with 5+ items from the menu and print the bill.

---

### Exercise 11 — Team Roster

Create a `TeamMember` class with:
- `Name`, `Role` (e.g., "Developer", "Designer", "Manager"), `HoursPerWeek`
- Validation: `HoursPerWeek` between 0 and 60
- `ToString()`

Create a `Team` class with:
- `TeamName` and private list of members
- `AddMember()`, `RemoveMember(string name)`
- `FindByRole(string role)` — returns list of matching members
- `GetTotalHours()` — total hours across all members
- `PrintRoster()` — formatted display with role grouping

---

## Section D: Design Challenges

### Exercise 12 — Inventory Management System

Create a `Product` class with:
- `Id` (read-only), `Name`, `Price` (validated ≥ 0), `Quantity` (validated ≥ 0)
- `TotalValue` computed property
- `Sell(int qty)` — decreases quantity if enough stock, returns `bool`
- `Restock(int qty)` — increases quantity
- `ToString()`

Create an `Inventory` class with:
- Private list of products
- `AddProduct(Product p)` — rejects duplicates (by Id)
- `FindProduct(int id)` — returns product or null
- `GetLowStockProducts(int threshold)` — returns list of products with quantity ≤ threshold
- `GetTotalInventoryValue()` — sum of all products' `TotalValue`
- `PrintReport()` — formatted report with all products and total value

Add at least 8 products, perform sells and restocks, then print the report. Show the low-stock products.

---

### Exercise 13 — Student Club Management

Create a `Student` class (id, name, gpa with validation 0-4, `ToString()`).

Create a `Club` class with:
- `ClubName`, `MinimumGpa` (requirement to join)
- Private list of members
- `AddMember(Student s)` — only if GPA meets minimum
- `RemoveMember(int studentId)`
- `GetAverageGpa()` — average GPA of current members
- `PrintMembers()`
- `ToString()`

Create 3 clubs with different GPA requirements and 8 students. Try adding students to clubs (some should be rejected). Print each club's membership and average GPA.

---

### Exercise 14 — Recipe Book (Advanced)

Create an `Ingredient` class (name, quantity, unit like "cups", "tbsp", "grams").

Create a `Recipe` class with:
- `Name`, `Category` (Breakfast/Lunch/Dinner/Dessert), `PrepTimeMinutes`
- Private `List<Ingredient>`
- `AddIngredient()`, `GetIngredientCount()`
- `ScaleRecipe(double factor)` — multiplies all ingredient quantities by the factor
- `ToString()`, `PrintRecipe()` — full formatted output

Create a `RecipeBook` class with:
- Private `List<Recipe>`
- `AddRecipe()`, `FindByName(string name)`, `FindByCategory(string category)`
- `GetQuickRecipes(int maxMinutes)` — recipes that take ≤ maxMinutes
- `PrintTableOfContents()`

Build a recipe book with at least 5 recipes, search by category, find quick meals, and print a full recipe.

---

## Difficulty Guide

| Exercises | Difficulty | Focus |
|-----------|-----------|-------|
| 1–4 | ⭐ Basic | Access modifiers, basic encapsulation, simple validation |
| 5–8 | ⭐⭐ Intermediate | Validation patterns, behavior methods, computed properties |
| 9–11 | ⭐⭐⭐ Challenging | Object interaction, collections of objects |
| 12–14 | ⭐⭐⭐⭐ Advanced | Multi-class design, full system thinking |

---

[← Back to Week 8 Overview](./README.md)
