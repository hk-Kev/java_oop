# Java OOP Cheatsheet – Exam Ready (Single File `Main.java`)

## Table of Contents
- [Purpose & Student Mindset](#purpose--student-mindset)
- [How to Solve Any Exam Question in 5 Steps](#how-to-solve-any-exam-question-in-5-steps)
- [Copy-Pasteable Code Blocks](#copy-pasteable-code-blocks)
  - [Class 1: BankBranch](#class-1-bankbranch)
  - [Class 2: Customer (with Constructor Chaining)](#class-2-customer-with-constructor-chaining)
  - [Class 3: LoanOfficer (with Object Reference)](#class-3-loanofficer-with-object-reference)
  - [Class 4: LoanProduct (with Method Overloading)](#class-4-loanproduct-with-method-overloading)
  - [Class 5: Guarantor](#class-5-guarantor)
  - [Class 6: LoanApplication](#class-6-loanapplication)
  - [Class 7: LoanRepayment](#class-7-loanrepayment)
  - [Class 8: Main (Menu, Plain Arrays, Input Loops)](#class-8-main-menu-plain-arrays-input-loops)
- [Quick Exam Tips & Corner-Cutting Checklist](#quick-exam-tips--corner-cutting-checklist)

---

## Purpose & Student Mindset

This cheatsheet is crafted for a **2–3 hour university OOP exam**. 
- **Zero bloat**: No unnecessary classes, enums, or complex enterprise patterns.
- **Fast typing**: Domain classes are clean 1-line POJOs with full encapsulation.
- **Input retry loops in `Main`**: If the user enters invalid data (negative numbers, letters, out-of-range ages), the console **loops on that specific field until they get it right** instead of crashing or restarting the whole form.
- **Parallel `String[]` for Status**: Status is tracked simply using `String[] appStatus` (`"PENDING"`, `"APPROVED"`, `"REJECTED"`).
- **Universal Java**: Standard `switch-case` compatible with all Java versions (Java 8 to 21+).
- **Single file**: All classes are written to live together inside a single `Main.java` file.

---

## How to Solve Any Exam Question in 5 Steps

1. **Copy Domain Class Templates**: For each required class, declare 5 `private` attributes, write the constructor, 1-line getters/setters, and `toString()`.
2. **Setup Array Storage in `Main`**: Declare `ClassName[] list = new ClassName[100]; int count = 0;`.
3. **Copy the 3 Input Helpers**: `readString()`, `readInt()`, and `readDouble()`. They use `try-catch` so user typos never crash your program.
4. **Write Registration with `while (true)` Validation**: Prompt the user, check conditions (`if (valid) break;`), and create the object.
5. **Add Transaction / Summary Logic**: For bookings or loans, lookup objects by ID, check business rules with `if / else`, and print reports.

---

## Copy-Pasteable Code Blocks

```java
// ==========================================
// SECTION: CLASS 1 - BankBranch
// ==========================================
class BankBranch {
    private int branchId;
    private String branchName;
    private String branchCode;
    private String branchLocation;
    private String branchManager;

    public BankBranch(int branchId, String branchName, String branchCode, String branchLocation, String branchManager) {
        this.branchId = branchId;
        this.branchName = branchName;
        this.branchCode = branchCode;
        this.branchLocation = branchLocation;
        this.branchManager = branchManager;
    }

    public int getBranchId() { return branchId; }
    public void setBranchId(int branchId) { this.branchId = branchId; }

    public String getBranchName() { return branchName; }
    public void setBranchName(String branchName) { this.branchName = branchName; }

    public String getBranchCode() { return branchCode; }
    public void setBranchCode(String branchCode) { this.branchCode = branchCode; }

    public String getBranchLocation() { return branchLocation; }
    public void setBranchLocation(String branchLocation) { this.branchLocation = branchLocation; }

    public String getBranchManager() { return branchManager; }
    public void setBranchManager(String branchManager) { this.branchManager = branchManager; }

    @Override
    public String toString() {
        return "BankBranch [ID=" + branchId + ", Name=" + branchName + ", Code=" + branchCode + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 2 - Customer (Constructor Overloading & Chaining)
// ==========================================
class Customer {
    private int customerId;
    private String customerName;
    private String customerEmail;
    private int customerAge;
    private double monthlyIncome;

    // Full constructor
    public Customer(int customerId, String customerName, String customerEmail, int customerAge, double monthlyIncome) {
        this.customerId = customerId;
        this.customerName = customerName;
        this.customerEmail = customerEmail;
        this.customerAge = customerAge;
        this.monthlyIncome = monthlyIncome;
    }

    // Overloaded constructor with constructor chaining using this(...)
    public Customer(int customerId, String customerName, int customerAge) {
        this(customerId, customerName, "Not provided", customerAge, 0.0);
    }

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

    @Override
    public String toString() {
        return "Customer [ID=" + customerId + ", Name=" + customerName + ", Age=" + customerAge + ", Income=" + monthlyIncome + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 3 - LoanOfficer (Object Association)
// ==========================================
class LoanOfficer {
    private int officerId;
    private String officerName;
    private String officerEmail;
    private int yearsOfExperience;
    private BankBranch branch; // Association

    public LoanOfficer(int officerId, String officerName, String officerEmail, int yearsOfExperience, BankBranch branch) {
        this.officerId = officerId;
        this.officerName = officerName;
        this.officerEmail = officerEmail;
        this.yearsOfExperience = yearsOfExperience;
        this.branch = branch;
    }

    public int getOfficerId() { return officerId; }
    public void setOfficerId(int officerId) { this.officerId = officerId; }

    public String getOfficerName() { return officerName; }
    public void setOfficerName(String officerName) { this.officerName = officerName; }

    public String getOfficerEmail() { return officerEmail; }
    public void setOfficerEmail(String officerEmail) { this.officerEmail = officerEmail; }

    public int getYearsOfExperience() { return yearsOfExperience; }
    public void setYearsOfExperience(int yearsOfExperience) { this.yearsOfExperience = yearsOfExperience; }

    public BankBranch getBranch() { return branch; }
    public void setBranch(BankBranch branch) { this.branch = branch; }

    @Override
    public String toString() {
        return "LoanOfficer [ID=" + officerId + ", Name=" + officerName + ", Branch=" + (branch != null ? branch.getBranchName() : "None") + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 4 - LoanProduct (Method Overloading)
// ==========================================
class LoanProduct {
    private int productId;
    private String productName;
    private double interestRate;
    private double maximumLoanAmount;
    private int maximumRepaymentMonths;

    public LoanProduct(int productId, String productName, double interestRate, double maximumLoanAmount, int maximumRepaymentMonths) {
        this.productId = productId;
        this.productName = productName;
        this.interestRate = interestRate;
        this.maximumLoanAmount = maximumLoanAmount;
        this.maximumRepaymentMonths = maximumRepaymentMonths;
    }

    // Method 1: Default calculation using product's own rate and months
    public double calculateRepayable(double principal) {
        return calculateRepayable(principal, this.interestRate, this.maximumRepaymentMonths);
    }

    // Method 2 (Overloaded): Calculation with custom rate and months
    public double calculateRepayable(double principal, double annualRate, int months) {
        double interest = principal * (annualRate / 100.0) * (months / 12.0);
        return principal + interest;
    }

    public int getProductId() { return productId; }
    public void setProductId(int productId) { this.productId = productId; }

    public String getProductName() { return productName; }
    public void setProductName(String productName) { this.productName = productName; }

    public double getInterestRate() { return interestRate; }
    public void setInterestRate(double interestRate) { this.interestRate = interestRate; }

    public double getMaximumLoanAmount() { return maximumLoanAmount; }
    public void setMaximumLoanAmount(double maximumLoanAmount) { this.maximumLoanAmount = maximumLoanAmount; }

    public int getMaximumRepaymentMonths() { return maximumRepaymentMonths; }
    public void setMaximumRepaymentMonths(int maximumRepaymentMonths) { this.maximumRepaymentMonths = maximumRepaymentMonths; }

    @Override
    public String toString() {
        return "LoanProduct [ID=" + productId + ", Name=" + productName + ", Rate=" + interestRate + "%, MaxAmt=" + maximumLoanAmount + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 5 - Guarantor
// ==========================================
class Guarantor {
    private int guarantorId;
    private String guarantorName;
    private String guarantorEmail;
    private String guarantorPhone;
    private double monthlyIncome;

    public Guarantor(int guarantorId, String guarantorName, String guarantorEmail, String guarantorPhone, double monthlyIncome) {
        this.guarantorId = guarantorId;
        this.guarantorName = guarantorName;
        this.guarantorEmail = guarantorEmail;
        this.guarantorPhone = guarantorPhone;
        this.monthlyIncome = monthlyIncome;
    }

    public int getGuarantorId() { return guarantorId; }
    public void setGuarantorId(int guarantorId) { this.guarantorId = guarantorId; }

    public String getGuarantorName() { return guarantorName; }
    public void setGuarantorName(String guarantorName) { this.guarantorName = guarantorName; }

    public String getGuarantorEmail() { return guarantorEmail; }
    public void setGuarantorEmail(String guarantorEmail) { this.guarantorEmail = guarantorEmail; }

    public String getGuarantorPhone() { return guarantorPhone; }
    public void setGuarantorPhone(String guarantorPhone) { this.guarantorPhone = guarantorPhone; }

    public double getMonthlyIncome() { return monthlyIncome; }
    public void setMonthlyIncome(double monthlyIncome) { this.monthlyIncome = monthlyIncome; }

    @Override
    public String toString() {
        return "Guarantor [ID=" + guarantorId + ", Name=" + guarantorName + ", Income=" + monthlyIncome + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 6 - LoanApplication
// ==========================================
class LoanApplication {
    private int applicationId;
    private Customer customer;
    private LoanProduct loanProduct;
    private Guarantor guarantor;
    private double requestedAmount;

    public LoanApplication(int applicationId, Customer customer, LoanProduct loanProduct, Guarantor guarantor, double requestedAmount) {
        this.applicationId = applicationId;
        this.customer = customer;
        this.loanProduct = loanProduct;
        this.guarantor = guarantor;
        this.requestedAmount = requestedAmount;
    }

    public int getApplicationId() { return applicationId; }
    public void setApplicationId(int applicationId) { this.applicationId = applicationId; }

    public Customer getCustomer() { return customer; }
    public void setCustomer(Customer customer) { this.customer = customer; }

    public LoanProduct getLoanProduct() { return loanProduct; }
    public void setLoanProduct(LoanProduct loanProduct) { this.loanProduct = loanProduct; }

    public Guarantor getGuarantor() { return guarantor; }
    public void setGuarantor(Guarantor guarantor) { this.guarantor = guarantor; }

    public double getRequestedAmount() { return requestedAmount; }
    public void setRequestedAmount(double requestedAmount) { this.requestedAmount = requestedAmount; }

    @Override
    public String toString() {
        return "LoanApplication [AppID=" + applicationId + ", Customer=" + customer.getCustomerName() + 
               ", Product=" + loanProduct.getProductName() + ", Amount=" + requestedAmount + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 7 - LoanRepayment
// ==========================================
class LoanRepayment {
    private int repaymentId;
    private LoanApplication loanApplication;
    private double repaymentAmount;
    private String repaymentDate;
    private LoanOfficer processedBy;

    public LoanRepayment(int repaymentId, LoanApplication loanApplication, double repaymentAmount, String repaymentDate, LoanOfficer processedBy) {
        this.repaymentId = repaymentId;
        this.loanApplication = loanApplication;
        this.repaymentAmount = repaymentAmount;
        this.repaymentDate = repaymentDate;
        this.processedBy = processedBy;
    }

    public int getRepaymentId() { return repaymentId; }
    public void setRepaymentId(int repaymentId) { this.repaymentId = repaymentId; }

    public LoanApplication getLoanApplication() { return loanApplication; }
    public void setLoanApplication(LoanApplication loanApplication) { this.loanApplication = loanApplication; }

    public double getRepaymentAmount() { return repaymentAmount; }
    public void setRepaymentAmount(double repaymentAmount) { this.repaymentAmount = repaymentAmount; }

    public String getRepaymentDate() { return repaymentDate; }
    public void setRepaymentDate(String repaymentDate) { this.repaymentDate = repaymentDate; }

    public LoanOfficer getProcessedBy() { return processedBy; }
    public void setProcessedBy(LoanOfficer processedBy) { this.processedBy = processedBy; }

    @Override
    public String toString() {
        return "LoanRepayment [ID=" + repaymentId + ", AppID=" + loanApplication.getApplicationId() + 
               ", Amount=" + repaymentAmount + ", Date=" + repaymentDate + "]";
    }
}
```

```java
// ==========================================
// SECTION: CLASS 8 - MAIN (Complete Menu, Storage & Validation)
// ==========================================
import java.util.Scanner;

public class Main {
    private static final int MAX = 100;

    // Plain arrays for storing records
    private static BankBranch[] branches = new BankBranch[MAX];
    private static int branchCount = 0;

    private static Customer[] customers = new Customer[MAX];
    private static int customerCount = 0;

    private static LoanOfficer[] officers = new LoanOfficer[MAX];
    private static int officerCount = 0;

    private static LoanProduct[] products = new LoanProduct[MAX];
    private static int productCount = 0;

    private static Guarantor[] guarantors = new Guarantor[MAX];
    private static int guarantorCount = 0;

    private static LoanApplication[] applications = new LoanApplication[MAX];
    private static String[] appStatus = new String[MAX]; // Parallel array for status ("PENDING", "APPROVED", "REJECTED")
    private static int applicationCount = 0;

    private static LoanRepayment[] repayments = new LoanRepayment[MAX];
    private static int repaymentCount = 0;

    private static Scanner scanner = new Scanner(System.in);

    // ==========================================
    // 3 SIMPLE INPUT HELPERS (Loops until valid input)
    // ==========================================
    private static String readString(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            String s = scanner.nextLine().trim();
            if (!s.isEmpty()) return s;
            System.out.println("Error: Cannot be blank. Please try again.");
        }
    }

    private static int readInt(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            try {
                return Integer.parseInt(scanner.nextLine().trim());
            } catch (Exception e) {
                System.out.println("Error: Please enter a valid whole number.");
            }
        }
    }

    private static double readDouble(String prompt) {
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
    // MAIN METHOD & CONSOLE MENU
    // ==========================================
    public static void main(String[] args) {
        while (true) {
            System.out.println("\n========== LOAN SYSTEM MENU ==========");
            System.out.println("1. Register Bank Branch");
            System.out.println("2. Register Customer");
            System.out.println("3. Register Loan Officer");
            System.out.println("4. Register Loan Product");
            System.out.println("5. Register Guarantor");
            System.out.println("6. Submit Loan Application");
            System.out.println("7. Review Loan Application");
            System.out.println("8. Approve / Reject Application");
            System.out.println("9. Record Loan Repayment");
            System.out.println("10. View Loan Summary / Records");
            System.out.println("0. Exit");
            System.out.println("======================================");

            int choice = readInt("Enter your choice");

            switch (choice) {
                case 1:
                    registerBranch();
                    break;
                case 2:
                    registerCustomer();
                    break;
                case 3:
                    registerOfficer();
                    break;
                case 4:
                    registerProduct();
                    break;
                case 5:
                    registerGuarantor();
                    break;
                case 6:
                    submitApplication();
                    break;
                case 7:
                    reviewApplication();
                    break;
                case 8:
                    decideApplication();
                    break;
                case 9:
                    recordRepayment();
                    break;
                case 10:
                    displaySummary();
                    break;
                case 0:
                    System.out.println("Exiting application. Goodbye!");
                    return;
                default:
                    System.out.println("Invalid option! Please choose between 0 and 10.");
            }
        }
    }

    // ==========================================
    // REGISTRATION METHODS (Input + Retry Loops)
    // ==========================================
    private static void registerBranch() {
        System.out.println("\n--- Register Bank Branch ---");
        if (branchCount >= MAX) { System.out.println("Storage full!"); return; }

        int id;
        while (true) {
            id = readInt("Enter Branch ID (>0)");
            if (id <= 0) {
                System.out.println("Branch ID must be positive.");
            } else if (findBranchIndex(id) != -1) {
                System.out.println("Branch ID already exists! Enter a unique ID.");
            } else {
                break;
            }
        }

        String name = readString("Enter Branch Name");
        String code = readString("Enter Branch Code");
        String location = readString("Enter Branch Location");
        String manager = readString("Enter Branch Manager");

        branches[branchCount++] = new BankBranch(id, name, code, location, manager);
        System.out.println("Branch registered successfully!");
    }

    private static void registerCustomer() {
        System.out.println("\n--- Register Customer ---");
        if (customerCount >= MAX) { System.out.println("Storage full!"); return; }

        int id;
        while (true) {
            id = readInt("Enter Customer ID (>0)");
            if (id <= 0) {
                System.out.println("Customer ID must be positive.");
            } else if (findCustomerIndex(id) != -1) {
                System.out.println("Customer ID already exists! Enter a unique ID.");
            } else {
                break;
            }
        }

        String name = readString("Enter Customer Name");

        String email;
        while (true) {
            email = readString("Enter Customer Email");
            if (email.contains("@") && email.contains(".")) break;
            System.out.println("Invalid email format (must contain @ and .). Try again.");
        }

        int age;
        while (true) {
            age = readInt("Enter Customer Age (18 - 100)");
            if (age >= 18 && age <= 100) break;
            System.out.println("Age must be between 18 and 100.");
        }

        double income;
        while (true) {
            income = readDouble("Enter Monthly Income (>0)");
            if (income > 0) break;
            System.out.println("Monthly income must be positive.");
        }

        customers[customerCount++] = new Customer(id, name, email, age, income);
        System.out.println("Customer registered successfully!");
    }

    private static void registerOfficer() {
        System.out.println("\n--- Register Loan Officer ---");
        if (officerCount >= MAX) { System.out.println("Storage full!"); return; }
        if (branchCount == 0) { System.out.println("Please register at least one Bank Branch first!"); return; }

        int id;
        while (true) {
            id = readInt("Enter Officer ID (>0)");
            if (id <= 0) {
                System.out.println("Officer ID must be positive.");
            } else if (findOfficerIndex(id) != -1) {
                System.out.println("Officer ID already exists! Enter a unique ID.");
            } else {
                break;
            }
        }

        String name = readString("Enter Officer Name");

        String email;
        while (true) {
            email = readString("Enter Officer Email");
            if (email.contains("@") && email.contains(".")) break;
            System.out.println("Invalid email format.");
        }

        int exp;
        while (true) {
            exp = readInt("Enter Years of Experience (>=0)");
            if (exp >= 0) break;
            System.out.println("Experience cannot be negative.");
        }

        int bIdx;
        while (true) {
            int branchId = readInt("Enter Branch ID to assign officer");
            bIdx = findBranchIndex(branchId);
            if (bIdx != -1) break;
            System.out.println("Branch not found! Try an existing branch ID.");
        }

        officers[officerCount++] = new LoanOfficer(id, name, email, exp, branches[bIdx]);
        System.out.println("Loan Officer registered successfully!");
    }

    private static void registerProduct() {
        System.out.println("\n--- Register Loan Product ---");
        if (productCount >= MAX) { System.out.println("Storage full!"); return; }

        int id;
        while (true) {
            id = readInt("Enter Product ID (>0)");
            if (id <= 0) {
                System.out.println("Product ID must be positive.");
            } else if (findProductIndex(id) != -1) {
                System.out.println("Product ID already exists!");
            } else {
                break;
            }
        }

        String name = readString("Enter Product Name");

        double rate;
        while (true) {
            rate = readDouble("Enter Annual Interest Rate (0 to 30%)");
            if (rate > 0 && rate <= 30) break;
            System.out.println("Interest rate must be > 0 and <= 30.");
        }

        double maxAmt;
        while (true) {
            maxAmt = readDouble("Enter Maximum Loan Amount (>0)");
            if (maxAmt > 0) break;
            System.out.println("Max loan amount must be positive.");
        }

        int maxMonths;
        while (true) {
            maxMonths = readInt("Enter Maximum Repayment Months (1 to 120)");
            if (maxMonths >= 1 && maxMonths <= 120) break;
            System.out.println("Months must be between 1 and 120.");
        }

        products[productCount++] = new LoanProduct(id, name, rate, maxAmt, maxMonths);
        System.out.println("Loan Product registered successfully!");
    }

    private static void registerGuarantor() {
        System.out.println("\n--- Register Guarantor ---");
        if (guarantorCount >= MAX) { System.out.println("Storage full!"); return; }

        int id;
        while (true) {
            id = readInt("Enter Guarantor ID (>0)");
            if (id <= 0) {
                System.out.println("Guarantor ID must be positive.");
            } else if (findGuarantorIndex(id) != -1) {
                System.out.println("Guarantor ID already exists!");
            } else {
                break;
            }
        }

        String name = readString("Enter Guarantor Name");

        String email;
        while (true) {
            email = readString("Enter Guarantor Email");
            if (email.contains("@") && email.contains(".")) break;
            System.out.println("Invalid email format.");
        }

        String phone = readString("Enter Guarantor Phone");

        double income;
        while (true) {
            income = readDouble("Enter Guarantor Monthly Income (>0)");
            if (income > 0) break;
            System.out.println("Income must be positive.");
        }

        guarantors[guarantorCount++] = new Guarantor(id, name, email, phone, income);
        System.out.println("Guarantor registered successfully!");
    }

    // ==========================================
    // LOAN WORKFLOW & BUSINESS LOGIC
    // ==========================================
    private static void submitApplication() {
        System.out.println("\n--- Submit Loan Application ---");
        if (applicationCount >= MAX) { System.out.println("Storage full!"); return; }
        if (customerCount == 0 || productCount == 0 || guarantorCount == 0) {
            System.out.println("Please register Customer, Loan Product, and Guarantor first!");
            return;
        }

        int appId;
        while (true) {
            appId = readInt("Enter Application ID (>0)");
            if (appId <= 0) {
                System.out.println("Application ID must be positive.");
            } else if (findApplicationIndex(appId) != -1) {
                System.out.println("Application ID already exists!");
            } else {
                break;
            }
        }

        int custIdx;
        while (true) {
            int custId = readInt("Enter Customer ID");
            custIdx = findCustomerIndex(custId);
            if (custIdx != -1) break;
            System.out.println("Customer not found! Try again.");
        }

        int prodIdx;
        while (true) {
            int prodId = readInt("Enter Product ID");
            prodIdx = findProductIndex(prodId);
            if (prodIdx != -1) break;
            System.out.println("Product not found! Try again.");
        }

        int guarIdx;
        while (true) {
            int guarId = readInt("Enter Guarantor ID");
            guarIdx = findGuarantorIndex(guarId);
            if (guarIdx != -1) break;
            System.out.println("Guarantor not found! Try again.");
        }

        Customer cust = customers[custIdx];
        LoanProduct prod = products[prodIdx];
        Guarantor guar = guarantors[guarIdx];

        // Eligibility Check 1: Customer cannot be their own guarantor
        if (cust.getCustomerId() == guar.getGuarantorId()) {
            System.out.println("Rejection: Customer cannot act as their own guarantor!");
            return;
        }

        // Eligibility Check 2: Customer age >= 21
        if (cust.getCustomerAge() < 21) {
            System.out.println("Rejection: Customer must be at least 21 years old to apply.");
            return;
        }

        // Eligibility Check 3: Guarantor income >= 30% of customer income
        if (guar.getMonthlyIncome() < (0.30 * cust.getMonthlyIncome())) {
            System.out.println("Rejection: Guarantor income must be at least 30% of customer's income.");
            return;
        }

        // Requested Amount with checks
        double amount;
        while (true) {
            amount = readDouble("Enter Requested Loan Amount");
            if (amount <= 0) {
                System.out.println("Amount must be positive.");
            } else if (amount > prod.getMaximumLoanAmount()) {
                System.out.println("Rejection: Amount exceeds Product maximum of " + prod.getMaximumLoanAmount());
            } else if (amount > (12 * cust.getMonthlyIncome())) {
                System.out.println("Rejection: Amount exceeds 12 times customer monthly income (" + (12 * cust.getMonthlyIncome()) + ")");
            } else {
                break;
            }
        }

        // Demonstrate explicit casting requirement (cast double to int for display)
        int castedAmount = (int) amount;
        System.out.println("Application processed. Rounded Loan Amount: " + castedAmount);

        applications[applicationCount] = new LoanApplication(appId, cust, prod, guar, amount);
        appStatus[applicationCount] = "PENDING";
        applicationCount++;
        System.out.println("Application submitted successfully with status: PENDING");
    }

    private static void reviewApplication() {
        System.out.println("\n--- Review Loan Application ---");
        int appId = readInt("Enter Application ID to review");
        int idx = findApplicationIndex(appId);
        if (idx == -1) {
            System.out.println("Application not found.");
            return;
        }
        System.out.println(applications[idx]);
        System.out.println("Current Status: " + appStatus[idx]);
    }

    private static void decideApplication() {
        System.out.println("\n--- Approve / Reject Application ---");
        int appId = readInt("Enter Application ID to decide");
        int idx = findApplicationIndex(appId);
        if (idx == -1) {
            System.out.println("Application not found.");
            return;
        }
        if (!"PENDING".equals(appStatus[idx])) {
            System.out.println("Decision failed: Only PENDING applications can be decided!");
            return;
        }

        while (true) {
            String decision = readString("Enter decision: (A)pprove or (R)eject").toUpperCase();
            if (decision.equals("A")) {
                appStatus[idx] = "APPROVED";
                System.out.println("Application has been APPROVED.");
                break;
            } else if (decision.equals("R")) {
                appStatus[idx] = "REJECTED";
                System.out.println("Application has been REJECTED.");
                break;
            } else {
                System.out.println("Invalid choice! Enter 'A' or 'R'.");
            }
        }
    }

    private static void recordRepayment() {
        System.out.println("\n--- Record Loan Repayment ---");
        if (repaymentCount >= MAX) { System.out.println("Storage full!"); return; }

        int appId = readInt("Enter Application ID");
        int appIdx = findApplicationIndex(appId);
        if (appIdx == -1) {
            System.out.println("Application not found.");
            return;
        }
        if (!"APPROVED".equals(appStatus[appIdx])) {
            System.out.println("Rejection: Repayments can only be recorded for APPROVED applications!");
            return;
        }

        LoanApplication app = applications[appIdx];
        double totalRepayable = app.getLoanProduct().calculateRepayable(app.getRequestedAmount());

        // Calculate how much has already been repaid
        double totalRepaidSoFar = 0.0;
        for (int i = 0; i < repaymentCount; i++) {
            if (repayments[i].getLoanApplication().getApplicationId() == app.getApplicationId()) {
                totalRepaidSoFar += repayments[i].getRepaymentAmount();
            }
        }

        double remainingBalance = totalRepayable - totalRepaidSoFar;
        if (remainingBalance <= 0) {
            System.out.println("Loan is already fully repaid! Outstanding balance: 0.0");
            return;
        }

        System.out.println("Total Repayable: " + totalRepayable + " | Paid so far: " + totalRepaidSoFar + " | Remaining: " + remainingBalance);

        int repId;
        while (true) {
            repId = readInt("Enter Repayment ID (>0)");
            if (repId <= 0) {
                System.out.println("Repayment ID must be positive.");
            } else if (findRepaymentIndex(repId) != -1) {
                System.out.println("Repayment ID already exists!");
            } else {
                break;
            }
        }

        double amount;
        while (true) {
            amount = readDouble("Enter Repayment Amount");
            if (amount <= 0) {
                System.out.println("Amount must be positive.");
            } else if (amount > remainingBalance) {
                System.out.println("Rejection: Overpayment! Max payable amount is " + remainingBalance);
            } else {
                break;
            }
        }

        String date = readString("Enter Repayment Date (e.g. 2026-10-22)");

        int offIdx;
        while (true) {
            int offId = readInt("Enter Officer ID processing this payment");
            offIdx = findOfficerIndex(offId);
            if (offIdx != -1) break;
            System.out.println("Officer not found! Try an existing officer ID.");
        }

        repayments[repaymentCount++] = new LoanRepayment(repId, app, amount, date, officers[offIdx]);
        System.out.println("Repayment recorded successfully! Remaining balance: " + (remainingBalance - amount));
    }

    private static void displaySummary() {
        System.out.println("\n================ LOAN SUMMARY RECORDS ================");
        if (applicationCount == 0) {
            System.out.println("No loan applications submitted yet.");
            return;
        }

        for (int i = 0; i < applicationCount; i++) {
            LoanApplication app = applications[i];
            String stat = appStatus[i];
            double totalRepayable = app.getLoanProduct().calculateRepayable(app.getRequestedAmount());

            double totalRepaid = 0.0;
            for (int j = 0; j < repaymentCount; j++) {
                if (repayments[j].getLoanApplication().getApplicationId() == app.getApplicationId()) {
                    totalRepaid += repayments[j].getRepaymentAmount();
                }
            }

            double balance = totalRepayable - totalRepaid;
            System.out.println("App ID: " + app.getApplicationId() +
                               " | Customer: " + app.getCustomer().getCustomerName() +
                               " | Product: " + app.getLoanProduct().getProductName() +
                               " | Status: " + stat +
                               " | Total Repayable: " + totalRepayable +
                               " | Total Repaid: " + totalRepaid +
                               " | Outstanding Balance: " + balance);
        }
        System.out.println("======================================================");
    }

    // ==========================================
    // LINEAR SEARCH HELPERS (Find by ID)
    // ==========================================
    private static int findBranchIndex(int id) {
        for (int i = 0; i < branchCount; i++) if (branches[i].getBranchId() == id) return i;
        return -1;
    }

    private static int findCustomerIndex(int id) {
        for (int i = 0; i < customerCount; i++) if (customers[i].getCustomerId() == id) return i;
        return -1;
    }

    private static int findOfficerIndex(int id) {
        for (int i = 0; i < officerCount; i++) if (officers[i].getOfficerId() == id) return i;
        return -1;
    }

    private static int findProductIndex(int id) {
        for (int i = 0; i < productCount; i++) if (products[i].getProductId() == id) return i;
        return -1;
    }

    private static int findGuarantorIndex(int id) {
        for (int i = 0; i < guarantorCount; i++) if (guarantors[i].getGuarantorId() == id) return i;
        return -1;
    }

    private static int findApplicationIndex(int id) {
        for (int i = 0; i < applicationCount; i++) if (applications[i].getApplicationId() == id) return i;
        return -1;
    }

    private static int findRepaymentIndex(int id) {
        for (int i = 0; i < repaymentCount; i++) if (repayments[i].getRepaymentId() == id) return i;
        return -1;
    }
}
```

---

## Quick Exam Tips & Corner-Cutting Checklist

| Task | Student Shortcut |
|---|---|
| **Adding a new class** | Copy any class above. Keep 5 `private` attributes, constructor, 1-line getters/setters, and `toString()`. Takes under 60 seconds. |
| **Constructor Chaining** | Just write `this(id, name, "Not provided", age, 0.0);` inside the smaller constructor. |
| **Input Crash Prevention** | Always use the 3 helpers: `readString()`, `readInt()`, and `readDouble()`. Never use raw `scanner.nextInt()` (it causes newline buffer bugs). |
| **Input Retries** | Use `while (true) { int val = readInt(...); if (condition) break; print("Error"); }`. |
| **Explicit Casting Requirement** | Just write `int rounded = (int) doubleValue;` before saving or printing. |
| **Searching Records** | Use the 2-line `for` loop helper: `for (int i = 0; i < count; i++) if (arr[i].getId() == id) return i; return -1;`. |
| **Status Tracking** | Use a simple `String[] status = new String[MAX];` and store `"PENDING"`, `"APPROVED"`, or `"REJECTED"`. |
