# Week 6 – Assignment: Student Gradebook Manager

[← Back to Week 6 Overview](./README.md)

---

## 📋 Overview

Build a **Student Gradebook Manager** — a console application that manages student names and their exam scores, computes statistics, and generates a formatted class report. This project brings together arrays, lists, loops, conditions, and methods into a practical tool.

---

## 🎯 Objectives

This assignment tests your ability to:

- Use arrays and/or lists to store and manage collections of data
- Iterate through collections using `for` and `foreach`
- Perform common operations: sum, average, min, max, count, search
- Write and call methods that accept arrays/lists as parameters
- Format output into a professional-looking report
- Handle edge cases (empty data, invalid input)

---

## 📝 Requirements

### Core Features

Your program must support the following workflow:

1. **Add students** — The user can add students by name. Each student gets a list of exam scores.
2. **Enter scores** — For each student, the user enters a variable number of exam scores (use a list — the number of exams may differ between students).
3. **Calculate statistics** — For each student, calculate their average score and assign a letter grade.
4. **Generate report** — Display a formatted class report with individual and class-wide statistics.

### Letter Grade Scale

| Score Range | Grade |
|-------------|-------|
| 90 – 100 | A |
| 80 – 89 | B |
| 70 – 79 | C |
| 60 – 69 | D |
| Below 60 | F |

### Required Methods

You must implement at least these methods:

```csharp
// Calculate the average of a list of scores
static double CalculateAverage(List<int> scores)

// Determine the letter grade from an average score
static string GetLetterGrade(double average)

// Find the highest score across all students
static int FindClassHighScore(List<List<int>> allScores)

// Find the lowest score across all students
static int FindClassLowScore(List<List<int>> allScores)

// Display the formatted report
static void DisplayReport(List<string> names, List<List<int>> allScores)
```

> **Note:** The `List<List<int>>` syntax means "a list of lists of integers" — each student has their own list of scores, and all of those lists are collected in one outer list. This is a sneak peek at how collections can be nested!

---

## 💻 Expected Output

```
╔═══════════════════════════════════════════════════╗
║            STUDENT GRADEBOOK MANAGER              ║
╚═══════════════════════════════════════════════════╝

How many students? 3

--- Student 1 ---
Name: Alice
Enter scores (type 'done' when finished):
  Score: 85
  Score: 92
  Score: 78
  Score: done
  3 scores recorded for Alice.

--- Student 2 ---
Name: Bob
Enter scores (type 'done' when finished):
  Score: 65
  Score: 70
  Score: done
  2 scores recorded for Bob.

--- Student 3 ---
Name: Charlie
Enter scores (type 'done' when finished):
  Score: 95
  Score: 88
  Score: 91
  Score: 97
  Score: done
  4 scores recorded for Charlie.

╔══════════════════════════════════════════════════════════╗
║                    CLASS REPORT                          ║
╠═══════════╦═════════════════════╦═════════╦══════════════╣
║ Student   ║ Scores              ║ Average ║ Grade        ║
╠═══════════╬═════════════════════╬═════════╬══════════════╣
║ Alice     ║ 85, 92, 78          ║  85.0   ║ B            ║
║ Bob       ║ 65, 70              ║  67.5   ║ D            ║
║ Charlie   ║ 95, 88, 91, 97      ║  92.8   ║ A            ║
╠═══════════╩═════════════════════╩═════════╩══════════════╣
║ Class Statistics                                         ║
╠══════════════════════════════════════════════════════════╣
║ Class Average:    81.8                                   ║
║ Highest Score:    97 (Charlie)                           ║
║ Lowest Score:     65 (Bob)                               ║
║ Students Passing: 2/3 (66.7%)                            ║
║ Grade Distribution: A:1  B:1  C:0  D:1  F:0             ║
╚══════════════════════════════════════════════════════════╝
```

> Your exact formatting doesn't need to match this precisely — focus on presenting the information clearly and including all required data.

---

## 🧩 Starter Template

Here's a basic structure to help you get started. Fill in the method bodies and expand as needed:

