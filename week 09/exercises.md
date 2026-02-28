# Week 9 – Exercises: Inheritance

[← Back to Week 9 Overview](./README.md)

---

## How to Use These Exercises

Work through the sections in order — they follow the lecture progression. Each section builds on the previous one. Try every exercise before looking at hints.

---

## Section A: Basic Inheritance (Lecture 1)

### Exercise 1 — Vehicle Hierarchy
Create a `Vehicle` base class with properties `Make`, `Model`, and `Year`. Add a `Describe()` method that prints `"2023 Toyota Camry"`. Then create:
- `Car` with an additional `NumberOfDoors` property
- `Motorcycle` with an additional `HasSidecar` (bool) property

Create one of each and call `Describe()` on both.

---

### Exercise 2 — Food Hierarchy
Create a `Food` base class with `Name` (string) and `Calories` (int). Add a method `PrintNutrition()` that displays the name and calories. Then create:
- `Fruit` with a `Vitamin` property (e.g., "Vitamin C")
- `Grain` with an `IsWholeGrain` (bool) property

Create a `List<Food>` with a mix of `Fruit` and `Grain` objects (hint: a `Fruit` *is a* `Food`, so it can go in a `List<Food>`). Loop through and call `PrintNutrition()` on each.

---

### Exercise 3 — Inheritance Diagram
Look at this code and draw the inheritance hierarchy (which class inherits from which):

```csharp
class Appliance { }
class KitchenAppliance : Appliance { }
class Toaster : KitchenAppliance { }
class Blender : KitchenAppliance { }
class WashingMachine : Appliance { }
```

Then answer: Is a `Toaster` an `Appliance`? Is a `WashingMachine` a `KitchenAppliance`?

---

### Exercise 4 — Is-A Test
For each pair, decide if inheritance is appropriate. Explain your reasoning.

1. `Rectangle` and `Shape`
2. `Engine` and `Car`
3. `SavingsAccount` and `BankAccount`
4. `Wheel` and `Bicycle`
5. `Laptop` and `Computer`
6. `Address` and `Person`

---

## Section B: Constructors and `protected` (Lecture 2)

### Exercise 5 — Product Hierarchy with Constructors
Create a `Product` base class with:
- Properties: `Name`, `Price` (decimal)
- Constructor that takes both parameters
- A `PrintProduct()` method

Create two derived classes:
- `Book` with `Author` and `PageCount` — constructor takes all 4 values and calls `base(name, price)`
- `Electronics` with `Brand` and `WarrantyMonths` — constructor takes all 4 values and calls `base(name, price)`

Create one of each and display their information.

---

### Exercise 6 — Protected Setter Practice
Create a `GameCharacter` class with:
- `Name` (public get, public set)
- `Health` (public get, **protected** set) — initialized to 100
- `Level` (public get, **protected** set) — initialized to 1

Constructor takes a name. Add a `PrintStatus()` method.

Create a `Warrior` derived class with:
- `Armor` (int) property
- `TakeDamage(int damage)` method that reduces Health (minimum 0), reducing damage by Armor amount first
- `LevelUp()` method that increases Level by 1 and adds 20 to Health

Test by creating a warrior, dealing damage, and leveling up.

---

### Exercise 7 — Constructor Chain Trace
Predict the **exact output** (including order) of the following code:

```csharp
class Vehicle
{
    public string Type { get; set; }

    public Vehicle(string type)
    {
        Type = type;
        Console.WriteLine($"Vehicle constructor: {type}");
    }
}

class Car : Vehicle
{
    public int Doors { get; set; }

    public Car(string type, int doors) : base(type)
    {
        Doors = doors;
        Console.WriteLine($"Car constructor: {doors} doors");
    }
}

class ElectricCar : Car
{
    public int BatteryCapacity { get; set; }

    public ElectricCar(string type, int doors, int battery) : base(type, doors)
    {
        BatteryCapacity = battery;
        Console.WriteLine($"ElectricCar constructor: {battery} kWh");
    }
}

ElectricCar tesla = new ElectricCar("Sedan", 4, 75);
Console.WriteLine($"\nResult: {tesla.Type}, {tesla.Doors} doors, {tesla.BatteryCapacity} kWh");
```

---

### Exercise 8 — Multiple Constructors
Create a `Person` class with `Name` and `Age`, with two constructors:
1. `Person(string name, int age)` — sets both
2. `Person(string name)` — sets name and defaults age to 0

Create a `Student` class with `Gpa`, with three constructors:
1. `Student(string name, int age, double gpa)` — calls `base(name, age)`
2. `Student(string name, double gpa)` — calls `base(name)`, sets GPA
3. `Student(string name)` — calls `base(name)`, defaults GPA to 0.0

Test all three constructors and print the results.

---

## Section C: Method Overriding (Lecture 3)

