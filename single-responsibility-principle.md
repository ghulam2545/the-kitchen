# Single Responsibility Principle

* **A class should have only one responsibility, or reason to change.**

_This principle states that a class should have only and only one responsibility to work. It cannot do multiple things in the same class. As below, I have considered a banking system service that is trying to process multiple tasks in the same class, and it violates SRP. This class is doing too many things, which makes it harder to maintain._

<details>

<summary>Click to expand code</summary>

```java
// ************************** BAD CODE ************************** //
class CoreBankingService {
    private String accountNumber;
    private double creditScore;
    private double loanAmount;
    private double balance;
    private String reportType;
    private String email;
    private String phoneNumber;

    public CoreBankingService(String accountNumber, double creditScore, double loanAmount, double balance, String reportType, String email, String phoneNumber) {
        this.accountNumber = accountNumber;
        this.creditScore = creditScore;
        this.loanAmount = loanAmount;
        this.balance = balance;
        this.reportType = reportType;
        this.email = email;
        this.phoneNumber = phoneNumber;
    }

    public boolean issueLoan() {
        if (creditScore >= 700 && loanAmount <= 100000) {
            System.out.println("Loan of $" + loanAmount + " approved for " + accountNumber);
            // Loan issuance logic here
            return true;
        } else {
            System.out.println("Loan of $" + loanAmount + " denied for " + accountNumber + ". Credit score or amount too high.");
            return false;
        }
    }

    public void generateReport() {
        if ("monthly".equalsIgnoreCase(reportType)) {
            System.out.println("Generating monthly report for " + accountNumber + ". Balance: $" + balance);
            // Monthly report logic here
        } else if ("annual".equalsIgnoreCase(reportType)) {
            System.out.println("Generating annual report for " + accountNumber + ". Balance: $" + balance);
            // Annual report logic here
        } else {
            System.out.println("Invalid report type for " + accountNumber);
        }
    }

    public void sendNotification(String message) {
        System.out.println("Sending notification to " + accountNumber + ": " + message);
        // Notification sending logic here
        if (email != null && !email.isEmpty()) {
            System.out.println("Sending email to " + email + ": " + message);
        }
        if (phoneNumber != null && !phoneNumber.isEmpty()) {
            System.out.println("Sending SMS to " + phoneNumber + ": " + message);
        }
    }
}

public class App {
    public static void main(String[] args) {
        String accountNumber = "3020034109034";
        double creditScore = 750;
        double loanAmount = 50000;
        double balance = 10000;
        String reportType = "monthly";
        String email = "user@example.com";
        String phoneNumber = "123-456-7890";

        CoreBankingService bankingService = new CoreBankingService(accountNumber, creditScore, loanAmount, balance, reportType, email, phoneNumber);

        boolean loanApproved = bankingService.issueLoan();
        bankingService.generateReport();
        if(loanApproved){
            bankingService.sendNotification("Your loan has been approved!");
        } else {
            bankingService.sendNotification("Your loan application was denied.");
        }
    }
}
```

</details>

_As the principle states that there should be only one responsibility, so now we can separate each task in a separate class, and good code will look like this. Now each class has a single responsibility, and adding new features won’t break existing code._

<details>

<summary>Click to expand code</summary>

```java
// ************************** GOOD CODE ************************** //

// Loan Service
class LoanService {
    private String accountNumber;
    private double creditScore;
    private double loanAmount;

    public LoanService(String accountNumber, double creditScore, double loanAmount) {
        this.accountNumber = accountNumber;
        this.creditScore = creditScore;
        this.loanAmount = loanAmount;
    }

    public boolean issueLoan() {
        if (creditScore >= 700 && loanAmount <= 100000) {
            System.out.println("Loan of $" + loanAmount + " approved for " + accountNumber);
            // Loan issuance logic here
            return true;
        } else {
            System.out.println("Loan of $" + loanAmount + " denied for " + accountNumber + ". Credit score or amount too high.");
            return false;
        }
    }
}

// Report Service
class ReportService {
    private String accountNumber;
    private double balance;
    private String reportType;

    public ReportService(String accountNumber, double balance, String reportType) {
        this.accountNumber = accountNumber;
        this.balance = balance;
        this.reportType = reportType;
    }

    public void generateReport() {
        if ("monthly".equalsIgnoreCase(reportType)) {
            System.out.println("Generating monthly report for " + accountNumber + ". Balance: $" + balance);
            // Monthly report logic here
        } else if ("annual".equalsIgnoreCase(reportType)) {
            System.out.println("Generating annual report for " + accountNumber + ". Balance: $" + balance);
            // Annual report logic here
        } else {
            System.out.println("Invalid report type for " + accountNumber);
        }
    }
}

// Notification Service
class NotificationService {
    private String accountNumber;
    private String email;
    private String phoneNumber;

    public NotificationService(String accountNumber, String email, String phoneNumber) {
        this.accountNumber = accountNumber;
        this.email = email;
        this.phoneNumber = phoneNumber;
    }

    public void sendNotification(String message) {
        System.out.println("Sending notification to " + accountNumber + ": " + message);
        // Notification sending logic here
        if (email != null && !email.isEmpty()) {
            System.out.println("Sending email to " + email + ": " + message);
        }
        if (phoneNumber != null && !phoneNumber.isEmpty()) {
            System.out.println("Sending SMS to " + phoneNumber + ": " + message);
        }
    }
}

public class App {
    public static void main(String[] args) {
        String accountNumber = "3020034109034";
        double creditScore = 750;
        double loanAmount = 50000;
        double balance = 10000;
        String reportType = "monthly";
        String email = "user@example.com";
        String phoneNumber = "123-456-7890";

        LoanService loanService = new LoanService(accountNumber, creditScore, loanAmount);
        ReportService reportService = new ReportService(accountNumber, balance, reportType);
        NotificationService notificationService = new NotificationService(accountNumber, email, phoneNumber);

        boolean loanApproved = loanService.issueLoan();
        reportService.generateReport();
        if(loanApproved){
            notificationService.sendNotification("Your loan has been approved!");
        } else {
            notificationService.sendNotification("Your loan application was denied.");
        }
    }
}
```

</details>

समय देने के लिए आपका धन्यवाद। 🙃
