# Lecture 3: Integration — Building a Complete Application

[← Previous: Lecture 2 – Introduction to Async/Await and Course Review](./lecture-2.md) | [Back to Week 15 Overview](./README.md)

---

## Lecture Overview

| Item | Detail |
|------|--------|
| Duration | 45 minutes |
| Topics | Building a complete console application integrating all course concepts; looking ahead to future courses |
| Preparation | All previous weeks — this lecture uses everything |

---

## 1. What We're Building: Employee Management System

In this lecture, we'll build a complete **Employee Management System** step by step. This application demonstrates how all the concepts from this course work together in a real program.

The system will use:

| Concept | Where It Appears |
|---------|-----------------|
| Classes & objects | `Employee`, `Manager`, `Developer` |
| Inheritance | `Manager` and `Developer` extend `Employee` |
| Abstract class | `Employee` is abstract with an abstract `CalculateBonus()` |
| Interface | `IPrintable` for formatted display |
| Encapsulation | Private fields, property validation |
| Enum | `Department` enum |
| Generics | `List<Employee>`, `Dictionary` |
| LINQ | Filtering, sorting, grouping employees |
| Exception handling | Input validation, custom exceptions |
| Static members | `EmployeeIdGenerator`, `InputHelper` |

Let's build it piece by piece.

---

## 2. Step 1 — The Enum and Interface

Start with the supporting types that other classes will depend on.

### The Department Enum

```csharp
public enum Department
{
    Engineering,
    Marketing,
    Sales,
    HumanResources,
    Finance
}
```

### The IPrintable Interface

```csharp
public interface IPrintable
{
    string ToFormattedString();
}
```

These are simple, but they give our system type safety (`Department` instead of raw strings) and a consistent display contract (`IPrintable`).

---

## 3. Step 2 — The Abstract Base Class

```csharp
public abstract class Employee : IPrintable
{
    // Static member — shared ID generator
    private static int _nextId = 1001;

    // Instance properties
    public int Id { get; }
    public string Name { get; set; }
    public Department Department { get; set; }

    private decimal _baseSalary;
    public decimal BaseSalary
    {
        get => _baseSalary;
        set
        {
            if (value < 0)
                throw new ArgumentException("Salary cannot be negative.");
            _baseSalary = value;
        }
    }

    // Constructor
    protected Employee(string name, Department department, decimal baseSalary)
    {
        if (string.IsNullOrWhiteSpace(name))
            throw new ArgumentException("Name cannot be empty.");

        Id = _nextId++;
        Name = name;
        Department = department;
        BaseSalary = baseSalary;
    }

    // Abstract method — each employee type calculates bonus differently
    public abstract decimal CalculateBonus();

    // Concrete method — total pay
    public decimal TotalCompensation() => BaseSalary + CalculateBonus();

    // Interface implementation
    public virtual string ToFormattedString()
    {
        return $"[{Id}] {Name} | {Department} | Salary: {BaseSalary:C} | Bonus: {CalculateBonus():C}";
    }

    public override string ToString() => $"{Name} (ID: {Id})";
}
```

Notice how many concepts appear in this single class:
- **Static field** (`_nextId`) for auto-incrementing IDs
- **Encapsulation** with a private backing field and validation in the setter
- **Abstract method** that derived classes must implement
- **Interface implementation** (`IPrintable`)
- **Exception throwing** for invalid data

---

## 4. Step 3 — The Derived Classes

### Manager

```csharp
public class Manager : Employee
{
    public int TeamSize { get; set; }

    public Manager(string name, Department department, decimal baseSalary, int teamSize)
        : base(name, department, baseSalary)
    {
        TeamSize = teamSize;
    }

    // Managers get 10% bonus + $500 per team member
    public override decimal CalculateBonus()
    {
        return BaseSalary * 0.10m + TeamSize * 500m;
    }

    public override string ToFormattedString()
    {
        return base.ToFormattedString() + $" | Team: {TeamSize} people";
    }
}
```

### Developer

```csharp
public class Developer : Employee
{
    public string PrimaryLanguage { get; set; }
    public int YearsOfExperience { get; set; }

    public Developer(string name, Department department, decimal baseSalary,
                     string primaryLanguage, int yearsOfExperience)
        : base(name, department, baseSalary)
    {
        PrimaryLanguage = primaryLanguage;
        YearsOfExperience = yearsOfExperience;
    }

    // Developers get 5% base bonus + 1% per year of experience
    public override decimal CalculateBonus()
    {
        decimal experienceMultiplier = 0.05m + (YearsOfExperience * 0.01m);
        return BaseSalary * experienceMultiplier;
    }

    public override string ToFormattedString()
    {
        return base.ToFormattedString() +
               $" | Lang: {PrimaryLanguage} | Exp: {YearsOfExperience} yrs";
    }
}
```

