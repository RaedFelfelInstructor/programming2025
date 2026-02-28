# Week 8 – Assignment: Bank Account System

[← Back to Week 8 Overview](./README.md)

---

## 📋 Overview

Build a **Bank Account System** — a console application that lets users create bank accounts, make deposits and withdrawals, transfer money between accounts, and view account statements. This assignment brings together everything from Week 8: encapsulation, validation, object behavior, and object interaction.

---

## 🎯 Learning Goals

- Design classes with proper encapsulation (private fields, validated properties)
- Add meaningful behavior through methods
- Have objects interact with each other (transfers between accounts)
- Use `ToString()` to control object display
- Build a menu-driven console application

---

## 📐 Requirements

### Class 1: `Transaction`

Represents a single transaction (deposit, withdrawal, or transfer).

| Member | Type | Details |
|--------|------|---------|
| `Date` | `DateTime` | Read-only, set automatically to `DateTime.Now` |
| `Type` | `string` | "Deposit", "Withdrawal", or "Transfer" |
| `Amount` | `decimal` | The transaction amount |
| `Description` | `string` | Brief description (e.g., "Deposit", "Transfer to #1002") |
| `BalanceAfter` | `decimal` | Account balance after this transaction |
| `ToString()` | | Format: `"2025-03-15  Deposit        +$200.00    Balance: $1,200.00"` |

### Class 2: `BankAccount`

Represents a single bank account with full encapsulation.

| Member | Type | Details |
|--------|------|---------|
| `AccountNumber` | `int` | Read-only, set in constructor |
| `OwnerName` | `string` | Validated — cannot be empty |
| `Balance` | `decimal` | Read-only from outside — only changed through methods |
| `AccountType` | `string` | "Checking" or "Savings" — validated |
| Transaction history | `List<Transaction>` | Private — stores all transactions |

**Methods:**

| Method | Returns | Description |
|--------|---------|-------------|
| `Deposit(decimal amount)` | `void` | Validates amount > 0, updates balance, records transaction |
| `Withdraw(decimal amount)` | `bool` | Validates amount > 0, checks sufficient funds, returns success |
| `Transfer(BankAccount target, decimal amount)` | `bool` | Withdraws from this account, deposits to target — one operation |
| `GetTransactionCount()` | `int` | Returns number of transactions |
| `PrintStatement()` | `void` | Prints formatted account statement with all transactions |
| `ToString()` | `string` | `"#1001 — Alice Johnson (Checking) — Balance: $1,500.00"` |

**Validation rules:**
- Deposit amount must be positive
- Withdrawal amount must be positive and ≤ balance
- Transfer amount must be positive, ≤ balance, and target cannot be the same account
- Owner name cannot be empty
- Account type must be "Checking" or "Savings"

### Class 3: `Bank`

Manages a collection of bank accounts.

| Member | Type | Details |
|--------|------|---------|
| `BankName` | `string` | Name of the bank |
| Account list | `List<BankAccount>` | Private list of all accounts |
| Next account number | `int` | Private, starts at 1001, auto-increments |

**Methods:**

| Method | Returns | Description |
|--------|---------|-------------|
| `CreateAccount(string owner, string type, decimal initialDeposit)` | `BankAccount` | Creates account with auto-generated number |
| `FindAccount(int accountNumber)` | `BankAccount` | Returns account or `null` |
| `GetTotalDeposits()` | `decimal` | Sum of all account balances |
| `GetAccountCount()` | `int` | Total number of accounts |
| `PrintAllAccounts()` | `void` | Formatted list of all accounts |

### Main Program (Menu System)

Create a menu-driven console application with these options:

1. **Create Account** — Ask for owner name, account type, and initial deposit
2. **Deposit** — Ask for account number and amount
3. **Withdraw** — Ask for account number and amount
4. **Transfer** — Ask for source account, target account, and amount
5. **View Account Statement** — Ask for account number, show full statement
6. **View All Accounts** — Show summary of all accounts
7. **Exit**

---

## 📝 Example Output

