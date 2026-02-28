# Week 14 – Exercises: LINQ and Lambda Expressions

[Back to Week 14 Overview](./README.md)

---

## How to Use These Exercises

Work through each section after completing the corresponding lecture. Start with Section A, then progress through the sections as your confidence grows. **Section D** exercises combine all concepts from the week.

**Difficulty Levels:**
- ⭐ Basic — Direct application of a single concept
- ⭐⭐ Intermediate — Combines two or more concepts
- ⭐⭐⭐ Challenging — Requires creative problem-solving

---

## Section A: Lambda Expressions, Where, Select, OrderBy (Lecture 1)

### Exercise 1 — Even Numbers ⭐

Given the list below, use LINQ to find all even numbers and print them.

```csharp
List<int> numbers = new List<int> { 15, 22, 8, 31, 44, 7, 16, 53, 28, 9 };
```

**Expected Output:**
```
Even numbers: 22, 8, 44, 16, 28
```

---

### Exercise 2 — Long Words ⭐

Given the list below, use LINQ to find all words with more than 5 characters, sorted alphabetically.

```csharp
List<string> words = new List<string>
{
    "apple", "banana", "cherry", "date", "elderberry",
    "fig", "grape", "honeydew", "kiwi", "lemon"
};
```

**Expected Output:**
```
Long words (sorted):
  banana
  cherry
  elderberry
  honeydew
```

---

### Exercise 3 — Number Transformer ⭐

Given a list of integers, use `Select` to create a new list where each number is squared. Print the results.

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
```

**Expected Output:**
```
Squared: 1, 4, 9, 16, 25, 36, 49, 64, 81, 100
```

---

### Exercise 4 — Name Formatter ⭐⭐

Given a list of names in lowercase, use LINQ to:
1. Filter out names shorter than 4 characters
2. Convert each name to title case (first letter uppercase)
3. Sort alphabetically

```csharp
List<string> names = new List<string>
{
    "alice", "bob", "charlie", "dan", "eve", "frank", "grace"
};
```

**Expected Output:**
```
Alice
Charlie
Frank
Grace
```

> **Hint:** To capitalize the first letter: `name.Substring(0, 1).ToUpper() + name.Substring(1)`

---

### Exercise 5 — Temperature Converter ⭐⭐

Given a list of temperatures in Celsius, use LINQ to:
1. Convert each to Fahrenheit using the formula: `F = C × 9/5 + 32`
2. Filter out any temperatures below freezing (below 32°F)
3. Sort from hottest to coldest

```csharp
List<double> celsiusTemps = new List<double> { -10, 0, 15, 25, 30, 37, 100 };
```

**Expected Output:**
```
Temperatures above freezing (°F):
  212.0°F
  98.6°F
  86.0°F
  77.0°F
  59.0°F
```

---

### Exercise 6 — Chain Builder ⭐⭐

Given the list below, write a **single LINQ chain** that:
1. Removes negative numbers
2. Removes duplicates (use `.Distinct()`)
3. Sorts in ascending order
4. Takes only the first 5 results (use `.Take(5)`)

```csharp
List<int> data = new List<int> { 5, -3, 8, 5, 12, -1, 8, 3, 15, 7, 3, 20, -5, 12 };
```

**Expected Output:**
```
Cleaned data: 3, 5, 7, 8, 12
```

---

## Section B: Aggregation and Element Methods (Lecture 2)

### Exercise 7 — Score Statistics ⭐

Given the list of test scores below, use LINQ aggregation methods to display the statistics.

```csharp
List<int> scores = new List<int> { 78, 92, 85, 67, 95, 73, 88, 91, 62, 84 };
```

**Expected Output:**
```
Score Statistics:
  Count:   10
  Sum:     815
  Average: 81.5
  Highest: 95
  Lowest:  62
  Passing (≥70): 8
  Failing (<70): 2
```

---

### Exercise 8 — Word Analyzer ⭐

Given a list of words, use LINQ to answer these questions:

```csharp
List<string> words = new List<string>
{
    "programming", "is", "fun", "and", "challenging",
    "but", "rewarding", "in", "the", "end"
};
```

**Expected Output:**
```
Word Analysis:
  Total words: 10
  Longest word: programming (11 chars)
  Shortest word: is (2 chars)
  Average length: 4.9 chars
  Any word > 10 chars? True
  All words > 1 char? True