Both classes demonstrate **inheritance**, **constructor chaining** with `base()`, **method overriding**, and **polymorphism** (each calculates `CalculateBonus()` differently).

---

## 5. Step 4 — A Custom Exception

```csharp
public class EmployeeNotFoundException : Exception
{
    public int SearchedId { get; }

    public EmployeeNotFoundException(int id)
        : base($"Employee with ID {id} was not found.")
    {
        SearchedId = id;
    }
}
```

A small but important detail — custom exceptions make error handling more meaningful and specific.

---

## 6. Step 5 — The Static Utility Class

```csharp
public static class InputHelper
{
    public static string ReadNonEmpty(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            string input = Console.ReadLine()?.Trim() ?? "";
            if (input.Length > 0) return input;
            Console.WriteLine("  Input cannot be empty. Try again.");
        }
    }

    public static int ReadInt(string prompt, int min = int.MinValue, int max = int.MaxValue)
    {
        while (true)
        {
            Console.Write(prompt);
            if (int.TryParse(Console.ReadLine(), out int result) && result >= min && result <= max)
                return result;
            Console.WriteLine($"  Please enter a whole number between {min} and {max}.");
        }
    }

    public static decimal ReadDecimal(string prompt, decimal min = 0)
    {
        while (true)
        {
            Console.Write(prompt);
            if (decimal.TryParse(Console.ReadLine(), out decimal result) && result >= min)
                return result;
            Console.WriteLine($"  Please enter a valid number (minimum {min}).");
        }
    }

    public static TEnum ReadEnum<TEnum>(string prompt) where TEnum : struct, Enum
    {
        var values = Enum.GetValues<TEnum>();
        Console.WriteLine(prompt);
        for (int i = 0; i < values.Length; i++)
            Console.WriteLine($"  {i + 1}. {values[i]}");

        while (true)
        {
            Console.Write("Choice: ");
            if (int.TryParse(Console.ReadLine(), out int choice) && choice >= 1 && choice <= values.Length)
                return values[choice - 1];
            Console.WriteLine($"  Please enter a number between 1 and {values.Length}.");
        }
    }
}
```

This helper class uses **static methods**, **generics** (`TEnum`), **input validation loops**, and **TryParse** — concepts from across the course.

---

## 7. Step 6 — The Service Class (Business Logic)

```csharp
public class EmployeeService
{
    private readonly List<Employee> _employees = new();

    public void Add(Employee employee)
    {
        _employees.Add(employee);
        Console.WriteLine($"  ✓ Added: {employee}");
    }

    public Employee GetById(int id)
    {
        var employee = _employees.FirstOrDefault(e => e.Id == id);
        if (employee == null)
            throw new EmployeeNotFoundException(id);
        return employee;
    }

    public List<Employee> GetAll() => _employees.ToList();

    public List<Employee> GetByDepartment(Department dept)
    {
        return _employees
            .Where(e => e.Department == dept)
            .OrderBy(e => e.Name)
            .ToList();
    }

    public List<Employee> GetTopEarners(int count)
    {
        return _employees
            .OrderByDescending(e => e.TotalCompensation())
            .Take(count)
            .ToList();
    }

    public decimal GetAverageSalary()
    {
        if (!_employees.Any())
            throw new InvalidOperationException("No employees to calculate average.");
        return _employees.Average(e => e.BaseSalary);
    }

    public Dictionary<Department, int> GetHeadcount()
    {
        return _employees
            .GroupBy(e => e.Department)
            .ToDictionary(g => g.Key, g => g.Count());
    }

    public void PrintReport()
    {
        Console.WriteLine("\n╔══════════════════════════════════════════════════╗");
        Console.WriteLine("║           EMPLOYEE REPORT                        ║");
        Console.WriteLine("╚══════════════════════════════════════════════════╝\n");

        if (!_employees.Any())
        {
            Console.WriteLine("  No employees in the system.");
            return;
        }

        foreach (var employee in _employees.OrderBy(e => e.Department).ThenBy(e => e.Name))
        {
            Console.WriteLine(employee.ToFormattedString());
        }

        Console.WriteLine($"\n  Total employees: {_employees.Count}");
        Console.WriteLine($"  Average salary:  {GetAverageSalary():C}");
        Console.WriteLine($"  Total payroll:   {_employees.Sum(e => e.TotalCompensation()):C}");

        Console.WriteLine("\n  Headcount by department:");
        foreach (var kvp in GetHeadcount().OrderBy(kvp => kvp.Key))
        {
            Console.WriteLine($"    {kvp.Key}: {kvp.Value}");
        }
    }
}
```

