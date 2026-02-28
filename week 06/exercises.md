# Week 6 – Exercises: Arrays and Collections

[← Back to Week 6 Overview](./README.md)

---

These exercises progress from basic array operations to complex list-based challenges. Work through them in order — each section builds on the previous one.

---

## Section A: Array Basics (Lecture 1)

### Exercise 1 — Array Initialization
Create a `string[]` array containing the names of 5 countries you'd like to visit. Print each country with its index number using a `for` loop, then print them again using `foreach` (without index numbers).

### Exercise 2 — Temperature Tracker
Write a program that:
1. Creates an `int[]` array to store 7 daily temperatures (hardcoded values)
2. Calculates and displays: the average temperature, the hottest day (index and value), and the coldest day (index and value)

**Expected Output (example):**
```
Daily temperatures: 22, 25, 19, 30, 28, 21, 24
Average: 24.1°C
Hottest: Day 4 (30°C)
Coldest: Day 3 (19°C)
```

### Exercise 3 — Reverse Print
Write a method `static void PrintReversed(int[] numbers)` that prints the elements of an array in reverse order **without modifying** the original array. Test with `{ 10, 20, 30, 40, 50 }`.

### Exercise 4 — Count Occurrences
Write a method `static int CountOccurrences(int[] array, int target)` that returns how many times `target` appears in the array. Test with `{ 3, 7, 3, 2, 7, 3, 9, 7 }` — how many times does `3` appear? How about `7`?

### Exercise 5 — Above Average
Write a program that:
1. Reads 5 numbers from the user into an array
2. Calculates the average
3. Displays all numbers that are **above** the average

**Sample Run:**
```
Enter number 1: 10
Enter number 2: 25
Enter number 3: 15
Enter number 4: 30
Enter number 5: 20
Average: 20.0
Above average: 25, 30
```

---

## Section B: Array Patterns (Lecture 2)

### Exercise 6 — Sort Three Ways
Create an array of 8 random integers (hardcoded). Display:
1. Original order
2. Sorted ascending
3. Sorted descending

> Hint: Sort ascending first, then use `Array.Reverse()`.

### Exercise 7 — Parallel Arrays — Student Roster
Create three parallel arrays for 4 students:
- `string[] names`
- `int[] ages`
- `double[] gpas`

Display a formatted table showing each student's information. Then find and display the student with the highest GPA.

**Expected Output:**
```
╔════════════╦═════╦══════╗
║ Name       ║ Age ║ GPA  ║
╠════════════╬═════╬══════╣
║ Alice      ║  20 ║ 3.80 ║
║ Bob        ║  22 ║ 3.45 ║
║ Charlie    ║  19 ║ 3.92 ║
║ Diana      ║  21 ║ 3.67 ║
╠════════════╩═════╩══════╣
║ Highest GPA: Charlie (3.92)  ║
╚══════════════════════════════╝
```

### Exercise 8 — Matrix Diagonal
Create a 4×4 integer matrix. Write a program that:
1. Fills it with values from 1 to 16 (row by row)
2. Prints the matrix in grid form
3. Prints the main diagonal (top-left to bottom-right)
4. Calculates the sum of the diagonal

**Expected Output:**
```
 1  2  3  4
 5  6  7  8
 9 10 11 12
13 14 15 16

Diagonal: 1, 6, 11, 16
Diagonal sum: 34
```

### Exercise 9 — Array Shift
Write a method `static void ShiftLeft(int[] array)` that shifts all elements one position to the left. The first element wraps around to the end.

**Example:** `{ 1, 2, 3, 4, 5 }` → `{ 2, 3, 4, 5, 1 }`

---

## Section C: Lists (Lecture 3)

### Exercise 10 — To-Do List
Create a simple to-do list program with this menu:
1. Add task
2. Mark task as done (remove it)
3. View all tasks
4. Exit

Use a `List<string>` to store the tasks. Display task numbers starting from 1 (not 0).

### Exercise 11 — Unique Values
Write a method `static List<int> GetUniqueValues(List<int> numbers)` that returns a new list containing only the unique values (no duplicates) from the input list.

**Test with:** `{ 5, 3, 7, 3, 8, 5, 9, 7, 1 }` → should return `{ 5, 3, 7, 8, 9, 1 }`

### Exercise 12 — Word Counter
Write a program that:
1. Asks the user to type a sentence
2. Splits the sentence into words (use `sentence.Split(' ')` to get a `string[]`)
3. Stores the words in a `List<string>`
4. Displays: the total word count, the longest word, and the shortest word

### Exercise 13 — Number Filter
Write a program that:
1. Lets the user enter numbers (type `0` to stop)
2. Stores them in a `List<int>`
3. Creates two new lists: one with even numbers, one with odd numbers
4. Displays both lists and their counts

**Sample Run:**
```
Enter numbers (0 to stop): 12 7 4 9 16 3 8 0

Even numbers (4): 12, 4, 16, 8
Odd numbers (3): 7, 9, 3
```

### Exercise 14 — List Merge and Sort
Write a method `static List<int> MergeAndSort(List<int> list1, List<int> list2)` that combines two lists into one and returns the result sorted in ascending order.

**Test with:** `{ 5, 1, 8 }` and `{ 3, 9, 2 }` → `{ 1, 2, 3, 5, 8, 9 }`

---

## Section D: Mixed Challenges

### Exercise 15 — Frequency Counter
Write a program that takes an array of integers and displays how many times each unique value appears.

**Input:** `{ 4, 2, 4, 7, 2, 4, 2, 7 }`

**Expected Output:**
```
4 appears 3 times
2 appears 3 times
7 appears 2 times
```

> Hint: Use one list to track which values you've already counted.

### Exercise 16 — Grade Distribution
Write a program that:
1. Reads an unknown number of scores (0–100) from the user into a list
2. Categorizes each score into a grade (A: 90+, B: 80–89, C: 70–79, D: 60–69, F: below 60)
3. Displays a simple histogram:

```
Grade Distribution:
A: ███ (3)
B: █████ (5)
C: ████ (4)
D: ██ (2)
F: █ (1)
```

### Exercise 17 — Inventory Tracker
Create a program using parallel lists (`List<string>` for names, `List<int>` for quantities, `List<double>` for prices) that supports:
1. Add a product (name, quantity, price)
2. Remove a product by name
3. Update quantity of a product
4. Display all products with total value (price × quantity)
5. Display the most expensive and least expensive products

---

## Bonus Challenges

### Bonus 1 — Matrix Transpose
Write a method that takes a 2D array and returns its **transpose** (rows become columns, columns become rows).

**Input:**
```
1 2 3
4 5 6
```
**Output:**
```
1 4
2 5
3 6
```

### Bonus 2 — Running Average
Write a program that continuously reads numbers from the user and after each entry, displays the running average of all numbers entered so far. Use a list to track all entered values.

### Bonus 3 — Two-Sum Finder
Given an array of integers and a target sum, find and display all pairs of numbers in the array that add up to the target.

**Input:** array = `{ 2, 7, 11, 15, 3, 6 }`, target = `9`
**Output:** `Pairs that sum to 9: (2, 7), (3, 6)`

---

[← Back to Week 6 Overview](./README.md)
