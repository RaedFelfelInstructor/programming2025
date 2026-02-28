# Week 10 – Exercises

[← Back to Week 10 Overview](./README.md)

---

These exercises are organized by lecture and difficulty. Work through them in order — each section builds on the previous one.

---

## Section A: Polymorphism (Lecture 1)

### Exercise 1 — Polymorphic Animal Sounds

Create an `Animal` base class with a `Name` property and a `virtual Speak()` method that returns `"..."`. Create three derived classes:

- `Dog` — `Speak()` returns `"Woof!"`
- `Cat` — `Speak()` returns `"Meow!"`
- `Duck` — `Speak()` returns `"Quack!"`

In `Main()`:
1. Create a `List<Animal>` containing one of each animal
2. Loop through the list and print each animal's name and sound

**Expected Output:**
```
Rex says: Woof!
Whiskers says: Meow!
Donald says: Quack!
```

---

### Exercise 2 — Payment Processor

Create a `Payment` base class with an `Amount` property and a `virtual ProcessPayment()` method that returns the amount as-is.

Create three derived classes:
- `CreditCardPayment` — adds a 2.5% processing fee
- `BankTransfer` — no fee (uses base behavior)
- `CryptoPayment` — adds a 1% network fee

In `Main()`:
1. Create a `List<Payment>` with mixed payment types
2. Loop through and print each payment type, original amount, and processed amount
3. Display the total processed amount

**Expected Output (for amounts 100, 250, 75):**
```
CreditCardPayment: $100.00 → $102.50
BankTransfer: $250.00 → $250.00
CryptoPayment: $75.00 → $75.75

Total: $428.25
```

---

### Exercise 3 — Polymorphic Method Parameter

Using the `Shape` hierarchy from Lecture 1 (the non-abstract version with `Circle`, `Rectangle`, `Triangle`):

Write a static method:
```csharp
static void DescribeShape(Shape shape)
```

That prints:
- The shape's type name (use `shape.GetType().Name`)
- The shape's color
- The shape's area (formatted to 2 decimal places)

Call it with three different shape objects.

---

## Section B: Abstract Classes (Lecture 2)

### Exercise 4 — Abstract Shape Conversion

Take the `Shape` class from Lecture 1's complete example and convert it to an abstract class:

1. Mark the class as `abstract`
2. Change `CalculateArea()` from `virtual` (with `return 0`) to `abstract` (no body)
3. Verify that `new Shape("Red")` now causes a compile error
4. Verify that `Circle`, `Rectangle`, and `Triangle` still work correctly
5. Add a new `Hexagon` class that overrides `CalculateArea()` using the formula: `(3√3 / 2) × s²`

---

### Exercise 5 — Appliance Hierarchy

Create an abstract `Appliance` class with:
- Properties: `Brand` (string), `Model` (string)
- Constructor that sets both properties
- Abstract method: `GetPowerUsage()` that returns a string
- A `ToString()` override that includes brand, model, and power usage

Create three derived classes:
- `WashingMachine` — has a `LoadSizeKg` property; `GetPowerUsage()` returns `"{LoadSizeKg * 100} watts"`
- `Refrigerator` — `GetPowerUsage()` always returns `"150 watts (constant)"`
- `Microwave` — has a `PowerLevel` property (1-10); `GetPowerUsage()` returns `"{PowerLevel * 120} watts"`

Create a `List<Appliance>`, add one of each, and print them all.

**Expected Output:**
```
WashingMachine: Samsung WF45 — 500 watts
Refrigerator: LG InstaView — 150 watts (constant)
Microwave: Panasonic NN-SN67H — 960 watts
```

---

### Exercise 6 — Notification System

Create an abstract `Notification` class with:
- Properties: `Recipient` (string), `Message` (string)
- Abstract method: `Send()` (void, prints a delivery message)
- A concrete method: `Preview()` that prints the recipient and message

Create three derived classes:
- `EmailNotification` — `Send()` prints `"📧 Sending email to {Recipient}: {Message}"`
- `SmsNotification` — `Send()` prints `"📱 Sending SMS to {Recipient}: {Message}"`
- `PushNotification` — `Send()` prints `"🔔 Sending push to {Recipient}: {Message}"`

Create a list of mixed notifications and send them all.

---

## Section C: Type Checking and Casting (Lecture 3)

### Exercise 7 — Expression-Bodied Rewrite

Take the `Shape` hierarchy from Lecture 2's complete example (with `GetDetails()`). Rewrite `CalculateArea()` and `GetDetails()` in each derived class using expression-bodied syntax:

```csharp
// Before
public override double CalculateArea()
{
    return Math.PI * Radius * Radius;
}

// After
public override double CalculateArea() => Math.PI * Radius * Radius;
```

Verify the program produces identical output.

---

### Exercise 8 — Type-Specific Employee Report