This class is the heart of the application. It uses:
- **`List<Employee>`** — polymorphic collection holding managers and developers
- **LINQ** — `Where`, `OrderBy`, `FirstOrDefault`, `Average`, `Sum`, `GroupBy`, `ToDictionary`
- **Exception handling** — throwing `EmployeeNotFoundException` and `InvalidOperationException`
- **Interfaces** — calling `ToFormattedString()` through `IPrintable`

---

## 8. Step 7 — The Main Program

```csharp
class Program
{
    static void Main(string[] args)
    {
        var service = new EmployeeService();
        bool running = true;

        Console.WriteLine("=== Employee Management System ===\n");

        while (running)
        {
            Console.WriteLine("\n--- Menu ---");
            Console.WriteLine("1. Add Manager");
            Console.WriteLine("2. Add Developer");
            Console.WriteLine("3. View All Employees");
            Console.WriteLine("4. Search by ID");
            Console.WriteLine("5. View by Department");
            Console.WriteLine("6. View Top Earners");
            Console.WriteLine("7. Full Report");
            Console.WriteLine("8. Exit");

            int choice = InputHelper.ReadInt("\nChoice: ", 1, 8);

            try
            {
                switch (choice)
                {
                    case 1:
                        AddManager(service);
                        break;
                    case 2:
                        AddDeveloper(service);
                        break;
                    case 3:
                        ViewAll(service);
                        break;
                    case 4:
                        SearchById(service);
                        break;
                    case 5:
                        ViewByDepartment(service);
                        break;
                    case 6:
                        ViewTopEarners(service);
                        break;
                    case 7:
                        service.PrintReport();
                        break;
                    case 8:
                        running = false;
                        Console.WriteLine("\nGoodbye!");
                        break;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"\n  Error: {ex.Message}");
            }
        }
    }

    static void AddManager(EmployeeService service)
    {
        Console.WriteLine("\n--- Add Manager ---");
        string name = InputHelper.ReadNonEmpty("Name: ");
        var dept = InputHelper.ReadEnum<Department>("Department:");
        decimal salary = InputHelper.ReadDecimal("Base salary: ", 0);
        int teamSize = InputHelper.ReadInt("Team size: ", 0, 100);

        service.Add(new Manager(name, dept, salary, teamSize));
    }

    static void AddDeveloper(EmployeeService service)
    {
        Console.WriteLine("\n--- Add Developer ---");
        string name = InputHelper.ReadNonEmpty("Name: ");
        var dept = InputHelper.ReadEnum<Department>("Department:");
        decimal salary = InputHelper.ReadDecimal("Base salary: ", 0);
        string language = InputHelper.ReadNonEmpty("Primary language: ");
        int years = InputHelper.ReadInt("Years of experience: ", 0, 50);

        service.Add(new Developer(name, dept, salary, language, years));
    }

    static void ViewAll(EmployeeService service)
    {
        var employees = service.GetAll();
        if (!employees.Any())
        {
            Console.WriteLine("\n  No employees yet.");
            return;
        }

        Console.WriteLine($"\n--- All Employees ({employees.Count}) ---");
        foreach (var emp in employees)
            Console.WriteLine($"  {emp.ToFormattedString()}");
    }

    static void SearchById(EmployeeService service)
    {
        int id = InputHelper.ReadInt("Enter employee ID: ");
        var emp = service.GetById(id);
        Console.WriteLine($"\n  {emp.ToFormattedString()}");
    }

    static void ViewByDepartment(EmployeeService service)
    {
        var dept = InputHelper.ReadEnum<Department>("Select department:");
        var employees = service.GetByDepartment(dept);

        if (!employees.Any())
        {
            Console.WriteLine($"\n  No employees in {dept}.");
            return;
        }

        Console.WriteLine($"\n--- {dept} Department ({employees.Count}) ---");
        foreach (var emp in employees)
            Console.WriteLine($"  {emp.ToFormattedString()}");
    }

    static void ViewTopEarners(EmployeeService service)
    {
        int count = InputHelper.ReadInt("How many top earners? ", 1, 20);
        var topEarners = service.GetTopEarners(count);

        Console.WriteLine($"\n--- Top {topEarners.Count} Earners ---");
        for (int i = 0; i < topEarners.Count; i++)
        {
            Console.WriteLine($"  {i + 1}. {topEarners[i].ToFormattedString()}");
            Console.WriteLine($"     Total Compensation: {topEarners[i].TotalCompensation():C}");
        }
    }
}
```

