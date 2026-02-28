# Week 7 – Assignment: Contact Manager

[← Back to Week 7 Overview](./README.md)

---

## 📋 Overview

Build a **Contact Manager** — a console application that lets users create, view, search, and manage a list of contacts. This project brings together everything from Week 7: classes, properties, constructors, constructor overloading, the `this` keyword, objects stored in lists, and multi-class design.

---

## 🎯 Learning Goals

This assignment will test your ability to:

- Design a class with properties (including validation)
- Write constructors (default and parameterized) with chaining
- Store objects in a `List<T>`
- Write methods that operate on a collection of objects
- Build a menu-driven console application using a loop

---

## 📐 Requirements

### The `Contact` Class

Create a `Contact` class with the following:

| Property | Type | Rules |
|----------|------|-------|
| `Name` | string | Required — cannot be empty |
| `Phone` | string | Required — cannot be empty |
| `Email` | string | Optional — can be empty, defaults to "(none)" |
| `Category` | string | Must be "Friend", "Family", "Work", or "Other" — defaults to "Other" |

**Constructors:**
1. `Contact(string name, string phone, string email, string category)` — full constructor with validation
2. `Contact(string name, string phone)` — chains to full constructor, defaults email to "(none)" and category to "Other"

**Methods:**
- `PrintContact()` — displays the contact in a formatted way
- `MatchesSearch(string keyword)` — returns `true` if the name, phone, or email contains the keyword (case-insensitive)

### The `ContactManager` Class

Create a `ContactManager` class with:

| Member | Type | Purpose |
|--------|------|---------|
| `Contacts` | List\<Contact\> | Stores all contacts |
| `AddContact(Contact contact)` | void | Adds a contact to the list |
| `DisplayAllContacts()` | void | Prints all contacts with numbering |
| `SearchContacts(string keyword)` | void | Finds and displays matching contacts |
| `GetContactCount()` | int | Returns the total number of contacts |
| `GetCategoryCount(string category)` | int | Returns how many contacts are in a specific category |

### The Main Program

Build a **menu-driven console application** with this menu:

```
╔════════════════════════════════╗
║       📇 Contact Manager       ║
╠════════════════════════════════╣
║  1. Add a new contact          ║
║  2. View all contacts          ║
║  3. Search contacts            ║
║  4. View statistics            ║
║  5. Exit                       ║
╚════════════════════════════════╝
```

**Menu option details:**

1. **Add a new contact** — Ask for name, phone, email (optional), and category (show valid options). Create a `Contact` and add it to the manager.
2. **View all contacts** — Display all contacts in a formatted list. Show a message if no contacts exist.
3. **Search contacts** — Ask for a search keyword and display all matching contacts.
4. **View statistics** — Show total contacts and breakdown by category.
5. **Exit** — Display a goodbye message and end the program.

---

## 📝 Example Output

```
╔════════════════════════════════╗
║       📇 Contact Manager       ║
╠════════════════════════════════╣
║  1. Add a new contact          ║
║  2. View all contacts          ║
║  3. Search contacts            ║
║  4. View statistics            ║
║  5. Exit                       ║
╚════════════════════════════════╝

Choose an option: 1

--- Add New Contact ---
Name: Alice Johnson
Phone: 555-1234
Email (press Enter to skip): alice@email.com
Category (Friend/Family/Work/Other): Friend

✅ Contact "Alice Johnson" added successfully!

Choose an option: 1

--- Add New Contact ---
Name: Bob Smith
Phone: 555-5678
Email (press Enter to skip):
Category (Friend/Family/Work/Other): Work

✅ Contact "Bob Smith" added successfully!

Choose an option: 1

--- Add New Contact ---
Name: Carol Johnson
Phone: 555-9999
Email (press Enter to skip): carol@company.com
Category (Friend/Family/Work/Other): Work

✅ Contact "Carol Johnson" added successfully!

Choose an option: 2

📋 All Contacts (3)
════════════════════════════════
  1. Alice Johnson
     📞 555-1234 | ✉️ alice@email.com
     📁 Friend

  2. Bob Smith
     📞 555-5678 | ✉️ (none)
     📁 Work

  3. Carol Johnson
     📞 555-9999 | ✉️ carol@company.com
     📁 Work
════════════════════════════════

Choose an option: 3

--- Search Contacts ---
Enter search keyword: Johnson

🔍 Search Results for "Johnson" (2 found):
────────────────────────────────
  1. Alice Johnson
     📞 555-1234 | ✉️ alice@email.com
     📁 Friend

  2. Carol Johnson
     📞 555-9999 | ✉️ carol@company.com
     📁 Work

Choose an option: 4

📊 Contact Statistics
════════════════════════════════
Total Contacts: 3
  👫 Friend:  1
  👨‍👩‍👧 Family:  0
  💼 Work:    2
  📌 Other:   0
════════════════════════════════

Choose an option: 5

👋 Goodbye! Your contacts have been saved... just kidding, not yet. 😄
```

