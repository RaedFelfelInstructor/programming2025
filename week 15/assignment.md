# Week 15 – Assignment: Course Library Manager

[Back to Week 15 Overview](./README.md)

---

## 📋 Overview

For this final assignment, you'll build a **Course Library Manager** — a console application that manages a collection of educational courses, tracks enrollments, and generates reports. This project brings together every major concept from the entire course.

> **This is your largest assignment yet.** Take it step by step. Build one class at a time, test as you go, and don't try to write everything at once.

---

## 🎯 What You're Building

A menu-driven console application where users can:

1. Add courses (online courses and classroom courses)
2. Enroll students in courses
3. View all courses
4. Search for courses
5. View enrollment reports
6. Generate a full library summary

---

## 📐 Required Design

### Enum

```csharp
public enum CourseLevel { Beginner, Intermediate, Advanced }
```

### Interface

```csharp
public interface ISearchable
{
    bool MatchesSearch(string keyword);
}
```

### Abstract Base Class: `Course`

| Member | Type | Details |
|--------|------|---------|
| `Id` | `int` (property) | Auto-incrementing using a **static** counter (start at 101) |
| `Title` | `string` (property) | Cannot be empty — throw `ArgumentException` if it is |
| `Instructor` | `string` (property) | Cannot be empty |
| `Level` | `CourseLevel` (property) | |
| `MaxStudents` | `int` (property) | Must be > 0 |
| `_enrolledStudents` | `List<string>` (private field) | Stores student names |
| `EnrolledCount` | `int` (read-only property) | Returns `_enrolledStudents.Count` |
| `IsFull` | `bool` (read-only property) | `EnrolledCount >= MaxStudents` |
| `Enroll(string studentName)` | Method | Adds student if not full and not already enrolled; throws appropriate exceptions |
| `GetEnrolledStudents()` | Method | Returns a copy of the enrolled list |
| `GetCourseType()` | `abstract string` | Returns `"Online"` or `"Classroom"` |
| `GetDetails()` | `abstract string` | Returns type-specific details |
| `ToString()` | Override | Formatted summary |

`Course` should also implement `ISearchable` — a course matches if the keyword (case-insensitive) appears in the `Title`, `Instructor`, or `CourseType`.

### Derived Class: `OnlineCourse`

| Member | Type | Details |
|--------|------|---------|
| `Platform` | `string` (property) | e.g., "Zoom", "Teams", "YouTube" |
| `IsRecorded` | `bool` (property) | Whether sessions are recorded |

- `GetCourseType()` returns `"Online"`
- `GetDetails()` returns something like `"Platform: Zoom | Recorded: Yes"`

### Derived Class: `ClassroomCourse`

| Member | Type | Details |
|--------|------|---------|
| `RoomNumber` | `string` (property) | e.g., "B204" |
| `Building` | `string` (property) | e.g., "Main Campus" |

- `GetCourseType()` returns `"Classroom"`
- `GetDetails()` returns something like `"Room: B204, Main Campus"`

### Custom Exception

```csharp
public class CourseFullException : Exception
{
    public string CourseName { get; }
    public CourseFullException(string courseName)
        : base($"Cannot enroll: '{courseName}' is full.") 
    {
        CourseName = courseName;
    }
}
```

Also throw `InvalidOperationException` if a student is already enrolled.

### Static Utility Class: `InputHelper`

Create a `static class InputHelper` with at least these methods:
- `ReadNonEmpty(string prompt)` — returns a non-empty trimmed string
- `ReadInt(string prompt, int min, int max)` — returns a validated integer
- `ReadYesNo(string prompt)` — returns `true` for "y"/"yes", `false` for "n"/"no"
- `ReadEnum<TEnum>(string prompt)` — displays numbered options and returns the selected enum value

### Service Class: `LibraryService`

A class that manages the `List<Course>` and provides these methods:

| Method | Description |
|--------|-------------|
| `AddCourse(Course course)` | Adds a course to the library |
| `GetAllCourses()` | Returns all courses |
| `GetCourseById(int id)` | Returns a course or throws an exception |
| `EnrollStudent(int courseId, string studentName)` | Enrolls a student (handle full/duplicate) |
| `Search(string keyword)` | Uses `ISearchable` to find matching courses |
| `GetCoursesByLevel(CourseLevel level)` | LINQ: filter by level |
| `GetMostPopularCourse()` | LINQ: course with most enrollments |
| `GetAverageEnrollment()` | LINQ: average enrolled count |
| `GetEnrollmentByLevel()` | LINQ + GroupBy: enrollment counts grouped by level |

### Main Program

A `while` loop with a numbered menu:

```
=== Course Library Manager ===

1. Add Online Course
2. Add Classroom Course
3. View All Courses
4. Enroll Student
5. Search Courses
6. View Course Details
7. Library Report
8. Exit
```