The `Main` program ties everything together with a clean menu loop, organized methods, and a top-level `try-catch` that prevents crashes.

---

## 9. Concept Map — What's Used Where

Here's a summary of every course concept and where it appears in this application:

| Course Concept | Where It Appears |
|---------------|-----------------|
| Variables & types | Throughout all classes |
| String interpolation | `ToFormattedString()`, display methods |
| Conditionals | Menu `switch`, validation logic |
| Loops | `while` menu loop, `foreach` for display |
| Methods | Every class has well-organized methods |
| Collections | `List<Employee>`, `Dictionary<Department, int>` |
| Classes & objects | `Employee`, `Manager`, `Developer`, `EmployeeService` |
| Encapsulation | Private `_baseSalary` with validation |
| Inheritance | `Manager : Employee`, `Developer : Employee` |
| Abstract class | `Employee` with abstract `CalculateBonus()` |
| Polymorphism | `List<Employee>` holding managers and developers |
| Interface | `IPrintable` implemented by `Employee` |
| Enum | `Department` |
| Exception handling | `try-catch`, custom `EmployeeNotFoundException` |
| LINQ | `Where`, `OrderBy`, `Average`, `Sum`, `GroupBy` |
| Static members | `InputHelper` static class, `_nextId` static field |
| Generics | `List<T>`, `Dictionary<TKey, TValue>`, `ReadEnum<TEnum>` |

---

## 10. Looking Ahead — What Comes Next

The skills you've built in this course are the **foundation** for everything that follows in this program. Here's how they connect:

### Database Course

| What You Learned | What You'll Use It For |
|-----------------|----------------------|
| Classes & properties | **Entity classes** — each class maps to a database table |
| Collections | **Query results** — databases return lists of objects |
| LINQ | **Entity Framework queries** — you'll query databases using the exact same LINQ syntax |
| Enums | **Status fields** — `OrderStatus.Pending`, `UserRole.Admin` |

```csharp
// This LINQ you learned → becomes a database query in EF Core
var students = context.Students
    .Where(s => s.Gpa >= 3.5)
    .OrderBy(s => s.Name)
    .ToList();
```

### Web App Course (MVC)

| What You Learned | What You'll Use It For |
|-----------------|----------------------|
| Classes | **Models** — the M in MVC |
| Interfaces | **Dependency injection** — controllers depend on interfaces, not concrete classes |
| Exception handling | **Error middleware** — handling errors in HTTP requests |
| Static helpers | **Utility classes** — validation, formatting, mapping |
| Encapsulation | **ViewModels** — controlling what data is exposed to views |

```csharp
// Your class design skills → MVC model
public class StudentController : Controller
{
    private readonly IStudentService _service;  // Interface from Week 11!

    public StudentController(IStudentService service)
    {
        _service = service;
    }

    public IActionResult Index()
    {
        var students = _service.GetAll();  // Your service pattern!
        return View(students);
    }
}
```

### System Design Course

| What You Learned | What You'll Use It For |
|-----------------|----------------------|
| Inheritance & interfaces | **Design patterns** — Strategy, Factory, Observer |
| Composition | **Building complex systems** from simple components |
| Abstract classes | **Framework design** — defining extension points |
| Generics | **Reusable data structures** and algorithms |

> **The bottom line:** Everything you learned in this course was designed with these future courses in mind. The `EmployeeService` pattern you just saw? That's exactly how services work in web applications. The LINQ queries? Those become database queries. The interfaces? Those power dependency injection. You're ready.

---

## Summary

| Topic | Key Takeaway |
|-------|-------------|
| Integration | Every concept from Weeks 1–15 works together in real applications |
| Architecture | Separate concerns: enums → models → services → UI |
| LINQ in practice | Replaces loops for filtering, sorting, grouping, and aggregating |
| Polymorphism in practice | `List<Employee>` holds different types; each behaves differently |
| Looking ahead | Classes → database entities, LINQ → EF queries, interfaces → DI |

**Congratulations!** You've completed the Introduction to Programming course. You now have a solid foundation in C# and object-oriented programming that will serve you in every course that follows.

---

[← Previous: Lecture 2 – Introduction to Async/Await and Course Review](./lecture-2.md) | [Back to Week 15 Overview](./README.md)