```

---

### Exercise 9 — Find the Student ⭐⭐

Using the `Student` class and list from Lecture 2, write LINQ queries to:

1. Find the student with the highest GPA
2. Find the first student whose name starts with "C"
3. Check if any student has a GPA below 2.0
4. Get the youngest student's name

Print each result.

---

### Exercise 10 — Shopping Cart ⭐⭐

Create a simple `CartItem` class and use LINQ to analyze a shopping cart:

```csharp
class CartItem
{
    public string Product { get; set; }
    public decimal Price { get; set; }
    public int Quantity { get; set; }
}
```

Create a list of at least 6 cart items, then use LINQ to display:
- Total number of items (sum of all quantities)
- Subtotal (sum of price × quantity for each item)
- Most expensive single item
- Cheapest single item
- Average item price

---

## Section C: GroupBy and Advanced Patterns (Lecture 3)

### Exercise 11 — Word Length Groups ⭐

Group the words below by their length and display each group:

```csharp
List<string> words = new List<string>
{
    "cat", "dog", "elephant", "ant", "bear",
    "fox", "giraffe", "hawk", "iguana", "jay"
};
```

**Expected Output:**
```
Words with 3 letters: cat, dog, ant, fox, jay
Words with 4 letters: bear, hawk
Words with 6 letters: iguana
Words with 7 letters: giraffe
Words with 8 letters: elephant
```

---

### Exercise 12 — Employee Department Report ⭐⭐

Create an `Employee` class:

```csharp
class Employee
{
    public string Name { get; set; }
    public string Department { get; set; }
    public decimal Salary { get; set; }
    public int YearsOfService { get; set; }
}
```

Create a list of at least 10 employees across 3+ departments. Then produce a department summary report:

**Expected Output (format):**
```
Department Report
=========================================
Department       Employees  Avg Salary  Total Salary
-----------------------------------------
Engineering           4     $85,000     $340,000
Marketing             3     $72,000     $216,000
Sales                 3     $68,000     $204,000
=========================================
Company Total:       10     $76,000     $760,000
```

---

### Exercise 13 — Grade Book with GroupBy ⭐⭐

Given a list of student grades, group them into letter grades (A, B, C, D, F) and display the distribution:

```csharp
List<int> grades = new List<int>
{
    95, 82, 67, 91, 78, 55, 88, 73, 96, 84,
    62, 89, 71, 93, 77, 58, 86, 74, 99, 80
};
```

Requirements:
- A: 90-100, B: 80-89, C: 70-79, D: 60-69, F: below 60
- Show the count and average for each letter grade
- Show the overall class average
- Sort by letter grade (A first, F last)

---

### Exercise 14 — Movie Collection ⭐⭐⭐

Create a `Movie` class:

```csharp
class Movie
{
    public string Title { get; set; }
    public string Genre { get; set; }
    public int Year { get; set; }
    public double Rating { get; set; }
}
```

Create a list of at least 12 movies across various genres and years. Then answer these questions using LINQ (one query each):

1. What are the top 3 highest-rated movies?
2. How many movies are in each genre?
3. What is the average rating per genre, sorted from highest to lowest?
4. Which genres have an average rating above 8.0?
5. What are the distinct years represented, sorted chronologically?
6. What is the highest-rated movie in each genre?

---

## Section D: Combined Challenges

### Exercise 15 — Sales Data Analyzer ⭐⭐⭐

Create a `Sale` class:

```csharp
class Sale
{
    public string Product { get; set; }
    public string Region { get; set; }
    public decimal Amount { get; set; }
    public string Month { get; set; }
}
```

Create a list of at least 15 sales across different products, regions, and months. Then produce a comprehensive report:

1. **Total revenue** across all sales
2. **Revenue by region**, sorted highest to lowest
3. **Top 3 products** by total revenue
4. **Monthly revenue** trend
5. **Region with the most sales** (by count)
6. **Average sale amount** per region
7. Any region where **all sales exceed $100**?

---

### Exercise 16 — Library Catalog ⭐⭐⭐

Create a `Book` class:

```csharp
class Book
{
    public string Title { get; set; }
    public string Author { get; set; }
    public string Genre { get; set; }
    public int Pages { get; set; }
    public int Year { get; set; }
    public bool IsAvailable { get; set; }
}
```

Create a catalog of at least 15 books. Build a mini library query system that displays:

1. All available books, sorted by title
2. The number of books per genre
3. Authors who have more than one book in the catalog
4. The longest book in each genre
5. Books published in the last 10 years (since 2016), grouped by genre
6. The percentage of books that are currently available
7. A "You might like" section: given a genre, find all available books in that genre sorted by page count (shortest first)

---

## Bonus Challenges 🏆

### Bonus 1 — LINQ Puzzle

Without running the code, predict the output:

```csharp
List<int> nums = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var result = nums
    .Where(n => n % 3 == 0)
    .Select(n => n * n)
    .Where(n => n > 20)
    .OrderByDescending(n => n)
    .ToList();

Console.WriteLine(string.Join(", ", result));
```

Then run it to check your answer.

---

### Bonus 2 — Method Syntax vs Query Syntax

C# also supports a SQL-like query syntax for LINQ. Rewrite this method syntax query using query syntax:

```csharp
var result = students
    .Where(s => s.Gpa >= 3.0)
    .OrderBy(s => s.Name)
    .Select(s => new { s.Name, s.Gpa });
```

> **Hint:** Query syntax starts with `from` and ends with `select`:
> ```csharp
> var result = from s in students
>              where s.Gpa >= 3.0
>              orderby s.Name
>              select new { s.Name, s.Gpa };
> ```

Research query syntax online and try converting 2–3 more queries from the exercises above.

---

### Bonus 3 — Custom Extension Method

Write your own extension method called `WhereNot` that returns items that do **not** match a condition:

```csharp
// Should work like this:
var nonCS = students.WhereNot(s => s.Major == "Computer Science").ToList();
// Returns all students except CS majors
```

> **Hint:** Extension methods are defined as `static` methods in a `static` class, with `this` before the first parameter.

---

[Back to Week 14 Overview](./README.md)
