# SELF ASSESSMENT PRACTICE - OBJECT-ORIENTED PROGRAMMING (JAVA)

## CASE STUDY: LOAN APPLICATION MANAGEMENT SYSTEM

A financial institution intends to develop a console-based **Loan Application Management System** to manage customers, bank branches, loan officers, loan products, loan applications, guarantors, and loan repayments.

The company currently experiences challenges related to incorrect information, duplicate applications, invalid loan amounts, and unauthorized repayments. 

To address these challenges, the system must support:
- Customer, branch, officer, product, and guarantor registration
- Eligibility checks and validation
- Application review, approval, or rejection
- Repayment tracking and balance calculations
- Interactive console menus with resilient exception handling

All records must remain available throughout program execution.

---

## GENERAL HINTS & CONSTRAINTS

- **Input:** Use `Scanner` for interactive data entry.
- **Storage:** Use plain arrays for storing multiple records (capacity of at least 5 per record type). Do **not** hardcode business records.
- **Class Structure:** Create eight classes: `BankBranch`, `Customer`, `LoanOfficer`, `LoanProduct`, `Guarantor`, `LoanApplication`, `LoanRepayment`, and `Main`. Maintain the listed domain attributes (exactly 5 attributes per domain class).
- **Status Tracking:** Keep application processing status separately in `Main` (for example, a parallel `Status[]` or `String[]` indexed with `LoanApplication[]`), without adding a sixth attribute to `LoanApplication`.

---

## SECTION A: CREATE THE REQUIRED CLASSES

Develop the following eight Java classes. Each of the seven domain classes must contain **exactly five attributes** as specified below.

### Class 1: BankBranch

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `branchId` | `int` | Unique identifier, positive integer (> 0) |
| `branchName` | `String` | Non-blank name of the branch |
| `branchCode` | `String` | Unique branch code |
| `branchLocation` | `String` | Physical location / address |
| `branchManager` | `String` | Name of the branch manager |

### Class 2: Customer

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `customerId` | `int` | Unique identifier, positive integer (> 0) |
| `customerName` | `String` | Non-blank customer name |
| `customerEmail` | `String` | Basic email format (contains `@` and `.`) |
| `customerAge` | `int` | Age between 18 and 100 |
| `monthlyIncome` | `double` | Monthly income (> 0.0) |

### Class 3: LoanOfficer

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `officerId` | `int` | Unique identifier, positive integer (> 0) |
| `officerName` | `String` | Non-blank officer name |
| `officerEmail` | `String` | Valid email format |
| `yearsOfExperience` | `int` | Non-negative integer (>= 0) |
| `branch` | `BankBranch` | Reference to the assigned `BankBranch` |

### Class 4: LoanProduct

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `productId` | `int` | Unique identifier, positive integer (> 0) |
| `productName` | `String` | Non-blank product name |
| `interestRate` | `double` | Annual interest rate (0 < rate <= 30%) |
| `maximumLoanAmount` | `double` | Maximum allowable loan amount (> 0.0) |
| `maximumRepaymentMonths` | `int` | Repayment period in months (1 to 120) |

### Class 5: Guarantor

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `guarantorId` | `int` | Unique identifier, positive integer (> 0) |
| `guarantorName` | `String` | Non-blank guarantor name |
| `guarantorEmail` | `String` | Valid email format |
| `guarantorPhone` | `String` | Non-blank phone number |
| `monthlyIncome` | `double` | Monthly income (> 0.0) |

### Class 6: LoanApplication

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `applicationId` | `int` | Unique identifier, positive integer (> 0) |
| `customer` | `Customer` | Reference to the applicant `Customer` |
| `loanProduct` | `LoanProduct` | Reference to the selected `LoanProduct` |
| `guarantor` | `Guarantor` | Reference to the assigned `Guarantor` |
| `requestedAmount` | `double` | Requested loan principal (> 0.0) |

### Class 7: LoanRepayment

| Attribute | Data Type | Description / Constraints |
|---|---|---|
| `repaymentId` | `int` | Unique identifier, positive integer (> 0) |
| `loanApplication` | `LoanApplication` | Reference to the approved `LoanApplication` |
| `repaymentAmount` | `double` | Payment amount (> 0.0) |
| `repaymentDate` | `String` | Date of repayment |
| `processedBy` | `LoanOfficer` | Reference to the processing `LoanOfficer` |

### Class 8: Main

The main execution class containing:
- `public static void main(String[] args)`
- Array storage for all 7 entities plus parallel application status
- Interactive console menu and business logic execution

---

## SECTION B: CONSTRUCTORS, ENCAPSULATION AND METHODS