Using the `Employee` hierarchy from Lecture 1 (`Employee`, `Manager`, `SalesPerson`):

Write a method:
```csharp
static void PrintDetailedReport(List<Employee> employees)
```

That prints each employee's name and pay, then uses `is` pattern matching to print:
- For managers: `"  Bonus: {bonus:C}"`
- For salespeople: `"  Commission Rate: {rate:P0} | Total Sales: {sales:C}"`
- For regular employees: `"  (Standard employee)"`

**Expected Output:**
```
Alice: $3,000.00
  (Standard employee)
Bob: $5,500.00
  Bonus: $1,500.00
Carol: $4,500.00
  Commission Rate: 10% | Total Sales: $20,000.00
```

---

### Exercise 9 — Multi-Level Vehicle Hierarchy

Create this hierarchy:
- Abstract `Vehicle` with `Name` property and abstract `GetDescription()` method
- Abstract `MotorVehicle : Vehicle` with `EngineSizeCC` property
- `Car : MotorVehicle` — `GetDescription()` returns `"{Name}: Car with {EngineSizeCC}cc engine"`
- `Motorcycle : MotorVehicle` — `GetDescription()` returns `"{Name}: Motorcycle with {EngineSizeCC}cc engine"`
- `Bicycle : Vehicle` with `GearCount` property — `GetDescription()` returns `"{Name}: Bicycle with {GearCount} gears"`

In `Main()`:
1. Create a `List<Vehicle>` with mixed types
2. Loop through, printing each description
3. Use `is MotorVehicle mv` to also print engine sizes for motorized vehicles only

---

## Section D: Combined Challenges

### Exercise 10 — School Grading System

Design an abstract `Assessment` class with:
- Properties: `StudentName`, `MaxScore`
- Abstract method: `CalculateScore()` returns `double`
- Concrete method: `GetGrade()` returns a letter grade based on `CalculateScore() / MaxScore * 100`

Create:
- `Exam` — has `PointsEarned`; `CalculateScore()` returns `PointsEarned`
- `Project` — has `FunctionalityScore`, `DesignScore`, `DocumentationScore`; `CalculateScore()` returns their average
- `Participation` — has `ClassesAttended`, `TotalClasses`; `CalculateScore()` returns `(ClassesAttended / TotalClasses) * MaxScore`

Grade scale: A (90+), B (80-89), C (70-79), D (60-69), F (below 60).

Create a mixed list of assessments and print a report card showing each assessment, score, percentage, and grade.

---

### Exercise 11 — Streaming Service Content

Create an abstract `Content` class with `Title`, `Year`, and an abstract `GetPlayTime()` method (returns a string). Create:

- `Movie` — has `RuntimeMinutes`
- `TvSeries` — has `Seasons` and `EpisodesPerSeason` and `EpisodeLengthMinutes`
- `Documentary` — has `Parts` and `PartLengthMinutes`

Add a concrete method `IsRecent()` that returns `true` if `Year >= 2020`.

Create a list of 5+ content items. Display all items, then display only recent items, then use type checking to calculate and display total watch time for TV series only.

---

### Exercise 12 — Restaurant Order System

Design a system with:
- Abstract `MenuItem` with `Name`, `BasePrice`, and abstract `CalculateTotal()`
- `FoodItem` — has `IsVegetarian`; `CalculateTotal()` adds 8% tax
- `Beverage` — has `Size` (string: "S", "M", "L"); `CalculateTotal()` adds 5% tax, and large beverages add a $0.50 surcharge
- `Dessert` — has `IsSpecial`; `CalculateTotal()` adds 8% tax, and specials get a 10% premium

Create a list of 6+ menu items. Print a receipt showing:
1. All items with calculated totals
2. A subtotal
3. Separate counts and subtotals for food, beverages, and desserts (use type checking)
4. An order total

---

### Exercise 13 — Geometry Toolkit 🏆

Build a comprehensive geometry toolkit:
- Abstract `Shape` with `Color` property, abstract `CalculateArea()`, abstract `CalculatePerimeter()`, and `ToString()` override
- `Circle` — area: πr², perimeter: 2πr
- `Rectangle` — standard formulas; add `IsSquare()` method
- `Triangle` — takes 3 sides; area using Heron's formula: √(s(s-a)(s-b)(s-c)) where s = (a+b+c)/2; perimeter: a+b+c; add `IsEquilateral()` method
- `Parallelogram` — takes base, side, height; area: base × height; perimeter: 2(base + side)

Create a list of 6+ shapes. Produce a report that:
1. Lists all shapes with area and perimeter
2. Shows the shape with the largest area
3. Shows the shape with the largest perimeter
4. Lists only squares (use type checking + `IsSquare()`)
5. Lists only equilateral triangles (use type checking + `IsEquilateral()`)

---

[← Back to Week 10 Overview](./README.md)