```
╔═══════════════════════════════════╗
║      🏦 First National Bank       ║
╠═══════════════════════════════════╣
║  1. Create Account                ║
║  2. Deposit                       ║
║  3. Withdraw                      ║
║  4. Transfer                      ║
║  5. View Account Statement        ║
║  6. View All Accounts             ║
║  7. Exit                          ║
╚═══════════════════════════════════╝

Choose an option: 1

--- Create New Account ---
Owner name: Alice Johnson
Account type (Checking/Savings): Checking
Initial deposit: 1000

✅ Account #1001 created for Alice Johnson (Checking) with $1,000.00

Choose an option: 1

--- Create New Account ---
Owner name: Bob Smith
Account type (Checking/Savings): Savings
Initial deposit: 500

✅ Account #1002 created for Bob Smith (Savings) with $500.00

Choose an option: 2

--- Deposit ---
Account number: 1001
Amount: 250

✅ Deposited $250.00 to account #1001. New balance: $1,250.00

Choose an option: 3

--- Withdraw ---
Account number: 1001
Amount: 100

✅ Withdrew $100.00 from account #1001. New balance: $1,150.00

Choose an option: 4

--- Transfer ---
From account number: 1001
To account number: 1002
Amount: 300

✅ Transferred $300.00 from #1001 to #1002

Choose an option: 5

--- Account Statement ---
Account number: 1001

╔══════════════════════════════════════════════════════╗
║  Account Statement — #1001                           ║
║  Owner: Alice Johnson                                ║
║  Type:  Checking                                     ║
╠══════════════════════════════════════════════════════╣
║  Date        Type          Amount      Balance       ║
║──────────────────────────────────────────────────────║
║  2025-03-15  Deposit       +$1,000.00  $1,000.00    ║
║  2025-03-15  Deposit       +$250.00    $1,250.00    ║
║  2025-03-15  Withdrawal    -$100.00    $1,150.00    ║
║  2025-03-15  Transfer      -$300.00    $850.00      ║
║              to #1002                                ║
╠══════════════════════════════════════════════════════╣
║  Current Balance: $850.00                            ║
║  Total Transactions: 4                               ║
╚══════════════════════════════════════════════════════╝

Choose an option: 6

📋 All Accounts at First National Bank
══════════════════════════════════════════
  #1001 — Alice Johnson (Checking) — Balance: $850.00
  #1002 — Bob Smith (Savings) — Balance: $800.00
══════════════════════════════════════════
  Total Deposits: $1,650.00
  Total Accounts: 2

Choose an option: 7

👋 Thank you for banking with First National Bank!
```

---

## 🧩 Starter Template

```csharp
// ============================================
// Bank Account System — Week 8 Assignment
// ============================================

// --- Transaction Class ---
class Transaction
{
    // TODO: Properties (Date, Type, Amount, Description, BalanceAfter)
    // TODO: Constructor
    // TODO: ToString()
}

// --- BankAccount Class ---
class BankAccount
{
    // TODO: Private fields + validated properties
    // TODO: Private List<Transaction> for history
    // TODO: Constructor (account number, owner, type, initial deposit)
    // TODO: Deposit(), Withdraw(), Transfer()
    // TODO: PrintStatement()
    // TODO: ToString()
}

// --- Bank Class ---
class Bank
{
    // TODO: Private List<BankAccount> and next account number counter
    // TODO: Constructor (bank name)
    // TODO: CreateAccount(), FindAccount()
    // TODO: GetTotalDeposits(), GetAccountCount()
    // TODO: PrintAllAccounts()
}

// --- Main Program ---
Bank bank = new Bank("First National Bank");
bool running = true;

while (running)
{
    Console.WriteLine();
    Console.WriteLine("╔═══════════════════════════════════╗");
    Console.WriteLine("║      🏦 First National Bank       ║");
    Console.WriteLine("╠═══════════════════════════════════╣");
    Console.WriteLine("║  1. Create Account                ║");
    Console.WriteLine("║  2. Deposit                       ║");
    Console.WriteLine("║  3. Withdraw                      ║");
    Console.WriteLine("║  4. Transfer                      ║");
    Console.WriteLine("║  5. View Account Statement        ║");
    Console.WriteLine("║  6. View All Accounts             ║");
    Console.WriteLine("║  7. Exit                          ║");
    Console.WriteLine("╚═══════════════════════════════════╝");
    Console.WriteLine();

    Console.Write("Choose an option: ");
    string choice = Console.ReadLine();

    switch (choice)
    {
        case "1":
            // TODO: Ask for owner, type, initial deposit
            // TODO: Call bank.CreateAccount()
            break;
        case "2":
            // TODO: Ask for account number and amount
            // TODO: Call account.Deposit()
            break;
        case "3":
            // TODO: Ask for account number and amount
            // TODO: Call account.Withdraw()
            break;
        case "4":
            // TODO: Ask for source, target, amount
            // TODO: Call source.Transfer(target, amount)
            break;
        case "5":
            // TODO: Ask for account number
            // TODO: Call account.PrintStatement()
            break;
        case "6":
            // TODO: Call bank.PrintAllAccounts()
            break;
        case "7":
            running = false;
            Console.WriteLine("\n👋 Thank you for banking with First National Bank!");
            break;
        default:
            Console.WriteLine("❌ Invalid option. Please choose 1-7.");
            break;
    }
}
```