Wrap each menu action in a `try-catch` so errors don't crash the program.

---

## 📦 Concepts Used

This assignment requires you to use:

| Concept | Where |
|---------|-------|
| Classes & objects | `Course`, `OnlineCourse`, `ClassroomCourse`, `LibraryService` |
| Inheritance | `OnlineCourse : Course`, `ClassroomCourse : Course` |
| Abstract class/method | `Course` is abstract; `GetCourseType()`, `GetDetails()` |
| Interface | `ISearchable` implemented by `Course` |
| Encapsulation | Private `_enrolledStudents`, validated properties |
| Enum | `CourseLevel` |
| Generics | `List<Course>`, `List<string>`, `Dictionary` in reports |
| LINQ | Filtering, sorting, grouping, aggregating in `LibraryService` |
| Exception handling | `CourseFullException`, `ArgumentException`, try-catch in menu |
| Static members | Static ID counter, `InputHelper` static class |

---

## 📊 Sample Output

```
=== Course Library Manager ===

1. Add Online Course
2. Add Classroom Course
3. View All Courses
4. Enroll Student
5. Search Courses
6. View Course Details
7. Library Report
8. Exit

Choice: 1

--- Add Online Course ---
Title: Introduction to Python
Instructor: Dr. Smith
Level:
  1. Beginner
  2. Intermediate
  3. Advanced
Choice: 1
Max students: 30
Platform: Zoom
Are sessions recorded? (y/n): y
  ✓ Added: Introduction to Python (ID: 101)

Choice: 4

--- Enroll Student ---
Course ID: 101
Student name: Alice Johnson
  ✓ Alice Johnson enrolled in Introduction to Python

Choice: 7

╔══════════════════════════════════════════╗
║          LIBRARY REPORT                  ║
╚══════════════════════════════════════════╝

All Courses:
  [101] Introduction to Python | Online | Beginner | 1/30 enrolled
        Platform: Zoom | Recorded: Yes
        Instructor: Dr. Smith

  [102] Data Structures | Classroom | Intermediate | 0/25 enrolled
        Room: B204, Main Campus
        Instructor: Prof. Lee

Summary:
  Total courses: 2
  Average enrollment: 0.5
  Most popular: Introduction to Python (1 enrolled)

Enrollment by Level:
  Beginner: 1 student(s)
  Intermediate: 0 student(s)
```

---

## ✅ Grading Rubric

| Criteria | Points |
|----------|--------|
| **Enum and interface** defined and used correctly | 10 |
| **Abstract base class** with static ID, validation, and enrolled students | 15 |
| **Two derived classes** with overridden methods | 15 |
| **Custom exception** used appropriately | 10 |
| **Static utility class** with validated input methods | 10 |
| **Service class** with LINQ-based methods | 15 |
| **Main program** with menu loop and error handling | 15 |
| **Code quality** — naming, organization, readability | 10 |
| **Total** | **100** |

---

## 💡 Hints

1. **Build incrementally.** Start with the `CourseLevel` enum and `Course` class. Get those compiling before adding derived classes.

2. **Test each class in isolation.** Before building the menu, create a few courses in `Main` and test methods directly:
   ```csharp
   var course = new OnlineCourse("Test", "Teacher", CourseLevel.Beginner, 5, "Zoom", true);
   course.Enroll("Alice");
   Console.WriteLine(course);
   ```

3. **Copy your `InputHelper` from lectures.** You don't need to write it from scratch — adapt the one from Lecture 1 and the integration exercise in Lecture 3.

4. **For `MatchesSearch`**, use `StringComparison.OrdinalIgnoreCase`:
   ```csharp
   title.Contains(keyword, StringComparison.OrdinalIgnoreCase)
   ```

5. **For `GetEnrollmentByLevel`**, use `GroupBy`:
   ```csharp
   courses.GroupBy(c => c.Level)
          .ToDictionary(g => g.Key, g => g.Sum(c => c.EnrolledCount));
   ```

6. **Return copies of lists** from your service (`.ToList()`) to prevent external code from modifying your internal data.

---

## 🌟 Bonus Challenges

1. **Remove a student** — add an `Unenroll(string studentName)` method and menu option.

2. **Export report to file** — write the library report to a `.txt` file using `File.WriteAllText()`.

3. **Course statistics** — add a menu option that shows: which courses are full, which have the most available spots, and the fill rate (enrolled / max) for each course.

4. **Sort options** — let the user choose to view courses sorted by title, by level, by enrollment count, or by fill rate.

5. **Data seeding** — create a `static` method `SeedData(LibraryService service)` that pre-populates the system with 5–10 sample courses and enrollments for testing.

---

[Back to Week 15 Overview](./README.md)
