# Java OOP Cheatsheet – Exam Ready (Single File `Main.java`)

## Table of Contents
- [Purpose & Student Mindset](#purpose--student-mindset)
- [How to Solve Any Exam Question in 5 Steps](#how-to-solve-any-exam-question-in-5-steps)
- [Copy-Pasteable Code Blocks](#copy-pasteable-code-blocks)
  - [The Universal Domain Class Template](#the-universal-domain-class-template)
  - [The Main Class (Everything Inside `main` - Zero `static` Variables, Zero Objects of Main)](#the-main-class)
- [Quick Exam Tips & Corner-Cutting Checklist](#quick-exam-tips--corner-cutting-checklist)

---

## Purpose & Student Mindset

This cheatsheet is crafted for a **2–3 hour university OOP exam**. 
- **1 Universal Domain Class Template**: Covers private attributes, full constructor, constructor chaining `this(...)`, 1-line getters/setters, and `toString()`.
- **Everything inside `public static void main`**: No confusing `Main app = new Main()`, no `static` variables, no extra methods to link. All arrays, scanner, retry loops, and menu options live directly in `main`.
- **Crash-proof input retries**: If a user enters negative numbers, letters, or out-of-range ages, it loops right there until they enter the right value.
- **Single file**: All domain classes and `Main` are in one single file.

---

## How to Solve Any Exam Question in 5 Steps

1. **Copy Domain Class Templates**: For each noun in the prompt (e.g. `Customer`, `Bus`, `Route`), copy the template, set its 5 attributes, constructor, getters/setters, and `toString()`.
2. **Setup Arrays in `main`**: Declare `ClassName[] list = new ClassName[100]; int count = 0;`.
3. **Loop Menu**: Write a `while (true)` loop with options 1, 2, ... and `0` to exit.
4. **Input with `while(true)`**: For each field, read with `scanner.nextLine().trim()`, check conditions with `if`, and `break` when valid.
5. **Create & Store**: Call `new ClassName(...)`, put it in the array, and increment `count++`.

---

## Copy-Pasteable Code Blocks

### The Universal Domain Class Template
*Use this exact template for any class in your exam (`Customer`, `Bus`, `Driver`, `Route`, `Ticket`, etc.). It covers all 5 attributes, encapsulation, constructor overloading, and constructor chaining `this(...)`.*

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
    private double monthlyIncome; // Can also be an object reference (e.g. private Branch branch;)

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

### The Main Class
*Everything lives directly inside `public static void main(String[] args)`. No `static` variables, no `Main app = new Main()`, no extra methods needed.*

```java
// ==========================================
// SECTION: MAIN CLASS (Everything directly inside main)
// ==========================================
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // 1. Array storage directly inside main
        Customer[] customers = new Customer[100];
        int customerCount = 0;

        String[] appStatus = new String[100]; // Parallel status array ("PENDING", "APPROVED", "REJECTED")

        // 2. Main interactive menu loop
        while (true) {
            System.out.println("\n========== MANAGEMENT SYSTEM MENU ==========");
            System.out.println("1. Register Customer");
            System.out.println("2. View Records / Summary");
            System.out.println("0. Exit");
            System.out.println("============================================");
            System.out.print("Enter choice: ");

            int choice;
            try {
                choice = Integer.parseInt(scanner.nextLine().trim());
            } catch (Exception e) {
                System.out.println("Invalid input! Please enter a number.");
                continue;
            }

            // OPTION 1: REGISTER CUSTOMER
            if (choice == 1) {
                System.out.println("\n--- Register Customer ---");
                if (customerCount >= 100) {
                    System.out.println("Storage full!");
                    continue;
                }

                // 1. Positive & Unique ID Loop
                int id;
                while (true) {
                    System.out.print("Enter Customer ID (>0): ");
                    try {
                        id = Integer.parseInt(scanner.nextLine().trim());
                        if (id <= 0) {
                            System.out.println("ID must be positive.");
                            continue;
                        }

                        // Check duplicate ID
                        boolean duplicate = false;
                        for (int i = 0; i < customerCount; i++) {
                            if (customers[i].getCustomerId() == id) {
                                duplicate = true;
                                break;
                            }
                        }

                        if (duplicate) {
                            System.out.println("ID already exists! Enter a unique ID.");
                        } else {
                            break; // Valid and unique!
                        }
                    } catch (Exception e) {
                        System.out.println("Please enter a valid whole number.");
                    }
                }

                // 2. Mandatory Non-blank Name Loop
                String name;
                while (true) {
                    System.out.print("Enter Customer Name: ");
                    name = scanner.nextLine().trim();
                    if (!name.isEmpty()) break;
                    System.out.println("Name cannot be blank!");
                }

                // 3. Valid Email Loop
                String email;
                while (true) {
                    System.out.print("Enter Customer Email: ");
                    email = scanner.nextLine().trim();
                    if (email.contains("@") && email.contains(".")) break;
                    System.out.println("Invalid email format (must contain @ and .). Try again.");
                }

                // 4. Age Range Loop (18 - 100)
                int age;
                while (true) {
                    System.out.print("Enter Customer Age (18 - 100): ");
                    try {
                        age = Integer.parseInt(scanner.nextLine().trim());
                        if (age >= 18 && age <= 100) break;
                        System.out.println("Age must be between 18 and 100.");
                    } catch (Exception e) {
                        System.out.println("Please enter a valid whole number.");
                    }
                }

                // 5. Positive Income Loop
                double income;
                while (true) {
                    System.out.print("Enter Monthly Income (>0): ");
                    try {
                        income = Double.parseDouble(scanner.nextLine().trim());
                        if (income > 0) break;
                        System.out.println("Income must be positive.");
                    } catch (Exception e) {
                        System.out.println("Please enter a valid decimal number.");
                    }
                }

                // Store object in array
                customers[customerCount] = new Customer(id, name, email, age, income);
                appStatus[customerCount] = "PENDING";
                customerCount++;

                System.out.println("Customer registered successfully!");

            // OPTION 2: VIEW RECORDS
            } else if (choice == 2) {
                System.out.println("\n================ REGISTERED RECORDS ================");
                if (customerCount == 0) {
                    System.out.println("No records registered yet.");
                } else {
                    for (int i = 0; i < customerCount; i++) {
                        System.out.println(customers[i] + " | Status: " + appStatus[i]);
                    }
                }
                System.out.println("====================================================");

            // OPTION 0: EXIT
            } else if (choice == 0) {
                System.out.println("Exiting application. Goodbye!");
                break;

            } else {
                System.out.println("Invalid option! Please choose a valid menu number.");
            }
        }
    }
}
```

---

## Quick Exam Tips & Corner-Cutting Checklist

| Task | Student Shortcut |
|---|---|
| **Adding a new class** | Copy the Universal Class Template. Rename the class and change the 5 fields. Takes under 60 seconds. |
| **Object Relationships** | Make one attribute an object reference (e.g. `private Bus bus;`). In `main`, prompt for `busId`, search the `buses[]` array, and pass `buses[i]` into the constructor. |
| **Constructor Chaining** | Just write `this(id, name, "Not provided", age, 0.0);` inside the smaller constructor. |
| **Input Crash Prevention** | Always read input with `scanner.nextLine().trim()`, then wrap `Integer.parseInt(...)` or `Double.parseDouble(...)` in a `try-catch`. |
| **Explicit Casting** | Just write `int rounded = (int) doubleValue;` before saving or printing. |
| **Searching Records by ID** | A simple 3-line `for` loop inside `main`: `for (int i = 0; i < count; i++) { if (arr[i].getId() == id) { ... } }`. |
| **Status Tracking** | Use a plain `String[] appStatus = new String[100];` right inside `main`. |
