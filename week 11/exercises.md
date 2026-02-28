# Week 11 – Exercises: Interfaces and Object Composition

[← Back to Week 11 Overview](./README.md)

---

## Section A: Interfaces Basics (Lecture 1)

### Exercise 1 — IDescribable
Define an interface `IDescribable` with a single method `string GetDescription()`. Create three classes — `Book` (Title, Author), `Movie` (Title, Director, Year), and `City` (Name, Country, Population) — that each implement the interface. Store them in a `List<IDescribable>` and print each description.

**Expected output:**
```
"The Great Gatsby" by F. Scott Fitzgerald
"Inception" directed by Christopher Nolan (2010)
Tokyo, Japan — Population: 13,960,000
```

### Exercise 2 — IResizable
Define an interface `IResizable` with a method `void Resize(double factor)` and a read-only property `double Area { get; }`. Implement it in `Circle` (radius) and `Rectangle` (width, height) classes. Write a method `static void DoubleSize(IResizable shape)` that resizes the shape by 2x and prints the new area. Test with both shapes.

### Exercise 3 — Interface vs Abstract Class
Design a system with `Dog`, `Cat`, `Robot`, and `Car`. Some can move, some can make sounds, and some are alive. Use the "is-a" vs "can-do" tests to decide what should be an abstract class and what should be an interface. Implement your design with at least:
- An abstract class `LivingThing` with `Name` and abstract `Eat()`
- An interface `IMovable` with `void Move()`
- An interface `ISoundMaker` with `void MakeSound()`

Create one instance of each type and demonstrate the interface polymorphism.

### Exercise 4 — IPrintable
Define an interface `IPrintable` with `void PrintFormatted()` and `int PageCount { get; }`. Implement it in `Report` (Title, Content, uses word count / 250 for page count), `Invoice` (InvoiceNumber, Amount, always 1 page), and `Manuscript` (Title, ChapterCount, 15 pages per chapter). Write a method that takes a `List<IPrintable>`, prints each item, and displays the total page count.

---

## Section B: Multiple Interfaces and Patterns (Lecture 2)

### Exercise 5 — Multiple Interfaces
Create interfaces `IPlayable` (with `void Play()`) and `IRecordable` (with `void Record()` and `bool IsRecording { get; }`). Create:
- `Song` — implements `IPlayable` only
- `Podcast` — implements both `IPlayable` and `IRecordable`
- `VoiceMemo` — implements `IRecordable` only

Store everything in a list of objects. Use `is` to find all playable items and play them, then find all recordable items and start recording.

### Exercise 6 — IComparable Student
Create a `Student` class with `Name`, `Gpa`, and `Credits` properties that implements `IComparable<Student>`. Students should be compared by GPA (highest first). If GPAs are equal, compare by Credits (highest first). Create a list of 6 students, sort them, and display the ranking.

**Expected output format:**
```
=== Student Rankings ===
1. Alice — GPA: 3.95, Credits: 90
2. Bob — GPA: 3.80, Credits: 60
3. Carol — GPA: 3.80, Credits: 45
...
```

### Exercise 7 — Notification System Extension
Create an `INotifiable` interface with `string ContactInfo { get; }` and `void Notify(string message)`. Implement it in:
- `EmailUser` — prints "📧 Email to {address}: {message}"
- `SmsUser` — prints "📱 SMS to {phone}: {message}"
- `SlackUser` — prints "💬 Slack to @{username}: {message}"

Create a `NotificationManager` class with:
- `void AddRecipient(INotifiable recipient)`
- `void BroadcastAll(string message)` — sends to all recipients
- `INotifiable FindByContact(string contact)` — returns first match or null

### Exercise 8 — ISearchable
Define an interface `ISearchable<T>` with `List<T> Search(string query)` and `int Count { get; }`. Implement it in:
- `ContactBook` — searches contacts by name
- `ProductCatalog` — searches products by name or description

Each class should store its own internal list and filter items based on the search query (case-insensitive substring match). Demonstrate searching across both.

---

## Section C: Composition (Lecture 3)