---

## 🧩 Starter Template

```csharp
// ============================================
// Contact Manager — Week 7 Assignment
// ============================================

// --- Main Program ---
ContactManager manager = new ContactManager();
bool running = true;

while (running)
{
    Console.WriteLine();
    Console.WriteLine("╔════════════════════════════════╗");
    Console.WriteLine("║       📇 Contact Manager       ║");
    Console.WriteLine("╠════════════════════════════════╣");
    Console.WriteLine("║  1. Add a new contact          ║");
    Console.WriteLine("║  2. View all contacts          ║");
    Console.WriteLine("║  3. Search contacts            ║");
    Console.WriteLine("║  4. View statistics            ║");
    Console.WriteLine("║  5. Exit                       ║");
    Console.WriteLine("╚════════════════════════════════╝");
    Console.WriteLine();

    Console.Write("Choose an option: ");
    string choice = Console.ReadLine();

    switch (choice)
    {
        case "1":
            // TODO: Ask for contact details, create Contact, add to manager
            break;
        case "2":
            // TODO: Call manager.DisplayAllContacts()
            break;
        case "3":
            // TODO: Ask for keyword, call manager.SearchContacts(keyword)
            break;
        case "4":
            // TODO: Display statistics
            break;
        case "5":
            running = false;
            Console.WriteLine("\n👋 Goodbye!");
            break;
        default:
            Console.WriteLine("❌ Invalid option. Please choose 1-5.");
            break;
    }
}

// --- Contact Class ---
class Contact
{
    // TODO: Properties with validation
    // TODO: Constructors (full + chained)
    // TODO: PrintContact() method
    // TODO: MatchesSearch(string keyword) method
}

// --- ContactManager Class ---
class ContactManager
{
    // TODO: List<Contact> Contacts
    // TODO: AddContact(), DisplayAllContacts(), SearchContacts()
    // TODO: GetContactCount(), GetCategoryCount()
}
```

---

## 📊 Grading Rubric

| Criteria | Points |
|----------|--------|
| **Contact class** — properties, validation, constructors with chaining | 25 |
| **ContactManager class** — list management, all required methods | 25 |
| **Menu system** — loop, switch, all 5 options working | 20 |
| **Search functionality** — case-insensitive, searches name/phone/email | 10 |
| **Statistics display** — total count + category breakdown | 10 |
| **Code quality** — naming conventions, readable structure, comments | 10 |
| **Total** | **100** |

---

## 💡 Hints

1. **Case-insensitive search:** Use `.ToLower()` on both the keyword and the values you're searching:
   ```csharp
   public bool MatchesSearch(string keyword)
   {
       string lower = keyword.ToLower();
       return Name.ToLower().Contains(lower) ||
              Phone.ToLower().Contains(lower) ||
              Email.ToLower().Contains(lower);
   }
   ```

2. **Reading optional input:** Check if the user pressed Enter without typing:
   ```csharp
   Console.Write("Email (press Enter to skip): ");
   string email = Console.ReadLine();
   if (string.IsNullOrWhiteSpace(email))
       email = "(none)";
   ```

3. **Validating category:** Use a loop to keep asking until they enter a valid category:
   ```csharp
   string category;
   do
   {
       Console.Write("Category (Friend/Family/Work/Other): ");
       category = Console.ReadLine();
   } while (category != "Friend" && category != "Family" &&
            category != "Work" && category != "Other");
   ```

4. **Constructor chaining reminder:**
   ```csharp
   public Contact(string name, string phone) : this(name, phone, "(none)", "Other")
   {
   }
   ```

---

## 🚀 Bonus Challenges

1. **Delete Contact:** Add option 6 to delete a contact by number. Display the contact first and ask for confirmation before deleting.

2. **Edit Contact:** Add option 7 to edit an existing contact. Show current values and let the user press Enter to keep each field unchanged.

3. **Sort Contacts:** In "View all contacts," offer sub-options to sort by name, category, or addition order.

4. **Favorite Contacts:** Add an `IsFavorite` (bool) property to `Contact`. Add a menu option to toggle favorites and another to display only favorites (⭐).

5. **Import Starter Data:** Add a method `LoadSampleData()` to `ContactManager` that pre-loads 5-6 contacts so testers don't have to manually enter data every time.

---

## 📁 Recommended File Structure

For this assignment, practice the multi-file approach:

```
ContactManager/
├── Program.cs           ← Main program with menu loop
├── Contact.cs           ← Contact class
├── ContactManager.cs    ← ContactManager class
└── ContactManager.csproj
```

---

[← Back to Week 7 Overview](./README.md)
