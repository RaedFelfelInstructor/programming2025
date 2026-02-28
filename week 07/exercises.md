# Week 7 – Exercises: Classes and Objects

[← Back to Week 7 Overview](./README.md)

---

These exercises reinforce the concepts from all three lectures. Work through them in order — they build from basic class creation to more complex multi-class scenarios.

---

## Section A: Basic Classes and Objects (Lecture 1)

### Exercise 1 — Pet Class
Create a `Pet` class with fields: `Name` (string), `Species` (string), `Age` (int). Add a `Describe()` method that prints something like: `"Buddy is a Dog, 5 years old."` Create at least 3 pet objects and call `Describe()` on each.

---

### Exercise 2 — Movie Class
Create a `Movie` class with fields: `Title`, `Director`, `Year`, `Rating` (double). Add a method `IsClassic()` that returns `true` if the movie was released before 2000. Create an array of 4 movies and print only the classics.

---

### Exercise 3 — Reference vs Value
**Predict the output** before running this code. Then run it to verify.

```csharp
class Counter
{
    public int Count;

    public void Increment()
    {
        Count++;
    }
}

// In Main:
Counter a = new Counter();
a.Count = 10;

Counter b = a;
b.Increment();
b.Increment();

Console.WriteLine($"a.Count = {a.Count}");
Console.WriteLine($"b.Count = {b.Count}");
Console.WriteLine(a == b);
```

**Question:** Why does modifying `b` affect `a`?

---

### Exercise 4 — Point Distance
Create a `Point` class with `X` and `Y` (double) fields. Add a method `DistanceTo(Point other)` that calculates the distance between two points using the formula:

```
distance = √((x₂ - x₁)² + (y₂ - y₁)²)
```

*Hint:* Use `Math.Sqrt()` and `Math.Pow()`.

```csharp
Point p1 = new Point();
p1.X = 0; p1.Y = 0;

Point p2 = new Point();
p2.X = 3; p2.Y = 4;

Console.WriteLine(p1.DistanceTo(p2));  // Should print 5
```

---

## Section B: Properties and Constructors (Lecture 2)

### Exercise 5 — Circle with Validation
Create a `Circle` class with:
- A `Radius` property that validates the value must be positive (> 0)
- A constructor that takes the radius
- Methods: `GetArea()` (π × r²) and `GetCircumference()` (2 × π × r)
- Use `Math.PI` for π

```csharp
Circle c1 = new Circle(5);
Console.WriteLine($"Area: {c1.GetArea():F2}");           // 78.54
Console.WriteLine($"Circumference: {c1.GetCircumference():F2}");  // 31.42

Circle c2 = new Circle(-3);  // Should warn and set radius to 1
```

---

### Exercise 6 — BankAccount Basics
Create a `BankAccount` class with:
- `AccountHolder` (string, auto-property)
- `Balance` (double, private set — can only be changed through methods)
- A constructor that takes the holder name and an initial balance (validate ≥ 0)
- `Deposit(double amount)` method — adds to balance (validate amount > 0)
- `Withdraw(double amount)` method — subtracts from balance (validate: amount > 0 and sufficient funds)
- `PrintStatement()` method that displays the account info

```csharp
BankAccount acc = new BankAccount("Alice", 1000);
acc.Deposit(500);
acc.Withdraw(200);
acc.Withdraw(5000);  // Should warn: insufficient funds
acc.PrintStatement();
// Output: Alice | Balance: $1,300.00
```

---

### Exercise 7 — Song with Auto-Properties
Create a `Song` class with auto-properties: `Title`, `Artist`, `DurationSeconds` (int). Add:
- A parameterized constructor
- A method `GetFormattedDuration()` that returns `"3:45"` format (minutes:seconds)
- A method `IsLong()` that returns `true` if over 5 minutes

Create a list of 5 songs and print only the long ones with their formatted duration.

---

### Exercise 8 — Constructor Overloading
Create an `Email` class with properties: `From`, `To`, `Subject`, `Body`, `IsUrgent` (bool). Write three constructors:

1. `Email(string from, string to, string subject, string body, bool isUrgent)` — full constructor
2. `Email(string from, string to, string subject, string body)` — defaults `IsUrgent` to `false`
3. `Email(string from, string to)` — defaults subject to "(No Subject)", body to "", and `IsUrgent` to `false`

