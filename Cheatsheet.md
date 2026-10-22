# Java OOP Cheatsheet – Exam Ready (Single File `Main.java`)

## Table of Contents
- [Purpose & Student Mindset](#purpose--student-mindset)
- [How to Solve Any Exam Question in 5 Steps](#how-to-solve-any-exam-question-in-5-steps)
- [Copy-Pasteable Code Blocks](#copy-pasteable-code-blocks)
  - [The Universal Domain Class Template (5 Attributes, Chaining, Getters/Setters)](#the-universal-domain-class-template)
  - [Main Class (Array Storage, Input Loops, Menu & Workflow)](#main-class-array-storage-input-loops-menu--workflow)
- [Quick Exam Tips & Corner-Cutting Checklist](#quick-exam-tips--corner-cutting-checklist)

---

## Purpose & Student Mindset

This cheatsheet is crafted for a **2–3 hour university OOP exam**. 
- **1 Universal Domain Class Template**: Instead of typing 7 separate repetitive classes, use this single blueprint for every entity (`Customer`, `Bus`, `Doctor`, `Product`, etc.).
- **No unnecessary keywords in `Main`**: Removed `private`, `static`, and `final MAX`. Arrays are declared directly with size `[100]`.
- **Fast typing**: Domain classes are clean 1-line POJOs with full encapsulation (`private` attributes, getters/setters).
- **Input retry loops in `Main`**: The console loops on each prompt until valid input is given — no crashes, no resetting.
- **Single file**: Everything lives together in one `Main.java`.

---

## How to Solve Any Exam Question in 5 Steps

1. **Copy the Domain Class Template**: For each noun in the prompt (e.g. `Customer`, `Bus`, `Route`), copy the template, set its 5 attributes, constructor, getters/setters, and `toString()`.
2. **Setup Array Storage in `Main`**: Declare `ClassName[] list = new ClassName[100]; int count = 0;`.
3. **Copy the 3 Input Helpers**: `readString()`, `readInt()`, and `readDouble()`. They catch bad input automatically.
4. **Write Registration with `while (true)` Validation**: Prompt the user, check conditions (`if (valid) break;`), and create the object.
5. **Add Transaction / Summary Logic**: Retrieve objects by ID, apply business rules with `if / else`, and print results.

---

## Copy-Pasteable Code Blocks

### The Universal Domain Class Template
*Use this exact template for any class in your exam (`Customer`, `Bus`, `Driver`, `Route`, `Booking`, etc.). It covers all 5 attributes, encapsulation, constructor overloading, and constructor chaining `this(...)`.*

```java
// ==========================================
// UNIVERSAL DOMAIN CLASS TEMPLATE (5 Attributes)
// ==========================================
class Customer {
    // 1. Exactly 5 private attributes (required for Encapsulation)
    private int customerId;
    private String customerName;
    private String customerEmail;
    private int customerAge;
    private double monthlyIncome; // Can also be an object reference, e.g. private Branch branch;

    // 2. Full Parameterized Constructor
    public Customer(int customerId, String customerName, String customerEmail, int customerAge, double monthlyIncome) {
        this.customerId = customerId;
        this.customerName = customerName;
        this.customerEmail = customerEmail;
        this.customerAge = customerAge;
        this.monthlyIncome = monthlyIncome;
    }

    // 3. Overloaded Constructor demonstrating Constructor Chaining via this(...)
    public Customer(int customerId, String customerName, int customerAge) {
        this(customerId, customerName, "Not provided", customerAge, 0.0);
    }

    // 4. One-line Getters and Setters (Fast to type, satisfies OOP rules)
    public int getCustomerId() { return customerId; }
    public void setCustomerId(int customerId) { this.customerId = customerId; }

    public String getCustomerName() { return customerName; }
    public void setCustomerName(String customerName) { this.customerName = customerName; }

    public String getCustomerEmail() { return customerEmail; }
    public void setCustomerEmail(String customerEmail) { this.customerEmail = customerEmail; }

    public int getCustomerAge() { return customerAge; }
    public void setCustomerAge(int customerAge) { this.customerAge = customerAge; }

    public double getMonthlyIncome() { return monthlyIncome; }
    public void setMonthlyIncome(double monthlyIncome) { this.monthlyIncome = monthlyIncome; }

    // 5. toString() for easy display
    @Override
    public String toString() {
        return "Customer [ID=" + customerId + ", Name=" + customerName + ", Age=" + customerAge + ", Income=" + monthlyIncome + "]";
    }
}
```

---

### Main Class (Array Storage, Input Loops, Menu & Workflow)
*Notice: No `private`, no `static` on fields or helper methods. Each array directly holds 100 items.*

```java
// ==========================================
// SECTION: MAIN CLASS (Menu, Storage & Input Loops)
// ==========================================
import java.util.Scanner;

public class Main {
    // Arrays sized directly to 100 (NO static, NO private, NO MAX constant needed!)
    Customer[] customers = new Customer[100];
    int customerCount = 0;

    String[] appStatus = new String[100]; // Parallel status array ("PENDING", "APPROVED", "REJECTED")

    Scanner scanner = new Scanner(System.in);

    // ==========================================
    // ENTRY POINT: Only main has 'static' (required by Java JVM)
    // ==========================================
    public static void main(String[] args) {
        Main app = new Main();
        app.startMenu();
    }

    // ==========================================
    // 3 INPUT HELPERS (Crash-proof, loops until valid)
    // ==========================================
    String readString(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            String s = scanner.nextLine().trim();
            if (!s.isEmpty()) return s;
            System.out.println("Error: Cannot be blank. Please try again.");
        }
    }

    int readInt(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            try {
                return Integer.parseInt(scanner.nextLine().trim());
            } catch (Exception e) {
                System.out.println("Error: Please enter a valid whole number.");
            }
        }
    }

    double readDouble(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            try {
                return Double.parseDouble(scanner.nextLine().trim());
            } catch (Exception e) {
                System.out.println("Error: Please enter a valid decimal number.");
            }
        }
    }

    // ==========================================
    // CONSOLE MENU
    // ==========================================
    void startMenu() {
        while (true) {
            System.out.println("\n========== MANAGEMENT SYSTEM MENU ==========");
            System.out.println("1. Register Record");
            System.out.println("2. View Records / Summary");
            System.out.println("0. Exit");
            System.out.println("============================================");

            int choice = readInt("Enter your choice");

            switch (choice) {
                case 1:
                    registerCustomer();
                    break;
                case 2:
                    displaySummary();
                    break;
                case 0:
                    System.out.println("Exiting application. Goodbye!");
                    return;
                default:
                    System.out.println("Invalid option! Please try again.");
            }
        }
    }

    // ==========================================
    // REGISTRATION WITH INPUT RETRY LOOPS
    // ==========================================
    void registerCustomer() {
        System.out.println("\n--- Register Customer ---");
        if (customerCount >= 100) { 
            System.out.println("Storage full!"); 
            return; 
        }

        // 1. Positive & Unique ID Loop
        int id;
        while (true) {
            id = readInt("Enter Customer ID (>0)");
            if (id <= 0) {
                System.out.println("ID must be positive.");
            } else if (findCustomerIndex(id) != -1) {
                System.out.println("ID already exists! Enter a unique ID.");
            } else {
                break;
            }
        }

        // 2. Mandatory Non-blank Name
        String name = readString("Enter Customer Name");

        // 3. Valid Email Loop
        String email;
        while (true) {
            email = readString("Enter Customer Email");
            if (email.contains("@") && email.contains(".")) break;
            System.out.println("Invalid email format (must contain @ and .). Try again.");
        }

        // 4. Age Range Loop (18 - 100)
        int age;
        while (true) {
            age = readInt("Enter Customer Age (18 - 100)");
            if (age >= 18 && age <= 100) break;
            System.out.println("Age must be between 18 and 100.");
        }

        // 5. Positive Double Loop
        double income;
        while (true) {
            income = readDouble("Enter Monthly Income (>0)");
            if (income > 0) break;
            System.out.println("Income must be positive.");
        }

        // Store into plain array & track initial status
        customers[customerCount] = new Customer(id, name, email, age, income);
        appStatus[customerCount] = "PENDING";
        customerCount++;

        System.out.println("Customer registered successfully!");
    }

    // ==========================================
    // DISPLAY / SUMMARY METHOD
    // ==========================================
    void displaySummary() {
        System.out.println("\n================ REGISTERED RECORDS ================");
        if (customerCount == 0) {
            System.out.println("No records registered yet.");
            return;
        }

        for (int i = 0; i < customerCount; i++) {
            System.out.println(customers[i] + " | Status: " + appStatus[i]);
        }
        System.out.println("====================================================");
    }

    // ==========================================
    // LINEAR SEARCH HELPER (2 lines: find by ID)
    // ==========================================
    int findCustomerIndex(int id) {
        for (int i = 0; i < customerCount; i++) {
            if (customers[i].getCustomerId() == id) return i;
        }
        return -1;
    }
}
```

---

## Quick Exam Tips & Corner-Cutting Checklist

| Task | Student Shortcut |
|---|---|
| **Adding a new class** | Copy the Universal Class Template. Rename the class and change the 5 fields. Takes under 60 seconds. |
| **Object Relationships** | Make one attribute an object reference (e.g. `private Bus bus;`), prompt for `busId`, find it in the array, and pass it to the constructor. |
| **Constructor Chaining** | Just write `this(id, name, "Not provided", age, 0.0);` inside the smaller constructor. |
| **Input Crash Prevention** | Always use `readString()`, `readInt()`, and `readDouble()`. Never use raw `scanner.nextInt()` (prevents newline bugs). |
| **Input Retries** | Use `while (true) { int val = readInt(...); if (condition) break; System.out.println("Error"); }`. |
| **Explicit Casting** | Just write `int rounded = (int) doubleValue;` before saving or printing. |
| **Searching Records** | Use the 2-line `for` loop helper: `for (int i = 0; i < count; i++) if (arr[i].getId() == id) return i; return -1;`. |
| **Status Tracking** | Use `String[] appStatus = new String[100];` and store `"PENDING"`, `"APPROVED"`, or `"REJECTED"`. |
