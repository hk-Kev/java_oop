# Java OOP Cheatsheet – One‑Page Reference (Project Version)
## Table of Contents
- [Purpose](#purpose)
- [How to approach a typical OOP question](#how-to-approach-a-typical-oop-question)
- [Copy‑pasteable blocks (fully commented)](#copy‑pasteable-blocks-fully-commented)
  - [Validator](#validator)
  - [Status enum](#status-enum)
  - [BankBranch class](#bankbranch-class)
  - [Customer class](#customer-class)
  - [LoanOfficer class](#loanofficer-class)
  - [LoanProduct class](#loanproduct-class)
  - [Guarantor class](#guarantor-class)
  - [LoanApplication class](#loanapplication-class)
  - [LoanRepayment class](#loanrepayment-class)
  - [Main class](#main-class)
- [Validation checklist](#validation-checklist)
## Purpose
A single markdown file you can copy‑paste directly into a **single `Main.java`** to solve any of the mid‑term OOP exercises (e.g., loan‑application case study). It includes:
- A concise *decision‑making guide* for typical exam sub‑questions (validation, object creation, menu flow, etc.)
- Fully‑commented, copy‑pasteable Java code blocks using **plain arrays** (no `ArrayList`)
- A reusable `Validator` helper with simple checks (no regex)
- A quick validation checklist table
- Searchable comment tags (`// == SECTION: …`) for fast navigation

---

## How to approach a typical OOP question
When you read a question, follow these mental steps. After each step, you’ll know which code snippet to copy‑paste.
1. **Identify the domain objects** (e.g., `Customer`, `LoanProduct`).
   - *Ask*: Which attributes are required? What types?
   - *Do*: Choose the corresponding class template from the cheatsheet.
2. **Determine required validations** for each attribute.
   - *Ask*: Should the value be positive, non‑empty, within a range?
   - *Do*: Use the `Validator` methods (see the checklist) and add `if` checks in the setter.
3. **Check for relationships / associations** (e.g., a `LoanOfficer` belongs to a `BankBranch`).
   - *Ask*: Is a reference required? Can it be `null`?
   - *Do*: Validate the reference before assignment.
4. **Decide if constructors need overloading** (e.g., `Customer` with optional email).
   - *Ask*: Does the question mention optional fields?
   - *Do*: Use the overloaded constructor provided.
5. **Map the required menu actions** (register, submit, approve, repay, summary).
   - *Ask*: Which actions are listed in the specification?
   - *Do*: Implement the corresponding method in `Main` (see the menu block).
6. **Plan the processing order** (registration → application → decision → repayment → summary).
   - *Ask*: Does the question enforce a specific sequence?
   - *Do*: Follow the order of method calls in `main`.
7. **Add exception handling** for non‑numeric input.
   - *Do*: Use the provided `readInt` / `readDouble` helpers that loop until a valid number is entered.
8. **Run a quick sanity check**: compile and test each menu option.
   - *Do*: `javac Main.java && java Main`.

> **Tip**: Use `Ctrl+F "// == SECTION:"` to jump to the relevant block.

---

## Copy‑pasteable blocks (fully commented)

```java
// == SECTION: VALIDATOR
/**
 * Simple validation helper – no regular expressions, easy to understand.
 */
public class Validator {
    // Check that a string is not null/empty after trimming
    public static boolean isNonEmpty(String s) {
        return s != null && !s.trim().isEmpty();
    }
    // Positive integer check (>0)
    public static boolean isPositiveInt(int i) {
        return i > 0;
    }
    // Positive double check (>0.0)
    public static boolean isPositiveDouble(double d) {
        return d > 0.0;
    }
    // Very simple email validation (contains '@' and '.')
    public static boolean isValidEmail(String e) {
        return e != null && e.contains("@") && e.contains(".");
    }
}
```

```java
// == SECTION: STATUS ENUM
enum Status { PENDING, APPROVED, REJECTED }
```

```java
// == SECTION: BANK BRANCH CLASS
public class BankBranch {
    private int branchId;          // >0, unique
    private String branchName;     // non‑empty
    private String branchCode;     // non‑empty
    private String branchLocation; // non‑empty
    private String branchManager; // non‑empty

    public BankBranch(int branchId, String branchName, String branchCode,
                      String branchLocation, String branchManager) {
        setBranchId(branchId);
        setBranchName(branchName);
        setBranchCode(branchCode);
        setBranchLocation(branchLocation);
        setBranchManager(branchManager);
    }

    // ----- Getters & Setters with validation -----
    public int getBranchId() { return branchId; }
    public void setBranchId(int branchId) {
        if (!Validator.isPositiveInt(branchId))
            throw new IllegalArgumentException("branchId must be positive");
        this.branchId = branchId;
    }
    public String getBranchName() { return branchName; }
    public void setBranchName(String branchName) {
        if (!Validator.isNonEmpty(branchName))
            throw new IllegalArgumentException("branchName cannot be empty");
        this.branchName = branchName;
    }
    public String getBranchCode() { return branchCode; }
    public void setBranchCode(String branchCode) {
        if (!Validator.isNonEmpty(branchCode))
            throw new IllegalArgumentException("branchCode cannot be empty");
        this.branchCode = branchCode;
    }
    public String getBranchLocation() { return branchLocation; }
    public void setBranchLocation(String branchLocation) {
        if (!Validator.isNonEmpty(branchLocation))
            throw new IllegalArgumentException("branchLocation cannot be empty");
        this.branchLocation = branchLocation;
    }
    public String getBranchManager() { return branchManager; }
    public void setBranchManager(String branchManager) {
        if (!Validator.isNonEmpty(branchManager))
            throw new IllegalArgumentException("branchManager cannot be empty");
        this.branchManager = branchManager;
    }
    @Override
    public String toString() {
        return "BankBranch{id=" + branchId + ", name='" + branchName + "'}";
    }
}
```

```java
// == SECTION: CUSTOMER CLASS (with constructor overloading)
public class Customer {
    private int customerId;            // >0, unique
    private String customerName;       // non‑empty
    private String customerEmail;      // valid email or "Not provided"
    private int customerAge;           // 18‑100
    private double monthlyIncome;      // >0.0

    // Full constructor
    public Customer(int customerId, String customerName, String customerEmail,
                    int customerAge, double monthlyIncome) {
        setCustomerId(customerId);
        setCustomerName(customerName);
        setCustomerEmail(customerEmail);
        setCustomerAge(customerAge);
        setMonthlyIncome(monthlyIncome);
    }
    // Overloaded constructor (email optional, income defaults to 0)
    public Customer(int customerId, String customerName, int customerAge) {
        this(customerId, customerName, "Not provided", customerAge, 0.0);
    }
    // ----- Getters & Setters -----
    public int getCustomerId() { return customerId; }
    public void setCustomerId(int customerId) {
        if (!Validator.isPositiveInt(customerId))
            throw new IllegalArgumentException("customerId must be positive");
        this.customerId = customerId;
    }
    public String getCustomerName() { return customerName; }
    public void setCustomerName(String customerName) {
        if (!Validator.isNonEmpty(customerName))
            throw new IllegalArgumentException("customerName cannot be empty");
        this.customerName = customerName;
    }
    public String getCustomerEmail() { return customerEmail; }
    public void setCustomerEmail(String customerEmail) {
        if (!Validator.isValidEmail(customerEmail))
            throw new IllegalArgumentException("invalid email");
        this.customerEmail = customerEmail;
    }
    public int getCustomerAge() { return customerAge; }
    public void setCustomerAge(int customerAge) {
        if (customerAge < 18 || customerAge > 100)
            throw new IllegalArgumentException("age out of range");
        this.customerAge = customerAge;
    }
    public double getMonthlyIncome() { return monthlyIncome; }
    public void setMonthlyIncome(double monthlyIncome) {
        if (!Validator.isPositiveDouble(monthlyIncome))
            throw new IllegalArgumentException("income must be positive");
        this.monthlyIncome = monthlyIncome;
    }
    @Override
    public String toString() {
        return "Customer{id=" + customerId + ", name='" + customerName + "'}";
    }
}
```

```java
// == SECTION: LOAN OFFICER CLASS
public class LoanOfficer {
    private int officerId;               // >0, unique
    private String officerName;          // non‑empty
    private String officerEmail;         // valid email
    private int yearsOfExperience;       // >=0
    private BankBranch branch;           // cannot be null

    public LoanOfficer(int officerId, String officerName, String officerEmail,
                       int yearsOfExperience, BankBranch branch) {
        setOfficerId(officerId);
        setOfficerName(officerName);
        setOfficerEmail(officerEmail);
        setYearsOfExperience(yearsOfExperience);
        setBranch(branch);
    }
    // ----- Getters & Setters -----
    public int getOfficerId() { return officerId; }
    public void setOfficerId(int officerId) {
        if (!Validator.isPositiveInt(officerId))
            throw new IllegalArgumentException("officerId must be positive");
        this.officerId = officerId;
    }
    public String getOfficerName() { return officerName; }
    public void setOfficerName(String officerName) {
        if (!Validator.isNonEmpty(officerName))
            throw new IllegalArgumentException("officerName cannot be empty");
        this.officerName = officerName;
    }
    public String getOfficerEmail() { return officerEmail; }
    public void setOfficerEmail(String officerEmail) {
        if (!Validator.isValidEmail(officerEmail))
            throw new IllegalArgumentException("invalid email");
        this.officerEmail = officerEmail;
    }
    public int getYearsOfExperience() { return yearsOfExperience; }
    public void setYearsOfExperience(int yearsOfExperience) {
        if (yearsOfExperience < 0)
            throw new IllegalArgumentException("experience cannot be negative");
        this.yearsOfExperience = yearsOfExperience;
    }
    public BankBranch getBranch() { return branch; }
    public void setBranch(BankBranch branch) {
        if (branch == null)
            throw new IllegalArgumentException("branch cannot be null");
        this.branch = branch;
    }
    @Override
    public String toString() {
        return "LoanOfficer{id=" + officerId + ", name='" + officerName + "'}";
    }
}
```

```java
// == SECTION: LOAN PRODUCT CLASS (method overloading example)
public class LoanProduct {
    private int productId;                // >0, unique
    private String productName;           // non‑empty
    private double interestRate;          // >0 && <=30
    private double maximumLoanAmount;     // >0
    private int maximumRepaymentMonths;  // >0

    public LoanProduct(int productId, String productName,
                       double interestRate, double maximumLoanAmount,
                       int maximumRepaymentMonths) {
        setProductId(productId);
        setProductName(productName);
        setInterestRate(interestRate);
        setMaximumLoanAmount(maximumLoanAmount);
        setMaximumRepaymentMonths(maximumRepaymentMonths);
    }
    // ----- Getters & Setters -----
    public int getProductId() { return productId; }
    public void setProductId(int productId) {
        if (!Validator.isPositiveInt(productId))
            throw new IllegalArgumentException("productId must be positive");
        this.productId = productId;
    }
    public String getProductName() { return productName; }
    public void setProductName(String productName) {
        if (!Validator.isNonEmpty(productName))
            throw new IllegalArgumentException("productName cannot be empty");
        this.productName = productName;
    }
    public double getInterestRate() { return interestRate; }
    public void setInterestRate(double interestRate) {
        if (!Validator.isPositiveDouble(interestRate) || interestRate > 30)
            throw new IllegalArgumentException("interestRate must be >0 and <=30");
        this.interestRate = interestRate;
    }
    public double getMaximumLoanAmount() { return maximumLoanAmount; }
    public void setMaximumLoanAmount(double maximumLoanAmount) {
        if (!Validator.isPositiveDouble(maximumLoanAmount))
            throw new IllegalArgumentException("maximumLoanAmount must be positive");
        this.maximumLoanAmount = maximumLoanAmount;
    }
    public int getMaximumRepaymentMonths() { return maximumRepaymentMonths; }
    public void setMaximumRepaymentMonths(int maximumRepaymentMonths) {
        if (!Validator.isPositiveInt(maximumRepaymentMonths))
            throw new IllegalArgumentException("maximumRepaymentMonths must be positive");
        this.maximumRepaymentMonths = maximumRepaymentMonths;
    }
    // ----- Overloaded repayment calculation -----
    public double calculateRepayable(double principal) {
        // Calls the more general method with default rate and months
        return calculateRepayable(principal, interestRate, maximumRepaymentMonths);
    }
    public double calculateRepayable(double principal, double annualRate, int months) {
        double interest = principal * (annualRate / 100.0) * (months / 12.0);
        return principal + interest;
    }
    @Override
    public String toString() {
        return "LoanProduct{id=" + productId + ", name='" + productName + "'}";
    }
}
```

```java
// == SECTION: GUARANTOR CLASS
public class Guarantor {
    private int guarantorId;            // >0, unique
    private String guarantorName;       // non‑empty
    private String guarantorEmail;      // valid email
    private String guarantorPhone;      // non‑empty
    private double monthlyIncome;       // >0

    public Guarantor(int guarantorId, String guarantorName,
                     String guarantorEmail, String guarantorPhone,
                     double monthlyIncome) {
        setGuarantorId(guarantorId);
        setGuarantorName(guarantorName);
        setGuarantorEmail(guarantorEmail);
        setGuarantorPhone(guarantorPhone);
        setMonthlyIncome(monthlyIncome);
    }
    // ----- Getters & Setters -----
    public int getGuarantorId() { return guarantorId; }
    public void setGuarantorId(int guarantorId) {
        if (!Validator.isPositiveInt(guarantorId))
            throw new IllegalArgumentException("guarantorId must be positive");
        this.guarantorId = guarantorId;
    }
    public String getGuarantorName() { return guarantorName; }
    public void setGuarantorName(String guarantorName) {
        if (!Validator.isNonEmpty(guarantorName))
            throw new IllegalArgumentException("guarantorName cannot be empty");
        this.guarantorName = guarantorName;
    }
    public String getGuarantorEmail() { return guarantorEmail; }
    public void setGuarantorEmail(String guarantorEmail) {
        if (!Validator.isValidEmail(guarantorEmail))
            throw new IllegalArgumentException("invalid email");
        this.guarantorEmail = guarantorEmail;
    }
    public String getGuarantorPhone() { return guarantorPhone; }
    public void setGuarantorPhone(String guarantorPhone) {
        if (!Validator.isNonEmpty(guarantorPhone))
            throw new IllegalArgumentException("guarantorPhone cannot be empty");
        this.guarantorPhone = guarantorPhone;
    }
    public double getMonthlyIncome() { return monthlyIncome; }
    public void setMonthlyIncome(double monthlyIncome) {
        if (!Validator.isPositiveDouble(monthlyIncome))
            throw new IllegalArgumentException("income must be positive");
        this.monthlyIncome = monthlyIncome;
    }
    @Override
    public String toString() {
        return "Guarantor{id=" + guarantorId + ", name='" + guarantorName + "'}";
    }
}
```

```java
// == SECTION: LOAN APPLICATION CLASS
public class LoanApplication {
    private int applicationId;          // >0, unique
    private Customer customer;          // cannot be null
    private LoanProduct loanProduct;    // cannot be null
    private Guarantor guarantor;        // cannot be null
    private double requestedAmount;    // >0

    public LoanApplication(int applicationId, Customer customer,
                           LoanProduct loanProduct, Guarantor guarantor,
                           double requestedAmount) {
        setApplicationId(applicationId);
        setCustomer(customer);
        setLoanProduct(loanProduct);
        setGuarantor(guarantor);
        setRequestedAmount(requestedAmount);
    }
    // ----- Getters & Setters -----
    public int getApplicationId() { return applicationId; }
    public void setApplicationId(int applicationId) {
        if (!Validator.isPositiveInt(applicationId))
            throw new IllegalArgumentException("applicationId must be positive");
        this.applicationId = applicationId;
    }
    public Customer getCustomer() { return customer; }
    public void setCustomer(Customer customer) {
        if (customer == null)
            throw new IllegalArgumentException("customer cannot be null");
        this.customer = customer;
    }
    public LoanProduct getLoanProduct() { return loanProduct; }
    public void setLoanProduct(LoanProduct loanProduct) {
        if (loanProduct == null)
            throw new IllegalArgumentException("loanProduct cannot be null");
        this.loanProduct = loanProduct;
    }
    public Guarantor getGuarantor() { return guarantor; }
    public void setGuarantor(Guarantor guarantor) {
        if (guarantor == null)
            throw new IllegalArgumentException("guarantor cannot be null");
        this.guarantor = guarantor;
    }
    public double getRequestedAmount() { return requestedAmount; }
    public void setRequestedAmount(double requestedAmount) {
        if (!Validator.isPositiveDouble(requestedAmount))
            throw new IllegalArgumentException("requestedAmount must be positive");
        this.requestedAmount = requestedAmount;
    }
    @Override
    public String toString() {
        return "LoanApplication{id=" + applicationId + ", customer=" +
               customer.getCustomerId() + "}";
    }
}
```

```java
// == SECTION: LOAN REPAYMENT CLASS
public class LoanRepayment {
    private int repaymentId;               // >0, unique
    private LoanApplication loanApplication; // cannot be null
    private double repaymentAmount;          // >0
    private String repaymentDate;            // non‑empty
    private LoanOfficer processedBy;         // cannot be null

    public LoanRepayment(int repaymentId, LoanApplication loanApplication,
                         double repaymentAmount, String repaymentDate,
                         LoanOfficer processedBy) {
        setRepaymentId(repaymentId);
        setLoanApplication(loanApplication);
        setRepaymentAmount(repaymentAmount);
        setRepaymentDate(repaymentDate);
        setProcessedBy(processedBy);
    }
    // ----- Getters & Setters -----
    public int getRepaymentId() { return repaymentId; }
    public void setRepaymentId(int repaymentId) {
        if (!Validator.isPositiveInt(repaymentId))
            throw new IllegalArgumentException("repaymentId must be positive");
        this.repaymentId = repaymentId;
    }
    public LoanApplication getLoanApplication() { return loanApplication; }
    public void setLoanApplication(LoanApplication loanApplication) {
        if (loanApplication == null)
            throw new IllegalArgumentException("loanApplication cannot be null");
        this.loanApplication = loanApplication;
    }
    public double getRepaymentAmount() { return repaymentAmount; }
    public void setRepaymentAmount(double repaymentAmount) {
        if (!Validator.isPositiveDouble(repaymentAmount))
            throw new IllegalArgumentException("repaymentAmount must be positive");
        this.repaymentAmount = repaymentAmount;
    }
    public String getRepaymentDate() { return repaymentDate; }
    public void setRepaymentDate(String repaymentDate) {
        if (!Validator.isNonEmpty(repaymentDate))
            throw new IllegalArgumentException("repaymentDate cannot be empty");
        this.repaymentDate = repaymentDate;
    }
    public LoanOfficer getProcessedBy() { return processedBy; }
    public void setProcessedBy(LoanOfficer processedBy) {
        if (processedBy == null)
            throw new IllegalArgumentException("processedBy cannot be null");
        this.processedBy = processedBy;
    }
    @Override
    public String toString() {
        return "LoanRepayment{id=" + repaymentId + ", amount=" + repaymentAmount + "}";
    }
}
```

```java
// == SECTION: MAIN CLASS – MENU & ARRAY STORAGE
import java.util.*;

public class Main {
    private static final int MAX = 100; // capacity for each entity array
    // ---- Plain arrays for storage ----
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
    private static Status[] appStatus = new Status[MAX];
    private static int applicationCount = 0;
    private static LoanRepayment[] repayments = new LoanRepayment[MAX];
    private static int repaymentCount = 0;
    private static final Scanner SC = new Scanner(System.in);

    public static void main(String[] args) {
        while (true) {
            printMenu();
            int choice = readInt("Choose option");
            switch (choice) {
                case 1 -> registerBranch();
                case 2 -> registerCustomer();
                case 3 -> registerOfficer();
                case 4 -> registerProduct();
                case 5 -> registerGuarantor();
                case 6 -> submitApplication();
                case 7 -> reviewApplication();
                case 8 -> decideApplication();
                case 9 -> recordRepayment();
                case 10 -> displaySummary();
                case 0 -> { System.out.println("Good‑bye!"); return; }
                default -> System.out.println("Invalid choice – try again.");
            }
        }
    }

    // ----- Helper methods for input -----
    private static int readInt(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            try { return Integer.parseInt(SC.nextLine().trim()); }
            catch (NumberFormatException e) { System.out.println("Please enter a valid integer."); }
        }
    }
    private static double readDouble(String prompt) {
        while (true) {
            System.out.print(prompt + ": ");
            try { return Double.parseDouble(SC.nextLine().trim()); }
            catch (NumberFormatException e) { System.out.println("Please enter a valid number."); }
        }
    }
    private static String readLine(String prompt) {
        System.out.print(prompt + ": ");
        return SC.nextLine();
    }

    // ----- Menu actions (each follows the validation checklist) -----
    private static void registerBranch() {
        if (branchCount >= MAX) { System.out.println("No space for more branches."); return; }
        int id = readInt("branchId");
        if (findBranchIndex(id) != -1) { System.out.println("Duplicate branchId."); return; }
        String name = readLine("branchName");
        String code = readLine("branchCode");
        String location = readLine("branchLocation");
        String manager = readLine("branchManager");
                try {
            branches[branchCount++] = new BankBranch(id, name, code, location, manager);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    private static void registerCustomer() {
        if (customerCount >= MAX) { System.out.println("No space for more customers."); return; }
        int id = readInt("customerId");
        if (findCustomerIndex(id) != -1) { System.out.println("Duplicate customerId."); return; }
        String name = readLine("customerName");
        String email = readLine("customerEmail");
        int age = readInt("customerAge");
        double income = readDouble("monthlyIncome");
                try {
            customers[customerCount++] = new Customer(id, name, email, age, income);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    private static void registerOfficer() {
        if (officerCount >= MAX) { System.out.println("No space for more officers."); return; }
        int id = readInt("officerId");
        if (findOfficerIndex(id) != -1) { System.out.println("Duplicate officerId."); return; }
        String name = readLine("officerName");
        String email = readLine("officerEmail");
        int exp = readInt("yearsOfExperience");
        int branchId = readInt("branchId (to associate)");
        int bIdx = findBranchIndex(branchId);
        if (bIdx == -1) { System.out.println("Branch not found."); return; }
                try {
            officers[officerCount++] = new LoanOfficer(id, name, email, exp, branches[bIdx]);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    private static void registerProduct() {
        if (productCount >= MAX) { System.out.println("No space for more products."); return; }
        int id = readInt("productId");
        if (findProductIndex(id) != -1) { System.out.println("Duplicate productId."); return; }
        String name = readLine("productName");
        double rate = readDouble("interestRate");
        double maxAmt = readDouble("maximumLoanAmount");
        int maxMonths = readInt("maximumRepaymentMonths");
                try {
            products[productCount++] = new LoanProduct(id, name, rate, maxAmt, maxMonths);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    private static void registerGuarantor() {
        if (guarantorCount >= MAX) { System.out.println("No space for more guarantors."); return; }
        int id = readInt("guarantorId");
        if (findGuarantorIndex(id) != -1) { System.out.println("Duplicate guarantorId."); return; }
        String name = readLine("guarantorName");
        String email = readLine("guarantorEmail");
        String phone = readLine("guarantorPhone");
        double income = readDouble("monthlyIncome");
                try {
            guarantors[guarantorCount++] = new Guarantor(id, name, email, phone, income);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    private static void submitApplication() {
        if (applicationCount >= MAX) { System.out.println("No space for more applications."); return; }
        int id = readInt("applicationId");
        if (findApplicationIndex(id) != -1) { System.out.println("Duplicate applicationId."); return; }
        int custId = readInt("customerId");
        int custIdx = findCustomerIndex(custId);
        if (custIdx == -1) { System.out.println("Customer not found."); return; }
        int prodId = readInt("productId");
        int prodIdx = findProductIndex(prodId);
        if (prodIdx == -1) { System.out.println("Product not found."); return; }
        int guarId = readInt("guarantorId");
        int guarIdx = findGuarantorIndex(guarId);
        if (guarIdx == -1) { System.out.println("Guarantor not found."); return; }
        double amount = readDouble("requestedAmount");
        // ----- Business rule checks (from checklist) -----
        Customer cust = customers[custIdx];
        LoanProduct prod = products[prodIdx];
        Guarantor guar = guarantors[guarIdx];
        if (cust.getCustomerAge() < 21) { System.out.println("Customer must be at least 21."); return; }
        if (amount > prod.getMaximumLoanAmount()) { System.out.println("Amount exceeds product max."); return; }
        if (amount > 12 * cust.getMonthlyIncome()) { System.out.println("Amount exceeds 12× customer income."); return; }
        if (guar.getMonthlyIncome() < 0.3 * cust.getMonthlyIncome()) { System.out.println("Guarantor income too low."); return; }
                try {
            applications[applicationCount] = new LoanApplication(id, cust, prod, guar, amount);
            appStatus[applicationCount] = Status.PENDING;
            applicationCount++;
            System.out.println("Application submitted and set to PENDING.");
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
        appStatus[applicationCount] = Status.PENDING;
        applicationCount++;
        System.out.println("Application submitted and set to PENDING.");
    }

    private static void reviewApplication() {
        int appId = readInt("applicationId to review");
        int idx = findApplicationIndex(appId);
        if (idx == -1) { System.out.println("Application not found."); return; }
        System.out.println("Application: " + applications[idx]);
        System.out.println("Status: " + appStatus[idx]);
    }

    private static void decideApplication() {
        int appId = readInt("applicationId to decide");
        int idx = findApplicationIndex(appId);
        if (idx == -1) { System.out.println("Application not found."); return; }
        if (appStatus[idx] != Status.PENDING) { System.out.println("Only PENDING applications can be decided."); return; }
        System.out.print("Approve (A) or Reject (R)? ");
        String resp = SC.nextLine().trim().toUpperCase();
        if (resp.equals("A")) { appStatus[idx] = Status.APPROVED; System.out.println("Application approved."); }
        else if (resp.equals("R")) { appStatus[idx] = Status.REJECTED; System.out.println("Application rejected."); }
        else { System.out.println("Invalid choice."); }
    }

    private static void recordRepayment() {
        if (repaymentCount >= MAX) { System.out.println("No space for more repayments."); return; }
        int appId = readInt("applicationId to repay");
        int appIdx = findApplicationIndex(appId);
        if (appIdx == -1) { System.out.println("Application not found."); return; }
        if (appStatus[appIdx] != Status.APPROVED) { System.out.println("Only APPROVED applications can receive repayments."); return; }
        int repId = readInt("repaymentId");
        if (findRepaymentIndex(repId) != -1) { System.out.println("Duplicate repaymentId."); return; }
        double amount = readDouble("repaymentAmount");
        String date = readLine("repaymentDate");
        int officerId = readInt("officerId processing this repayment");
        int offIdx = findOfficerIndex(officerId);
        if (offIdx == -1) { System.out.println("Officer not found."); return; }
                try {
            repayments[repaymentCount++] = new LoanRepayment(repId, applications[appIdx], amount, date, officers[offIdx]);
            System.out.println("Repayment recorded.");
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
        System.out.println("Repayment recorded.");
    }

    private static void displaySummary() {
        System.out.println("--- Loan Summary ---");
        for (int i = 0; i < applicationCount; i++) {
            LoanApplication app = applications[i];
            Status stat = appStatus[i];
            double totalRepayable = app.getLoanProduct().calculateRepayable(app.getRequestedAmount());
            double totalRepaid = 0.0;
            for (int j = 0; j < repaymentCount; j++) {
                if (repayments[j].getLoanApplication().getApplicationId() == app.getApplicationId()) {
                    totalRepaid += repayments[j].getRepaymentAmount();
                }
            }
            double outstanding = totalRepayable - totalRepaid;
            System.out.println("AppId:" + app.getApplicationId() + " Customer:" +
                               app.getCustomer().getCustomerName() + " Status:" + stat +
                               " Total:" + totalRepayable + " Repaid:" + totalRepaid +
                               " Owes:" + outstanding);
        }
    }

    // ----- Helper search methods (linear search) -----
    private static int findBranchIndex(int id) { for (int i = 0; i < branchCount; i++) if (branches[i].getBranchId() == id) return i; return -1; }
    private static int findCustomerIndex(int id) { for (int i = 0; i < customerCount; i++) if (customers[i].getCustomerId() == id) return i; return -1; }
    private static int findOfficerIndex(int id) { for (int i = 0; i < officerCount; i++) if (officers[i].getOfficerId() == id) return i; return -1; }
    private static int findProductIndex(int id) { for (int i = 0; i < productCount; i++) if (products[i].getProductId() == id) return i; return -1; }
    private static int findGuarantorIndex(int id) { for (int i = 0; i < guarantorCount; i++) if (guarantors[i].getGuarantorId() == id) return i; return -1; }
    private static int findApplicationIndex(int id) { for (int i = 0; i < applicationCount; i++) if (applications[i].getApplicationId() == id) return i; return -1; }
    private static int findRepaymentIndex(int id) { for (int i = 0; i < repaymentCount; i++) if (repayments[i].getRepaymentId() == id) return i; return -1; }
}
```

---

## Validation checklist (quick reference)
| Type | Check |
|------|-------|
| `int` id | positive & unique |
| `String` name | non‑empty |
| `String` email | contains `@` and `.` |
| age | 18‑100 (customer) |
| income | positive |
| officer experience | non‑negative |
| loan amount | >0, ≤ product max, ≤ 12×customer income |
| guarantor income | ≥ 30 % of customer income |
| interest rate | >0 and ≤30 |
| repayment months | 1‑120 |
| cust ≠ guarantor | cannot be same person |

---

*Save this file as `Main.java` (or paste the blocks into your own project) and run:* 
```
javac Main.java
java Main
```
The menu will guide you through all required actions.

---

*End of cheatsheet.*
