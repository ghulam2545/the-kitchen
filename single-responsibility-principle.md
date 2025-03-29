# Single Responsibility Principle

* **A class should have only one responsibility, or reason to change.**

_This principle states that a class should have only and only one responsibility to work. It cannot do multiple things in the same class. As below, I have considered a banking system service that is trying to process multiple tasks in the same class, and it violates SRP. This class is doing too many things, which makes it harder to maintain._

<details>

<summary>Click to expand code</summary>

```java
// ** BAD CODE ** //
public class App {}
```

</details>

_As the principle states that there should be only one responsibility, so now we can separate each task in a separate class, and good code will look like this. Now each class has a single responsibility, and adding new features won’t break existing code._

<details>

<summary>Click to expand code</summary>

```java
// ** GOOD CODE ** //
public class App {}
```

</details>

समय देने के लिए आपका धन्यवाद। 🙃
