# Week 1 – Exercises

[← Back to Week 1 Overview](./README.md)

---

These exercises cover material from all three lectures. Work through them in order — they progress from basic to more challenging. Each exercise is self-contained; create a new project or reuse an existing one for each.

---

## Section A: Output and Program Structure (Lectures 1–2)

### Exercise 1 — Hello You
Write a program that prints the following three lines (replace with your own name):

```
Hello, my name is [your name].
I am learning C# programming.
This is my first week!
```

---

### Exercise 2 — Write vs. WriteLine
**Predict first, then run.** What does this program output?

```csharp
Console.Write("C");
Console.Write("Sharp");
Console.WriteLine("!");
Console.WriteLine("Is");
Console.Write("Great ");
Console.Write("Fun");
```

Write down your prediction, then create a project and check.

---

### Exercise 3 — Escape Sequences
Write a program that produces this **exact** output using escape characters (`\t`, `\"`, `\\`, `\n`):

```
Item:	"Laptop"
Price:	$999.99
Stock:	Available
Path:	C:\Store\Electronics\laptops.csv
```

---

### Exercise 4 — Box Art
Write a program that displays this bordered box using `Console.WriteLine()`:

```
+---------------------------+
|   Welcome to C# Programming   |
|   Semester 1 - Week 1         |
+---------------------------+
```

Try to align the text neatly. You can use spaces — no special techniques needed.

---

### Exercise 5 — Comment Practice
Take your solution from Exercise 4 and add:
- A single-line comment at the top explaining what the program does
- A multi-line comment before the box explaining why you chose the text you used
- An inline comment on at least one `Console.WriteLine` line

---

## Section B: Input and Interaction (Lecture 3)

### Exercise 6 — Greeting Program
Write a program that:
1. Asks the user for their name
2. Asks the user for their favorite color
3. Displays: `"Hello, [name]! I hear you like [color]."`

Use string interpolation for the output.

---

### Exercise 7 — Simple Math
Write a program that:
1. Asks the user for two whole numbers
2. Displays their sum, difference, product, and quotient

Example output:
```
Enter first number: 10
Enter second number: 3
10 + 3 = 13
10 - 3 = 7
10 * 3 = 30
10 / 3 = 3
```

> Note: Integer division truncates the decimal. `10 / 3` gives `3`, not `3.33`. We'll cover this in Week 2.

---

### Exercise 8 — Temperature Display
Write a program that asks the user for a temperature in Celsius (as a whole number) and displays it along with a simple conversion to Fahrenheit.

The formula is: **F = C × 9 / 5 + 32**

Example output:
```
Enter temperature in Celsius: 25
25°C is 77°F
```

> Hint: Use `int` for now. The result may not be perfectly precise — that's okay for this exercise.

---

### Exercise 9 — Mad Libs
Create a simple Mad Libs game. Ask the user for:
1. A name
2. An animal
3. A number
4. A place

Then display a silly sentence using all four inputs. For example:

```
Enter a name: Bob
Enter an animal: penguin
Enter a number: 42
Enter a place: the moon

Bob saw 42 penguins dancing on the moon!
```

Use string interpolation to build the sentence.

---

### Exercise 10 — Receipt Generator
Write a program that asks for the following information and displays a formatted receipt:
1. Item name (text)
2. Quantity (whole number)
3. Price per item (whole number for now)

Example output:
```
=== PURCHASE RECEIPT ===
Item:       Widget
Quantity:   3
Unit Price: $15
Total:      $45
========================
```

Use string interpolation and `\t` for alignment.

---

## Section C: Challenge Problems

These are optional and more difficult. Try them if you finish the above exercises.

### Challenge 1 — Countdown Display
Write a program that asks the user for their name and a countdown number, then displays:

```
Enter your name: Alice
Enter a countdown number: 5

5... 4... 3... 2... 1...
Blast off, Alice!
```

> Hint: For now, you'll need to do the subtraction manually (we don't know loops yet). Just use `Console.Write()` and math expressions.

```csharp
int n = int.Parse(Console.ReadLine());
Console.Write($"{n}... ");
Console.Write($"{n - 1}... ");
// ... continue the pattern
```

---

### Challenge 2 — Time Converter
Ask the user for a number of **minutes** and convert it to hours and remaining minutes.

Example:
```
Enter total minutes: 150
That is 2 hours and 30 minutes.
```

> Hint: Use integer division (`/`) to get the hours and the modulo operator (`%`) to get the remaining minutes. For example, `150 / 60` is `2` and `150 % 60` is `30`.

---

### Challenge 3 — Personal Dashboard
Build a program that asks for the user's name, age, and daily study hours, then displays a dashboard:

```
Enter your name: Alice
Enter your age: 20
Enter daily study hours: 3

╔══════════════════════════════════╗
║        STUDENT DASHBOARD         ║
╠══════════════════════════════════╣
║ Name:          Alice             ║
║ Age:           20                ║
║ Study/Day:     3 hours           ║
║ Study/Week:    21 hours          ║
║ Study/Month:   90 hours          ║
║ Age next year: 21                ║
╚══════════════════════════════════╝
```

---

## Solutions

Try every exercise **on your own first** before looking at solutions. If you're stuck, re-read the relevant lecture section, then try again. Getting stuck and working through it is how you learn.

Solutions will be discussed in class.

---

[← Back to Week 1 Overview](./README.md)