```csharp
// Student Gradebook Manager
// Week 6 Assignment

List<string> studentNames = new List<string>();
List<List<int>> allScores = new List<List<int>>();

Console.WriteLine("╔═══════════════════════════════════════════════════╗");
Console.WriteLine("║            STUDENT GRADEBOOK MANAGER              ║");
Console.WriteLine("╚═══════════════════════════════════════════════════╝");

// Step 1: Get number of students
Console.Write("\nHow many students? ");
int studentCount = int.Parse(Console.ReadLine());

// Step 2: Input student data
for (int i = 0; i < studentCount; i++)
{
    Console.WriteLine($"\n--- Student {i + 1} ---");
    Console.Write("Name: ");
    string name = Console.ReadLine();
    studentNames.Add(name);

    List<int> scores = new List<int>();
    Console.WriteLine("Enter scores (type 'done' when finished):");

    // TODO: Read scores in a loop until user types "done"
    // Use int.TryParse for safe input handling!

    allScores.Add(scores);
    Console.WriteLine($"  {scores.Count} scores recorded for {name}.");
}

// Step 3: Display the report
DisplayReport(studentNames, allScores);


// === METHOD DEFINITIONS ===

static double CalculateAverage(List<int> scores)
{
    // TODO: Calculate and return the average
    // Handle the case where the list might be empty!
    return 0;
}

static string GetLetterGrade(double average)
{
    // TODO: Return "A", "B", "C", "D", or "F" based on the average
    return "";
}

static int FindClassHighScore(List<List<int>> allScores)
{
    // TODO: Find the single highest score across ALL students
    return 0;
}

static int FindClassLowScore(List<List<int>> allScores)
{
    // TODO: Find the single lowest score across ALL students
    return 0;
}

static void DisplayReport(List<string> names, List<List<int>> allScores)
{
    // TODO: Display the formatted report
    // Include: individual student rows, class average, high/low scores,
    //          pass rate, grade distribution
}
```

---

## 💡 Hints

1. **Reading scores until "done":** Use a `while (true)` loop. Read the input as a string, check if it's `"done"`, otherwise use `int.TryParse` to convert it. If parsing fails, show an error message and continue.

2. **Finding who has the highest score:** When you find the max score, also track the index so you can look up the student name.

3. **Class average:** This is the average of ALL scores across ALL students, not the average of the student averages (those are different!).

4. **Grade distribution:** Create an array or set of counters — one for each grade letter. Loop through students, get their grade, and increment the right counter.

5. **Empty scores:** What if a student has no scores? Your `CalculateAverage` method should handle this gracefully (e.g., return 0 and display "N/A").

6. **Nested lists:** `allScores[i]` gives you the `List<int>` for student `i`. Then `allScores[i][j]` gives you score `j` for student `i`.

---

## 📊 Grading Rubric

| Criteria | Points |
|----------|--------|
| **Data Input (20 pts)** | |
| Correctly reads student names into a list | 5 |
| Correctly reads variable number of scores per student | 10 |
| Uses TryParse for safe score input | 5 |
| **Calculations (30 pts)** | |
| `CalculateAverage` correctly computes average | 8 |
| `GetLetterGrade` returns correct grade for all ranges | 7 |
| `FindClassHighScore` works across nested lists | 5 |
| `FindClassLowScore` works across nested lists | 5 |
| Class average calculated correctly (all scores, not average of averages) | 5 |
| **Report Output (25 pts)** | |
| Individual student rows with scores, average, and grade | 10 |
| Class statistics section with all required data | 10 |
| Clean, readable formatting | 5 |
| **Code Quality (15 pts)** | |
| Proper use of methods (at least 5 methods) | 5 |
| Methods accept and return appropriate parameters | 5 |
| Code is organized and readable | 5 |
| **Edge Cases (10 pts)** | |
| Handles invalid score input gracefully | 5 |
| Handles student with no scores | 5 |
| **Total** | **100 pts** |

---

## 🚀 Bonus Challenges

### Bonus 1: Search Feature (+5 pts)
Add a feature after the report that lets the user search for a student by name and see their individual details.

### Bonus 2: Top Performer Highlight (+5 pts)
Identify and highlight the top-performing student (highest average) in the report with a special indicator (e.g., ⭐ or "★ Top Performer").

### Bonus 3: Score Analysis Per Student (+5 pts)
For each student, also display their highest score, lowest score, and score range (highest - lowest).

### Bonus 4: Sort by Average (+5 pts)
Add an option to display the report sorted by student average (highest to lowest). Remember: when you sort one list, you need to keep the parallel lists in sync!

### Bonus 5: File-Style Output (+5 pts)
In addition to the console display, create a simple text-based "file" by storing the report as a `List<string>` and displaying it. This previews the concept of writing to files (which you'll learn later).

---

## 📤 Submission

Submit a single `.cs` file containing your complete program. Make sure to:

- Test with at least 3 students with varying numbers of scores
- Test with edge cases (student with no scores, invalid input)
- Include comments explaining your approach for complex sections

---

[← Back to Week 6 Overview](./README.md)
