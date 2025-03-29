# Dependency Inversion Principle

* **High-level components should rely on abstractions, or interfaces, instead of low-level components.**

_This principle helps us to write loosely coupled code, and it states that we should prefer abstraction and interface instead of directly injecting dependency at a low level._

<details>

<summary>Click to expand code</summary>

```java
// ************************** BAD CODE: ************************** //

class SendSMSService {
    public void sendSMS(String phoneNumber, String message) {
        System.out.println("Sending SMS to " + phoneNumber + ": " + message);
        // Actual SMS sending logic here
    }
}

class CustomerService {
    private SendSMSService smsService;

    public CustomerService() {
        this.smsService = new SendSMSService(); // High-level module depends on low-level module
    }

    public void notifyCustomer(String phoneNumber, String message) {
        smsService.sendSMS(phoneNumber, message);
    }
}

public class App {
    public static void main(String[] args) {
        CustomerService customerService = new CustomerService();
        customerService.notifyCustomer("123-456-7890", "Your account opening process is completed!");
    }
}
```

</details>

_The below code relies on abstraction, so let's suppose if the bank decided to send notifications via emails, then it doesn't need to change the implementation logic of customer service; it just provides our new notifier._

<details>

<summary>Click to expand code</summary>

```java
/// ************************** GOOD CODE: ************************** //

// Abstraction (Interface)
interface MessageService {
    void sendMessage(String destination, String message);
}

// Low-level module implementing the abstraction
class SendSMSService implements MessageService {
    @Override
    public void sendMessage(String phoneNumber, String message) {
        System.out.println("Sending SMS to " + phoneNumber + ": " + message);
        // Actual SMS sending logic here
    }
}

// Low-level module implementing the abstraction
class SendEmailService implements MessageService {
    @Override
    public void sendMessage(String email, String message) {
        System.out.println("Sending Email to " + email + ": " + message);
        // Actual email sending logic here
    }
}

// High-level module depending on abstraction
class CustomerService {
    private MessageService messageService;

    public CustomerService(MessageService messageService) {
        this.messageService = messageService; // Dependency injection
    }

    public void notifyCustomer(String destination, String message) {
        messageService.sendMessage(destination, message);
    }
}

public class App {
    public static void main(String[] args) {
        // Using SMS Service
        MessageService smsService = new SendSMSService();
        CustomerService customerServiceSMS = new CustomerService(smsService);
        customerServiceSMS.notifyCustomer("123-456-7890", "Your account opening process is completed!");

        // Using Email Service
        MessageService emailService = new SendEmailService();
        CustomerService customerServiceEmail = new CustomerService(emailService);
        customerServiceEmail.notifyCustomer("user@example.com", "Your account opening process is completed!");
    }
}
```

</details>

समय देने के लिए आपका धन्यवाद। 🙃