### Exercise 9 — Computer Builder
Starting from the `Computer` composition example (Lecture 3), add:
- A `GraphicsCard` class with `Model` and `MemoryGb`
- An optional `GraphicsCard` property on `Computer` (can be `null`)
- Update `PrintSpecs()` to show "(Integrated)" when no graphics card is present

Create two computers: a gaming PC with a graphics card and an office PC without one.

### Exercise 10 — Music Player
Create a composition-based music player:
- `Song` class with `Title`, `Artist`, `DurationSeconds`
- `Playlist` class that holds a `List<Song>` with methods: `Add(Song)`, `Remove(int index)`, `GetSong(int index)`, `int Count`
- `MusicPlayer` class that **has a** `Playlist` and tracks `CurrentSongIndex`

The `MusicPlayer` should support:
- `void Play()` — prints "Now playing: {Title} by {Artist}"
- `void Next()` — moves to next song (wraps to start)
- `void Previous()` — moves to previous song (wraps to end)
- `void ShowQueue()` — shows all songs with `>` marker on current

**Expected output:**
```
Now playing: Bohemian Rhapsody by Queen

Queue:
> 1. Bohemian Rhapsody by Queen [5:55]
  2. Stairway to Heaven by Led Zeppelin [8:02]
  3. Hotel California by Eagles [6:31]
```

### Exercise 11 — Restaurant
Model a restaurant using composition:
- `MenuItem` class with `Name`, `Price`, `Category` (string: "Appetizer", "Main", "Dessert", "Drink")
- `Menu` class that holds a `List<MenuItem>` with methods to get items by category
- `Order` class that holds ordered items with `AddItem(MenuItem)`, `RemoveItem(int index)`, `GetTotal()`, `PrintReceipt()`
- `Restaurant` class that **has a** `Menu` and can create `Order` objects

Demonstrate creating a menu, placing an order with several items, and printing the receipt.

---

## Section D: Combined Challenges

### Exercise 12 — Library System
Build a library system combining all three OOP concepts:

**Interfaces:**
- `IBorrowable` with `void CheckOut(string borrower)`, `void Return()`, `bool IsAvailable { get; }`, `string Borrower { get; }`

**Inheritance:**
- Abstract class `LibraryItem` with `Title`, `Year`, abstract `string GetDetails()`
- `Book` extends `LibraryItem` — adds `Author`, `Isbn`
- `Dvd` extends `LibraryItem` — adds `Director`, `DurationMinutes`
- `Magazine` extends `LibraryItem` — adds `IssueNumber`, `Publisher`

**Composition:**
- `Library` class that **has a** `List<LibraryItem>` with methods for adding items, checking out, returning, and searching

All three subclasses should implement `IBorrowable`. Demonstrate:
- Adding several items to the library
- Checking out a book and a DVD
- Trying to check out an already borrowed item (print an error)
- Returning an item
- Searching by title (case-insensitive)
- Listing all available items and all borrowed items

### Exercise 13 — Vehicle Fleet 🏆
Design a vehicle fleet management system:

**Interfaces:**
- `IFuelable` with `double FuelLevel { get; }`, `void Refuel(double amount)`, `double MaxFuel { get; }`
- `IElectric` with `double BatteryLevel { get; }`, `void Charge(double amount)`, `double MaxBattery { get; }`
- `IMaintenable` with `DateTime LastServiceDate { get; }`, `bool NeedsService()`, `void PerformService()`

**Classes:**
- `GasCar` — implements `IFuelable` and `IMaintenable`
- `ElectricCar` — implements `IElectric` and `IMaintenable`
- `HybridCar` — implements `IFuelable`, `IElectric`, and `IMaintenable`

**Composition:**
- `Fleet` class that **has a** `List<object>` (or better, a common base/interface) and provides:
  - `void AddVehicle(...)` 
  - `void RefuelAll()` — refuels all `IFuelable` vehicles
  - `void ChargeAll()` — charges all `IElectric` vehicles
  - `void ServiceDue()` — lists all vehicles that need service
  - `void PrintFleetStatus()` — prints status of every vehicle

Each vehicle should also use composition for a `ServiceRecord` component that tracks service history.

Demonstrate: adding mixed vehicles, refueling gas and hybrid cars, charging electric and hybrid cars, checking service status, and printing the full fleet report.

---

[← Back to Week 11 Overview](./README.md)