### Exercise 9 — Payment Hierarchy
Create a `Payment` base class with:
- Properties: `Amount` (decimal), `Date` (string)
- Constructor with both parameters
- `virtual` method `ProcessPayment()` that prints `"Processing payment of $X on [date]"`
- `override ToString()` returning `"Payment: $X on [date]"`

Create derived classes:
- `CreditCardPayment` with `CardNumber` (string, last 4 digits) — override `ProcessPayment()` to add `"Charging card ending in XXXX"`
- `CashPayment` — override `ProcessPayment()` to add `"Cash received. Change: $X"` (calculate change from a `CashGiven` property)

Test both payment types.

---

### Exercise 10 — ToString() Override Chain
Create this hierarchy where each `ToString()` builds on its parent:

```
Appliance → ToString(): "[Brand] Appliance"
    └── WashingMachine → ToString(): "[Brand] Washing Machine - [Capacity]kg"
        └── SmartWashingMachine → ToString(): "[Brand] Smart Washing Machine - [Capacity]kg (WiFi: [Yes/No])"
```

Each derived `ToString()` should call `base.ToString()` and extend it. (Hint: the derived class will need to replace "Appliance" with more specific text — consider building the string differently or just constructing from the properties directly.)

---

### Exercise 11 — Virtual Method Design
Create a `Notification` base class with:
- `Recipient` property
- `Message` property
- `virtual void Send()` that prints `"Sending notification to [Recipient]: [Message]"`

Create three derived classes:
- `EmailNotification` with `Subject` — override `Send()` to print email format
- `SmsNotification` with `PhoneNumber` — override `Send()` to show character count
- `PushNotification` with `AppName` — override `Send()` to show app name

Test all three. Example outputs:
```
📧 Email to alice@email.com
   Subject: Meeting Reminder
   Body: Don't forget the meeting at 3pm

📱 SMS to 555-0123 (42 chars)
   Don't forget the meeting at 3pm

🔔 Push via Calendar App to Bob
   Don't forget the meeting at 3pm
```

---

## Section D: Combined Challenges

### Exercise 12 — Library Catalog
Design a library system with:

**Base class `LibraryItem`:**
- Properties: `Title`, `Year`, `IsCheckedOut` (bool)
- Constructor, `CheckOut()` and `Return()` methods
- `virtual GetDetails()` method
- `override ToString()`

**Derived classes:**
- `Book` — adds `Author`, `Pages`
- `DVD` — adds `Director`, `RuntimeMinutes`
- `Magazine` — adds `Issue` (string), `Publisher`

Each derived class overrides `GetDetails()` and `ToString()`.

Create a `List<LibraryItem>` with a mix of all types. Print all items, check out a few, and print again showing their status.

---

### Exercise 13 — School System
Build a school system hierarchy:

**Base class `Person`:**
- Properties: `Name`, `Email`, `Id`
- Constructor with `base()` chaining
- `virtual PrintInfo()` and `override ToString()`

**Derived classes:**
- `Student` — adds `Gpa`, `Major`, `EnrollmentYear`
- `Teacher` — adds `Department`, `YearsExperience`, `Salary` (protected set)
- `Staff` — adds `Role`, `Department`

Create a list with a mix of all three types. Print everyone's info using their overridden `PrintInfo()` method. Then filter and print only students with GPA above 3.5 (use a loop with type checking: `if (person is Student s)` — we'll cover this more in Week 10, but try it here).

---

### Exercise 14 — Banking System (Advanced)
Create a banking hierarchy:

**Base class `Account`:**
- Properties: `AccountNumber`, `Owner`, `Balance` (protected set)
- Constructor with initial balance
- `virtual Deposit(decimal amount)` and `virtual Withdraw(decimal amount)` (returns bool)
- `override ToString()`

**Derived classes:**
- `CheckingAccount` — no overdraft allowed (withdraw returns `false` if insufficient funds)
- `SavingsAccount` — adds `InterestRate`, `ApplyInterest()` method, withdraw has a `MinimumBalance` restriction
- `CreditAccount` — adds `CreditLimit`, allows "withdrawing" up to the credit limit beyond 0 balance

Each derived class overrides `Withdraw()` with its own rules and calls `base.Deposit()` where appropriate. Add `ToString()` overrides.

Create one of each account type. Perform several deposits and withdrawals, showing the balance after each transaction.

---

## Difficulty Guide

| Exercises | Difficulty | Concepts |
|-----------|-----------|----------|
| 1–4 | ⭐ Basic | Inheritance syntax, "is-a" test |
| 5–8 | ⭐⭐ Intermediate | Constructor chaining, `protected`, multiple constructors |
| 9–11 | ⭐⭐ Intermediate | `virtual`/`override`, `base` calls, `ToString()` |
| 12–14 | ⭐⭐⭐ Challenging | Full hierarchies, design decisions, integration |

---

## Solutions

Try every exercise **on your own first** before looking at solutions. If you're stuck, re-read the relevant lecture section, then try again. Getting stuck and working through it is how you learn.

Solutions will be discussed in class.

---

[← Back to Week 9 Overview](./README.md)
