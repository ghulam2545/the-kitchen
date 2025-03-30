# Open-Closed Principle

* **Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.** OR
* **You should be able to extend a class's behavior without modifying it.**

todo

<details>

<summary>Click to expand code</summary>

```java
// ************************** BAD CODE ************************** //
class CardIssuer {
    public void issueCard(String cardType) {
        if (cardType.equals("CREDIT")) {
            System.out.println("Issuing Credit Card.");
        } else if (cardType.equals("DEBIT")) {
            System.out.println("Issuing Debit Card.");
        } else if (cardType.equals("GIFT")) {
            System.out.println("Issuing Gift Card.");
        } // Adding new card types requires modifying this class.
        else {
            System.out.println("Unknown card type.");
        }
    }
}

public class App {
    public static void main(String[] args) {
        CardIssuer issuer = new CardIssuer();
        issuer.issueCard("CREDIT");
        issuer.issueCard("DEBIT");
        issuer.issueCard("GIFT");
        issuer.issueCard("PREPAID"); // This requires modifying CardIssuer
    }
}
```

</details>

todo

<details>

<summary>Click to expand code</summary>

```java
// ************************** GOOD CODE ************************** //
// Interface for Card Issuance
interface Card {
    void issue();
}

// Credit Card Implementation
class CreditCard implements Card {
    @Override
    public void issue() {
        System.out.println("Issuing Credit Card.");
    }
}

// Debit Card Implementation
class DebitCard implements Card {
    @Override
    public void issue() {
        System.out.println("Issuing Debit Card.");
    }
}

// Gift Card Implementation
class GiftCard implements Card {
    @Override
    public void issue() {
        System.out.println("Issuing Gift Card.");
    }
}

// Prepaid Card Implementation
class PrepaidCard implements Card {
    @Override
    public void issue() {
        System.out.println("Issuing Prepaid Card.");
    }
}

// Card Issuer Class - Now Open for Extension
class CardIssuer {
    public void issueCard(Card card) {
        card.issue();
    }
}

public class App {
    public static void main(String[] args) {
        CardIssuer issuer = new CardIssuer();

        issuer.issueCard(new CreditCard());
        issuer.issueCard(new DebitCard());
        issuer.issueCard(new GiftCard());
        issuer.issueCard(new PrepaidCard());
    }
}
```

</details>

समय देने के लिए आपका धन्यवाद। 🙃
