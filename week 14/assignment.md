# Week 14 – Assignment: Employee Report Generator

[Back to Week 14 Overview](./README.md)

---

## 📋 Overview

Build a console application that manages employee data and generates comprehensive reports using LINQ. This assignment brings together everything from Week 14 — lambda expressions, filtering, sorting, aggregation, grouping — and applies it to a realistic business scenario.

You'll create a system that loads employee data, then lets the user generate various reports through a menu-driven interface. Every report must be generated using LINQ — **no manual loops for data processing**.

---

## 🎯 Requirements

### Data Model

Create an `Employee` class with the following properties:

| Property | Type | Description |
|----------|------|-------------|
| `Id` | `int` | Unique employee ID |
| `Name` | `string` | Full name |
| `Department` | `string` | Department name |
| `Position` | `string` | Job title |
| `Salary` | `decimal` | Annual salary |
| `HireDate` | `DateTime` | Date hired |
| `IsActive` | `bool` | Currently employed |

Include:
- A constructor that sets all properties
- A `YearsOfService` read-only property that calculates years from `HireDate` to today
- A `ToString()` override for formatted display

### Sample Data

Create a list of **at least 15 employees** with the following characteristics:
- At least **4 different departments** (e.g., Engineering, Marketing, Sales, HR)
- A mix of active and inactive employees
- Salary range from $40,000 to $150,000
- Hire dates ranging from 2015 to 2025
- At least 2 employees per department

### Menu System

Display a menu with the following report options:

```
========================================
    EMPLOYEE REPORT GENERATOR
========================================

1. Employee Directory
2. Department Summary
3. Salary Analysis
4. Seniority Report
5. Search Employees
6. Custom Filter
7. Exit

Choose a report (1-7):
```

### Report Details

**Report 1 — Employee Directory**

Display all **active** employees sorted by department, then by name within each department. Show: Name, Department, Position, Salary, Years of Service.

**Report 2 — Department Summary**

For each department, show:
- Number of active employees
- Average salary
- Total salary cost (payroll)
- Highest-paid employee name

Sort departments by total payroll descending.

**Report 3 — Salary Analysis**

Display:
- Company-wide average salary (active employees only)
- Median salary (hint: sort and take the middle element)
- Highest and lowest paid employees with their details
- Number of employees in salary brackets: <$50K, $50K–$75K, $75K–$100K, $100K+
- Departments where the average salary exceeds the company-wide average

**Report 4 — Seniority Report**

Display:
- Top 5 longest-serving active employees
- Average years of service per department
- Employees with 5+ years of service
- New hires (less than 1 year)

**Report 5 — Search Employees**

Prompt the user for a search term, then find all employees whose:
- Name contains the search term (case-insensitive), OR
- Department contains the search term, OR
- Position contains the search term

Display matching results sorted by name.

**Report 6 — Custom Filter**

Let the user build a filtered view by choosing:
1. Department (show available departments, or "All")
2. Active only, Inactive only, or Both
3. Minimum salary (or skip)
4. Sort by: Name, Salary, Hire Date, or Department

Display the filtered results.

---

## 💡 LINQ Rule

**All data processing must use LINQ.** This means:
- No `foreach` loops for filtering, sorting, or aggregating data
- `foreach` is allowed only for **displaying** results (iterating to print)
- Every filter, sort, count, sum, average, group, and search must use LINQ methods

---

## 📐 Example Output

Here's what Report 2 (Department Summary) might look like:

```
========================================
       DEPARTMENT SUMMARY
========================================

Department       Active  Avg Salary    Total Payroll   Top Earner
------------------------------------------------------------------------
Engineering           5    $105,000       $525,000      Sarah Chen
Marketing             3     $78,333       $235,000      James Wilson
Sales                 4     $67,500       $270,000      Maria Lopez
HR                    2     $72,500       $145,000      Patricia Brown
------------------------------------------------------------------------
Company Total:       14     $83,929     $1,175,000

Departments above company average: Engineering
```

---

## 🏗️ Starter Template

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Department { get; set; }
    public string Position { get; set; }
    public decimal Salary { get; set; }
    public DateTime HireDate { get; set; }
    public bool IsActive { get; set; }

    public Employee(int id, string name, string department,
                    string position, decimal salary,
                    DateTime hireDate, bool isActive)
    {
        Id = id;
        Name = name;
        Department = department;
        Position = position;
        Salary = salary;
        HireDate = hireDate;
        IsActive = isActive;
    }

    public int YearsOfService =>
        (int)((DateTime.Now - HireDate).TotalDays / 365.25);

    public override string ToString()
    {
        string status = IsActive ? "Active" : "Inactive";
        return $"{Name,-20} | {Department,-15} | {Position,-20} | " +
               $"{Salary,10:C0} | {YearsOfService} yrs | {status}";
    }
}

class Program
{
    static List<Employee> employees = new List<Employee>();