---

## 📊 Grading Rubric

| Criteria | Points |
|----------|--------|
| **Transaction class** — proper encapsulation, read-only properties, `ToString()` | 10 |
| **BankAccount class** — private fields, validated properties, `private set` on Balance | 20 |
| **BankAccount methods** — Deposit, Withdraw, Transfer with full validation | 20 |
| **BankAccount statement** — formatted output with transaction history | 10 |
| **Bank class** — account management, auto-numbering, find, statistics | 15 |
| **Menu system** — all 7 options working, input handling | 15 |
| **Code quality** — naming conventions, encapsulation, readable structure | 10 |
| **Total** | **100** |

---

## 💡 Hints

1. **Auto-incrementing account numbers:** Use a private field in `Bank` that increments each time `CreateAccount()` is called:
   ```csharp
   private int nextAccountNumber = 1001;

   public BankAccount CreateAccount(string owner, string type, decimal initialDeposit)
   {
       BankAccount account = new BankAccount(nextAccountNumber, owner, type, initialDeposit);
       nextAccountNumber++;
       // ... add to list
       return account;
   }
   ```

2. **Transfer is two operations:** A transfer from account A to account B is really:
   - Withdraw from A
   - Deposit to B
   - But if the withdrawal fails, don't do the deposit!
   ```csharp
   public bool Transfer(BankAccount target, decimal amount)
   {
       if (target == this)
       {
           Console.WriteLine("Cannot transfer to the same account.");
           return false;
       }
       // ... validate and process
   }
   ```

3. **Parsing decimal input:** Use `decimal.TryParse()` to safely convert user input:
   ```csharp
   Console.Write("Amount: ");
   if (!decimal.TryParse(Console.ReadLine(), out decimal amount))
   {
       Console.WriteLine("Invalid amount.");
       break;
   }
   ```

4. **String formatting for currency:** Use `:C` for currency format and padding for alignment:
   ```csharp
   Console.WriteLine($"{"Deposit",-15} +{amount,10:C}  {balance,12:C}");
   ```

---

## 🌟 Bonus Challenges

1. **Interest Calculation:** Add a `CalculateInterest(double annualRate)` method to `BankAccount` that adds monthly interest (annualRate / 12) to savings accounts only.

2. **Overdraft Protection:** Checking accounts can go up to $100 negative (overdraft), but savings accounts cannot go below $0. Show a warning when overdraft is used.

3. **Transaction Filtering:** Add a method `GetTransactionsByType(string type)` that returns only deposits, withdrawals, or transfers.

4. **Date Range Statement:** Add `PrintStatement(DateTime from, DateTime to)` that shows only transactions within a date range.

5. **Account Summary Report:** Add a method to `Bank` that prints a full report: total assets, average balance, account type breakdown, account with highest/lowest balance.

---

[← Back to Week 8 Overview](./README.md)
