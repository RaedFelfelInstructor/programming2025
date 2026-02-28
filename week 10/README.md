# Week 10 – Polymorphism and Abstract Classes

[← Back to Course Home](../../README.md)

---

## 📋 Overview

Last week you learned **inheritance** — how a derived class can reuse and extend a base class. This week, you'll discover the real payoff of that idea: **polymorphism**. Polymorphism means you can write code that works with a base type, and it automatically does the right thing for each derived type at runtime. It's one of the most powerful ideas in object-oriented programming.

Here's a quick preview. Imagine you have a list of `Shape` objects — some are circles, some are rectangles, some are triangles. With polymorphism, you can call `shape.CalculateArea()` on every item in the list, and each shape calculates its area using its own formula. You don't need to check what type it is. The right method runs automatically.

You'll also learn about **abstract classes** — base classes that define a contract ("every shape must have a `CalculateArea` method") without providing a default implementation. Abstract classes force derived classes to supply their own version, which prevents bugs from incomplete subclasses.

---

## 🎯 Learning Objectives

By the end of this week, you will be able to:

1. **Explain** what polymorphism is and why it makes code more flexible
2. **Use** base class variables to hold derived class objects
3. **Write** code that calls overridden methods through base type references
4. **Define** abstract classes and abstract methods
5. **Implement** abstract methods in derived classes
6. **Design** class hierarchies using abstraction (Shape → Circle, Rectangle)
7. **Use** type checking and casting with `is` and `as`
8. **Model** a real-world domain using inheritance, polymorphism, and abstraction

---

## 📚 Materials

| # | Material | Topic |
|---|----------|-------|
| 1 | [Lecture 1 – Polymorphism: One Type, Many Forms](./lecture-1.md) | Base type references, virtual/override in action, polymorphic collections |
| 2 | [Lecture 2 – Abstract Classes and Abstract Methods](./lecture-2.md) | Abstract classes, abstract methods, designing with abstraction |
| 3 | [Lecture 3 – Type Checking, Casting, and Real-World Modeling](./lecture-3.md) | `is` and `as` operators, pattern matching, complete modeling exercise |
| 4 | [Exercises](./exercises.md) | Practice problems for each lecture |
| 5 | [Assignment](./assignment.md) | 📝 Vehicle Fleet Manager — mini-project |

---

## 🗺️ Where Are We?

```
Block 1: Language Fundamentals
  Week 1:  Getting Started with C#
  Week 2:  Variables, Data Types, and Operators
  Week 3:  Conditional Statements
  Week 4:  Loops and Iteration
  Week 5:  Methods and Modular Code
  Week 6:  Arrays and Collections

Block 2: OOP Foundations
  Week 7:  Classes and Objects
  Week 8:  Encapsulation and Object Behavior
  Week 9:  Inheritance
 ➤ Week 10: Polymorphism and Abstract Classes   ← You are here
  Week 11: Interfaces and Object Composition

Block 3: Advanced Language Topics
  Week 12: Exception Handling
  Week 13: Generics, Enums, and Nullable Types
  Week 14: LINQ and Lambda Expressions
  Week 15: Putting It All Together
```

---

## ✅ Prerequisites

Before starting this week, make sure you can:

- Define base and derived classes using inheritance (Week 9)
- Use `virtual` and `override` to change behavior in subclasses (Week 9)
- Call base class constructors with `base()` (Week 9)
- Create and use `List<T>` collections (Week 6)
- Write classes with properties, constructors, and methods (Weeks 7–8)

---

## 🏁 By the End of This Week

After completing all lectures, exercises, and the assignment, you should be able to:

- [ ] Store derived objects in a base-type variable or collection
- [ ] Call overridden methods through a base-type reference and get the correct behavior
- [ ] Create abstract classes that define a contract for derived classes
- [ ] Implement all abstract methods in concrete derived classes
- [ ] Use `is` to check an object's type at runtime
- [ ] Use `as` to safely cast between types
- [ ] Design a small class hierarchy that models a real-world domain

---

[Start with Lecture 1 →](./lecture-1.md)