    static void Main()
    {
        LoadEmployees();
        RunMenu();
    }

    static void LoadEmployees()
    {
        // TODO: Add at least 15 employees
        employees.Add(new Employee(1, "Sarah Chen", "Engineering",
            "Senior Developer", 120000m,
            new DateTime(2018, 3, 15), true));

        // Add more employees here...
    }

    static void RunMenu()
    {
        bool running = true;
        while (running)
        {
            Console.WriteLine("\n========================================");
            Console.WriteLine("    EMPLOYEE REPORT GENERATOR");
            Console.WriteLine("========================================\n");
            Console.WriteLine("1. Employee Directory");
            Console.WriteLine("2. Department Summary");
            Console.WriteLine("3. Salary Analysis");
            Console.WriteLine("4. Seniority Report");
            Console.WriteLine("5. Search Employees");
            Console.WriteLine("6. Custom Filter");
            Console.WriteLine("7. Exit\n");
            Console.Write("Choose a report (1-7): ");

            string choice = Console.ReadLine() ?? "";

            switch (choice)
            {
                case "1": EmployeeDirectory(); break;
                case "2": DepartmentSummary(); break;
                case "3": SalaryAnalysis(); break;
                case "4": SeniorityReport(); break;
                case "5": SearchEmployees(); break;
                case "6": CustomFilter(); break;
                case "7": running = false; break;
                default:
                    Console.WriteLine("Invalid choice. Please try again.");
                    break;
            }
        }

        Console.WriteLine("\nGoodbye!");
    }

    static void EmployeeDirectory()
    {
        // TODO: Implement using LINQ
    }

    static void DepartmentSummary()
    {
        // TODO: Implement using LINQ
    }

    static void SalaryAnalysis()
    {
        // TODO: Implement using LINQ
    }

    static void SeniorityReport()
    {
        // TODO: Implement using LINQ
    }

    static void SearchEmployees()
    {
        // TODO: Implement using LINQ
    }

    static void CustomFilter()
    {
        // TODO: Implement using LINQ
    }
}
```

---

## 📊 Grading Rubric

| Criteria | Points |
|----------|--------|
| **Employee class** — All properties, constructor, YearsOfService, ToString | 10 |
| **Sample data** — At least 15 employees, 4+ departments, mixed data | 10 |
| **Report 1** — Employee Directory with correct sorting | 10 |
| **Report 2** — Department Summary with grouping and aggregation | 15 |
| **Report 3** — Salary Analysis with brackets and comparisons | 15 |
| **Report 4** — Seniority Report with correct date calculations | 10 |
| **Report 5** — Search with case-insensitive multi-field matching | 10 |
| **Report 6** — Custom Filter with user input and dynamic query building | 10 |
| **LINQ usage** — All data processing uses LINQ (no loops for filtering/sorting) | 5 |
| **Code quality** — Clean formatting, meaningful names, no code duplication | 5 |
| **Total** | **100** |

---

## 💡 Hints

1. **GroupBy for Report 2:** Group employees by department, then use aggregation methods on each group.

2. **Salary brackets:** You can use `GroupBy` with a conditional:
   ```csharp
   .GroupBy(e => e.Salary switch
   {
       < 50000m => "Under $50K",
       < 75000m => "$50K - $75K",
       < 100000m => "$75K - $100K",
       _ => "$100K+"
   })
   ```

3. **Median calculation:** Sort the salaries, then pick the middle element:
   ```csharp
   var sorted = salaries.OrderBy(s => s).ToList();
   decimal median = sorted[sorted.Count / 2];
   ```

4. **Case-insensitive search:** Use `.Contains(term, StringComparison.OrdinalIgnoreCase)` or convert both to lowercase with `.ToLower()`.

5. **Custom filter:** Build the query step by step:
   ```csharp
   IEnumerable<Employee> query = employees;

   if (department != "All")
       query = query.Where(e => e.Department == department);

   if (activeOnly)
       query = query.Where(e => e.IsActive);

   // Apply sort at the end
   var results = query.OrderBy(e => e.Name).ToList();
   ```

6. **Formatting columns:** Use string alignment:
   ```csharp
   Console.WriteLine($"{name,-20} {salary,10:C0} {years,5} years");
   ```

---

## 🏆 Bonus Challenges

1. **Export to CSV:** Add a menu option to export any report's data to a CSV file using LINQ to format the lines.

2. **Salary percentile:** For each employee, calculate what percentile their salary falls in (e.g., "Sarah Chen earns more than 85% of employees").

3. **Year-over-year hiring:** Use `GroupBy` on hire year to show a hiring timeline — how many employees were hired each year.

4. **Department comparison:** Show a side-by-side comparison of two departments selected by the user.

5. **Attrition analysis:** Among inactive employees, show which department had the most departures and the average tenure of departed employees.

---

[Back to Week 14 Overview](./README.md)
