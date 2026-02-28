# Week 13 – Practice Exercises

[← Back to Week 13 Overview](./README.md)

---

These exercises cover all three topics from this week: generics, enums, and nullable types. They're organized by difficulty — start with Section A and work your way up.

---

## Section A: Fundamentals

### Exercise 1 — Word Counter (Dictionary)
Create a program that reads a sentence from the user, splits it into words, and counts how many times each word appears using a `Dictionary<string, int>`. Display the results alphabetically.

**Example Input:** `"the cat sat on the mat the cat"`

**Expected Output:**
```
cat: 2
mat: 1
on: 1
sat: 1
the: 3
```

---

### Exercise 2 — Browser History (Stack)
Simulate browser back/forward navigation. Use a `Stack<string>` for back history and another for forward history. Start on "Home". Let the user:
- Type a URL to visit a new page (clears forward history)
- Type `back` to go back
- Type `forward` to go forward
- Type `quit` to exit

Display the current page after each action.

---

### Exercise 3 — Day Planner (Enum)
Define a `DayOfWeek` enum (Monday through Sunday). Write a method that takes a `DayOfWeek` and returns whether it's a weekday or weekend. Write another method that returns a suggested activity for each day. Print all 7 days with their type and activity.

**Expected Output:**
```
Monday: Weekday — Focus on deep work
Tuesday: Weekday — Team meetings
...
Saturday: Weekend — Outdoor activities
Sunday: Weekend — Rest and recharge
```

---

### Exercise 4 — Temperature Readings (Nullable)
Create a `double?[]` of 7 temperature readings where some are `null` (sensor was offline). Write methods to:
- Count how many readings are available (not null)
- Calculate the average of available readings
- Find the highest reading (return `null` if no readings)

**Example Array:** `{ 72.5, null, 68.3, null, 75.1, 70.8, null }`

---

### Exercise 5 — Phone Book (Dictionary)
Create a phone book using `Dictionary<string, string>`. Implement a menu with options to:
1. Add a contact (name → phone number)
2. Look up a number by name
3. Remove a contact
4. Display all contacts
5. Exit

Handle duplicate names by asking the user if they want to update the existing entry.

---

## Section B: Intermediate

### Exercise 6 — Generic Min/Max Finder
Write a generic method `FindMinMax<T>(List<T> items, out T min, out T max)` where `T : IComparable<T>`. Test it with `List<int>`, `List<double>`, and `List<string>`.

> **Hint:** Use `CompareTo()` — it returns negative if less than, 0 if equal, positive if greater than.

---

### Exercise 7 — Task Manager with Enums
Create a `TaskItem` class with:
- `Title` (string)
- `Status` (enum: NotStarted, InProgress, Completed, OnHold)
- `Priority` (enum: Low, Medium, High, Critical)

Store tasks in a `List<TaskItem>`. Implement:
- Add a task
- Change a task's status (only allow valid transitions: NotStarted → InProgress → Completed, any state → OnHold)
- Display all tasks grouped by status
- Display tasks filtered by priority

---

### Exercise 8 — Print Queue Simulator
Simulate a print queue using `Queue<T>` with a custom `PrintJob` class:
- `PrintJob` has: `DocumentName`, `Pages`, `Priority` (enum: Normal, Rush)

Implement:
- Add jobs to the queue
- Process (dequeue) the next job, displaying its details
- Show all pending jobs
- Count total pages pending

---

### Exercise 9 — Survey Results (Nullable)
Model survey responses where users can skip questions. Create a `SurveyResponse` class with:
- `RespondentName` (string)
- `Age` (int?)
- `Rating` (int?) — 1 to 5
- `WouldRecommend` (bool?)

Create a list of 5 responses (some with null values). Write methods to:
- Count respondents who provided an age
- Calculate average rating (ignoring nulls)
- Count how many would recommend (where `WouldRecommend == true`)
- Display a summary report

---

### Exercise 10 — Generic Stack Implementation
Write your own `SimpleStack<T>` class (without using `Stack<T>`) using a `List<T>` internally. Implement:
- `Push(T item)`
- `Pop()` — throws if empty
- `Peek()` — throws if empty
- `Count` property
- `IsEmpty` property

Test with at least two different types.

---

## Section C: Advanced

### Exercise 11 — Inventory System
Build an inventory system using `Dictionary<string, (int Quantity, decimal Price)>` where the key is the product name. Implement:
- Add product (or increase quantity if it exists)
- Remove product (decrease quantity; remove entry if quantity reaches 0)
- Check stock for a specific product
- Display full inventory sorted by product name
- Calculate total inventory value

> **Hint:** Value tuples `(int Quantity, decimal Price)` work as dictionary values.

---

### Exercise 12 — State Machine
Create a generic `StateMachine<TState>` class where `TState : Enum`. It should:
- Track the current state
- Accept a dictionary of valid transitions: `Dictionary<TState, List<TState>>`
- Have a `TransitionTo(TState newState)` method that only allows valid transitions (throws otherwise)
- Keep a `Stack<TState>` history for undo support
- Have an `Undo()` method that reverts to the previous state

Test it with an `OrderStatus` enum (Pending → Processing → Shipped → Delivered, any → Cancelled).

---

### Exercise 13 — Grade Book System
Create a complete grade book that combines all three topics:
- `Subject` enum (Math, Science, English, History, Art)
- `GradeBook` class using `Dictionary<string, Dictionary<Subject, List<int?>>>` — student name → subject → list of grades (nullable for excused absences)
- Methods:
  - Add a grade for a student in a subject
  - Add a null grade (excused absence)
  - Get a student's average for a subject (ignoring nulls)
  - Get the class average for a subject
  - Get a student's overall average across all subjects
  - Print a full report card for a student

---

## Challenge Problems

### Challenge 1 — Generic Repository
Create a generic `Repository<T>` class that can store, retrieve, and manage any type of entity. Requirements:
- `T` must have an `Id` property (use an interface `IEntity` with `int Id { get; }`)
- Use `Dictionary<int, T>` for storage
- Methods: `Add(T entity)`, `GetById(int id)` (returns `T?`), `GetAll()`, `Delete(int id)`, `Update(T entity)`, `Count`
- Create two entity types (e.g., `Product` and `Customer`) and test with both

### Challenge 2 — Expression Evaluator with Undo
Build a calculator that:
- Uses a `Stack<double>` for operand history
- Uses an `enum Operation { Add, Subtract, Multiply, Divide }`
- Supports undo (reverts the last operation)
- Uses `double?` for the result (null if no operations performed)
- Tracks operation history using `Queue<(Operation Op, double Operand)>`

### Challenge 3 — Configuration Manager
Create a `ConfigManager` class that:
- Stores settings as `Dictionary<string, string?>` (nullable values for unset settings)
- Has an `enum SettingCategory { Display, Audio, Network, Security }`
- Groups settings by category using `Dictionary<SettingCategory, List<string>>`
- Provides `GetSetting(string key)` returning `string?`
- Provides `GetSettingOrDefault(string key, string defaultValue)` using `??`
- Has `SetSetting(string key, string? value)` — passing `null` clears the setting
- Implements `ResetCategory(SettingCategory category)` — sets all settings in a category to null
- Prints a summary showing set vs unset settings per category

---

[← Back to Week 13 Overview](./README.md)