Use constructor chaining. Test all three.

---

## Section C: `this` Keyword and Multi-Class Projects (Lecture 3)

### Exercise 9 — `this` Practice
Rewrite the following class to use `this` to resolve naming conflicts in the constructor. Verify it works correctly.

```csharp
class Player
{
    public string Name { get; set; }
    public int Score { get; set; }
    public int Level { get; set; }

    public Player(string n, int s, int l)
    {
        Name = n;
        Score = s;
        Level = l;
    }
}
```

---

### Exercise 10 — School Roster
Create two classes:

**`Student` class:**
- Properties: `Name`, `Grade` (int, 1-12)
- Constructor with validation (grade must be 1-12)
- `PrintInfo()` method

**`Classroom` class:**
- Properties: `RoomNumber` (string), `Teacher` (string), `Students` (List\<Student\>)
- `AddStudent(Student student)` method
- `PrintRoster()` method that displays all students
- `GetStudentCount()` method

Create a classroom, add 5 students, and display the roster.

---

### Exercise 11 — Music Playlist
Create two classes:

**`Song` class:**
- Properties: `Title`, `Artist`, `DurationSeconds`
- Constructor, `GetFormattedDuration()` method

**`Playlist` class:**
- Properties: `Name`, `Songs` (List\<Song\>)
- `AddSong(Song song)` method
- `GetTotalDuration()` method that returns the total seconds of all songs
- `PrintPlaylist()` method that shows all songs with a total at the bottom

Create a playlist with at least 5 songs and display it:

```
🎵 My Favorites (5 songs)
──────────────────────────
1. "Bohemian Rhapsody" by Queen [5:55]
2. "Hotel California" by Eagles [6:30]
3. "Stairway to Heaven" by Led Zeppelin [8:02]
4. "Imagine" by John Lennon [3:07]
5. "Yesterday" by The Beatles [2:05]
──────────────────────────
Total Duration: 25:39
```

---

## Section D: Combined Challenges

### Exercise 12 — Inventory System
Create a `Product` class with:
- Properties: `Name`, `Price`, `Quantity`
- Constructor with all parameters
- `GetTotalValue()` method

Create a list of at least 5 products. Then write methods (either in a separate `Inventory` class or in the main program) to:
1. Print all products in a formatted table
2. Find the most expensive product
3. Find the product with the highest total value (price × quantity)
4. Calculate the total inventory value across all products

---

### Exercise 13 — Quiz Game (Mini Challenge)
Create a `Question` class with:
- `Text` (the question), `Answer` (the correct answer), `Points` (int)
- A method `AskQuestion()` that prints the question, reads input, checks the answer, and returns the points earned (0 if wrong)

Create a `Quiz` class with:
- A `List<Question>` and a quiz name
- An `AddQuestion(Question q)` method
- A `RunQuiz()` method that asks all questions and prints the final score

Build a quiz with at least 5 questions and run it:

```
🧠 C# Basics Quiz
═══════════════════

Q1 (10 pts): What keyword creates a new object?
Your answer: new
✅ Correct! +10 points

Q2 (10 pts): What type stores true/false values?
Your answer: boolean
❌ Incorrect. The answer is: bool

...

Final Score: 30 / 50
```

---

### Exercise 14 — Deck of Cards (Advanced)
Create a `Card` class with `Suit` (string: "Hearts", "Diamonds", "Clubs", "Spades") and `Rank` (string: "2" through "10", "Jack", "Queen", "King", "Ace"). Add a `DisplayCard()` method that prints something like `"🂡 Ace of Spades"`.

Create a `Deck` class with a `List<Card>` that creates all 52 cards in the constructor. Add:
- `Shuffle()` method (swap each card with a random position — use `Random`)
- `DrawCard()` method that removes and returns the top card
- `CardsRemaining()` method

Draw 5 cards from a shuffled deck and display them.

---

## Difficulty Guide

| Exercises | Difficulty | Concepts |
|-----------|-----------|----------|
| 1–4 | ⭐ Basic | Fields, objects, methods, references |
| 5–8 | ⭐⭐ Intermediate | Properties, validation, constructors, overloading |
| 9–11 | ⭐⭐ Intermediate | `this`, multi-class, composition |
| 12–14 | ⭐⭐⭐ Challenging | Full integration, design thinking |

---

[← Back to Week 7 Overview](./README.md)