1. **Encapsulation:** Declare all domain-class attributes as `private`. Implement suitable public getters and setters for accessing and updating fields with validation checks.
2. **Parameterized Constructor:** Implement a full parameterized constructor in `Customer` (and each domain class) to initialize all five attributes.
3. **Constructor Overloading:** Overload the `Customer` constructor with a second constructor accepting `(int customerId, String customerName, int customerAge)`. Initialize `customerEmail` to `"Not provided"` and `monthlyIncome` to `0.0`.
4. **Constructor Chaining:** Demonstrate constructor chaining by calling `this(...)` from the shorter constructor to the full constructor.
5. **Method Overloading in LoanProduct:**
   - `calculateRepayable(double principal)`: Calculates total repayable using the product's own `interestRate` and `maximumRepaymentMonths`.
   - `calculateRepayable(double principal, double annualRate, int months)`: Calculates total repayable using custom rate and months.
   - **Formula:**
     $$\text{Simple Interest} = \text{principal} \times \left(\frac{\text{annualRate}}{100}\right) \times \left(\frac{\text{months}}{12.0}\right)$$
     $$\text{Total Repayable} = \text{principal} + \text{Simple Interest}$$
   - Both overloaded methods must be utilized in the program.
6. **Explicit Casting:** Demonstrate explicit type casting by displaying a loan amount as `(int)` while retaining the original `double` value in memory.

---

## SECTION C: CONDITIONAL STATEMENTS, LOOPS AND VALIDATION

1. **Attribute Validation:**
   - IDs must be positive (`> 0`) and unique across the array.
   - Mandatory names must be non-blank.
   - Email format must be valid (contains `@` and `.`).
   - Customer age must be between 18 and 100.
   - Customer and guarantor incomes must be positive (`> 0.0`).
   - Officer experience must be non-negative (`>= 0`).
   - Display clear rejection messages upon invalid inputs.

2. **Loan Eligibility Rules (`if / else-if / else`):**
   - Customer age must be at least 21.
   - Customer and guarantor monthly incomes must both be positive.
   - Requested amount must be `> 0`, within product maximum, and at most `12 × customer monthly income`.
   - Guarantor income must be at least `30% of customer monthly income`.
   - Product interest rate must be `> 0` and `<= 30%`.
   - Repayment period must be between 1 and 120 months.
   - Customer cannot act as their own guarantor (`customer.getCustomerId() != guarantor.getGuarantorId()`).

3. **Loop Structures:**
   - Use `for` loops to search arrays and reject duplicate IDs, duplicate branch codes, and a second `PENDING` application for the same customer and loan product.
   - Use a `while` loop to repeat the interactive menu until the user selects Exit.
   - Use a `switch-case` to handle menu options; invalid choices must display an error and return to the menu.

---

## SECTION D: LOAN APPLICATIONS, DECISIONS, REPAYMENTS AND EXCEPTIONS

1. **Application Registration:**
   - Register a branch, officer, customer, product, and guarantor first.
   - Submit a loan application referencing valid registered objects.
   - Set initial application status to `PENDING` in a parallel status array in `Main`.

2. **Review and Decisions:**
   - Allow an officer to review a `PENDING` application (view details without altering status).
   - Allow an officer to `APPROVE` or `REJECT` a `PENDING` application.
   - Only `PENDING` applications may change status; only eligible applications may be approved.

3. **Repayment Tracking:**
   - Record partial repayments **only** for `APPROVED` applications.
   - Calculate total repayable using simple interest, subtract successful repayments, and display the balance.
   - Reject non-positive amounts, overpayments (paying more than the outstanding balance), or payments on fully settled loans.

4. **Exception Handling (`try-catch`):**
   - Use `try-catch` to handle non-numeric inputs (e.g. `InputMismatchException` / `NumberFormatException`) for IDs, ages, income, loan amounts, and repayments without crashing.
   - Catch `IllegalArgumentException` from class setters.
   - Display a helpful message and allow retry or return safely to the menu.

5. **Loan Summary:**
   - Provide a method to display a comprehensive loan summary showing:
     - Customer Name
     - Product Name
     - Application Status
     - Total Repayable Amount
     - Total Repaid Amount
     - Outstanding Balance

---

## SECTION E: INTERACTIVE MENU & LIVE DEMONSTRATION

### Menu Options

| Option | Action |
|:---:|---|
| **1** | Register Bank Branch |
| **2** | Register Customer |
| **3** | Register Loan Officer |
| **4** | Register Loan Product |
| **5** | Register Guarantor |
| **6** | Submit Loan Application |
| **7** | Review Loan Application |
| **8** | Approve / Reject Loan Application |
| **9** | Record Loan Repayment |
| **10** | View Loan Summary / Records |
| **0** | Exit |

### Demonstration Checklist

1. Compile and run the Java program cleanly with no warnings or crashes.
2. Demonstrate registration of Branch, Officer, Customer, Product, and Guarantor.
3. Submit an application, approve it, and record at least one successful repayment.
4. Demonstrate validation rejection for:
   - Duplicate ID
   - Ineligible application (e.g. amount > 12× income or guarantor income < 30%)
   - Invalid numeric entry (letters entered for an integer/double)
   - Overpayment on a loan
5. Display updated loan status and outstanding balance in the summary view.
