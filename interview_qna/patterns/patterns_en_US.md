### **Design Patterns Interview Questions**

---

### **1. Design Patterns Fundamentals**

**Q1. What is a design pattern, and why are design patterns important in software development?**

- **Answer**:
  A **design pattern** is a proven, reusable solution to a common problem that occurs within a specific context in software design. It is not a finished design but rather a template or guideline for solving a problem in different situations.

  **Importance of design patterns**:

  1. **Reusability**: Patterns provide solutions that have been tested and used in various scenarios, promoting code reuse and reducing the need to reinvent solutions.
  2. **Maintainability**: Patterns help to structure code in a way that makes it easier to understand, extend, and maintain.
  3. **Scalability**: Patterns provide a foundation for designing systems that can scale efficiently as requirements grow.
  4. **Communication**: They provide a common language that developers can use to discuss solutions, improving team collaboration and understanding of code.
  5. **Flexibility**: Patterns promote loose coupling and modular design, making it easier to modify or extend components without impacting the entire system.

  **Use case**: Design patterns are widely used in large-scale software systems, especially in enterprise applications where maintainability, scalability, and reusability are critical.

---

**Q2. What are the three main categories of design patterns, and can you provide an example of each?**

- **Answer**:
  Design patterns are typically classified into three main categories: **creational**, **structural**, and **behavioral**.

  **1. Creational patterns**:

  - **Purpose**: Focus on the process of object creation, providing mechanisms to create objects in a controlled, reusable, and flexible way.
  - **Example**: **Singleton Pattern**: Ensures that a class has only one instance and provides a global point of access to it.
  - **Use case**: When you need to ensure that a single instance of a class is used across the application, such as in managing database connections or configuration settings.

  **2. Structural patterns**:

  - **Purpose**: Deal with the composition of classes and objects, ensuring that larger structures are built in a flexible and efficient way.
  - **Example**: **Adapter Pattern**: Allows incompatible interfaces to work together by wrapping an existing class with a new interface.
  - **Use case**: When you need to integrate third-party libraries with different interfaces into your system.

  **3. Behavioral patterns**:

  - **Purpose**: Focus on communication between objects, promoting flexible interactions and reducing coupling.
  - **Example**: **Observer Pattern**: Allows one or more objects (observers) to be notified when the state of another object (subject) changes.
  - **Use case**: Used in event-driven systems like GUIs, where changes in one component need to be reflected in others, such as when user input updates multiple views.

  **Use case**: Understanding these categories helps in selecting the right pattern based on the problem being solved, improving code clarity, and facilitating team discussions around design choices.

---

### **2. Creational Design Patterns**

**Q3. What is the Singleton pattern, and when would you use it?**

- **Answer**:
  The **Singleton pattern** is a creational design pattern that ensures a class has only **one instance** and provides a global point of access to that instance.

  **Key characteristics**:

  - **Private constructor**: Prevents external classes from creating multiple instances.
  - **Static instance**: Holds the single instance of the class.
  - **Lazy initialization**: The instance is created only when it is first requested, ensuring resources are not used unnecessarily.
  - **Thread safety**: In multi-threaded environments, care must be taken to ensure that the Singleton is instantiated only once across all threads.

  **When to use the Singleton pattern**:

  1. **Global resource management**: When you need to control access to a global resource, such as a configuration manager, logging system, or connection pool.
  2. **Consistency**: When you want to ensure there is a single consistent instance of a class throughout the application.
  3. **Performance optimization**: When creating multiple instances of a class is expensive, but the same functionality can be provided by a single instance.

  **Code example (Java)**:

  ```java
  public class Singleton {
      private static Singleton instance;

      private Singleton() {}  // Private constructor

      public static synchronized Singleton getInstance() {
          if (instance == null) {
              instance = new Singleton();
          }
          return instance;
      }
  }
  ```

  **Use case**: The Singleton pattern is commonly used in scenarios where a single instance is needed to coordinate actions, such as logging services, configuration management, or database connection pools.

---

**Q4. What is the Factory Method pattern, and how does it differ from the Abstract Factory pattern?**

- **Answer**:
  **Factory Method pattern** and **Abstract Factory pattern** are both creational design patterns, but they differ in their scope and intent.

  **Factory Method pattern**:

  - **Purpose**: Defines an interface for creating an object but allows subclasses to alter the type of object that is created.
  - **How it works**: It delegates the responsibility of object creation to subclasses, allowing more flexibility in choosing the concrete class to instantiate.
  - **Use case**: Use Factory Method when a class cannot anticipate the exact class of objects it needs to create.

  **Example** (Java):

  ```java
  abstract class Dialog {
      abstract Button createButton();  // Factory method
  }

  class WindowsDialog extends Dialog {
      Button createButton() {
          return new WindowsButton();  // Specific button implementation
      }
  }

  class WebDialog extends Dialog {
      Button createButton() {
          return new HTMLButton();  // Specific button implementation
      }
  }
  ```

  **Abstract Factory pattern**:

  - **Purpose**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
  - **How it works**: It defines a set of related objects that belong together and ensures they are created consistently.
  - **Use case**: Use Abstract Factory when you need to create families of objects that must work together, such as creating UI elements for different platforms.

  **Example** (Java):

  ```java
  interface GUIFactory {
      Button createButton();
      Checkbox createCheckbox();
  }

  class WindowsFactory implements GUIFactory {
      public Button createButton() {
          return new WindowsButton();
      }
      public Checkbox createCheckbox() {
          return new WindowsCheckbox();
      }
  }

  class MacFactory implements GUIFactory {
      public Button createButton() {
          return new MacButton();
      }
      public Checkbox createCheckbox() {
          return new MacCheckbox();
      }
  }
  ```

  **Difference**:

  - **Factory Method**: Focuses on a single product, allowing subclasses to decide which class to instantiate.
  - **Abstract Factory**: Focuses on creating related products, often as part of a family, ensuring that the components are compatible.

  **Use case**: Use the **Factory Method** when subclasses should control the object creation, and use **Abstract Factory** when multiple related objects need to be created in a consistent way across families of products (e.g., GUI toolkits, themes).

---

### **3. Structural Design Patterns**

**Q5. What is the Adapter pattern, and when would you use it?**

- **Answer**:
  The **Adapter pattern** is a structural design pattern that allows two incompatible interfaces to work together. It acts as a bridge between two classes that otherwise could not communicate due to interface differences.

  **How it works**:

  - The Adapter wraps an existing class and provides the necessary interface that the client expects. The Adapter translates calls between the client and the wrapped object, ensuring they can communicate effectively.

  **When to use the Adapter pattern**:

  1. **Legacy code integration**: When you need to integrate legacy code or third-party libraries with a new interface without modifying the original code.
  2. **Interface incompatibility**: When two classes that have similar functionality need to work together but have incompatible interfaces.

  **Example** (Java):

  ```java
  // Target interface
  interface MediaPlayer {
      void play(String audioType, String fileName);
  }

  // Adaptee class (incompatible)
  class VLCPlayer {
      void playVLC(String fileName) {
          System.out.println("Playing VLC file: " + fileName);
      }
  }

  // Adapter class
  class MediaAdapter implements MediaPlayer {
      VLCPlayer vlcPlayer;

      MediaAdapter() {
          vlcPlayer = new VLCPlayer();
      }

      public void play(String audioType, String fileName) {
          if(audioType.equalsIgnoreCase("vlc")) {
              vlcPlayer.playVLC(fileName);
          }
      }
  }

  // Client class
  class AudioPlayer implements MediaPlayer {
      MediaAdapter mediaAdapter;

      public void play(String audioType, String fileName) {
          if (audioType.equalsIgnoreCase("vlc")) {
              mediaAdapter = new MediaAdapter();
              mediaAdapter.play(audioType, fileName);
          }
      }
  }
  ```

  **Use case**: The Adapter pattern is useful in scenarios such as integrating third-party APIs, refactoring legacy systems, or providing backward compatibility for updated interfaces.

---

**Q6. What is the difference between the Adapter pattern and the Decorator pattern?**

- **Answer**:
  Both the **Adapter** and **Decorator** patterns are structural patterns, but they serve different purposes and are used in different scenarios.

  **Adapter pattern**:

  - **Purpose**: The Adapter pattern allows two incompatible interfaces to work together by translating the interface of one class into another interface that the client expects.
  - **Use case**: Use when you need to integrate classes or systems with incompatible interfaces, such as third-party libraries or legacy code.

  **Example**: Wrapping a third-party payment gateway that has a different interface than your system to ensure compatibility without modifying the original code.

  **Decorator pattern**:

  - **Purpose**: The Decorator pattern allows behavior to be added to an object dynamically, without altering its structure. It provides a flexible alternative to subclassing by creating a set of decorator classes that are used to wrap concrete components.
  - **Use case**: Use when you need to add functionality to an object in a flexible and extensible manner, such as adding features like logging, caching, or validation without modifying the original class.

  **Example** (Java):

  ```java
      interface Coffee {
          String getDescription();
          double cost();
      }

      class SimpleCoffee implements Coffee {
          public String getDescription() {
              return "Simple coffee";
          }
          public double cost() {
              return 5.0;
          }
      }

      class MilkDecorator implements Coffee {
          private Coffee coffee;

          MilkDecorator(Coffee coffee) {
              this.coffee = coffee;
          }

          public String getDescription() {
              return coffee.getDescription() + ", with milk";
          }
          public double cost() {
              return coffee.cost() + 1.0;
          }
      }
  ```

  **Key difference**:

  - **Adapter**: Translates one interface to another.
  - **Decorator**: Adds additional behavior to objects without modifying their structure.

  **Use case**: Use the **Adapter pattern** for interface compatibility issues, and use the **Decorator pattern** when you want to add new responsibilities to objects dynamically.

---

### **4. Behavioral Design Patterns**

**Q7. What is the Observer pattern, and how does it differ from the Publisher-Subscriber pattern?**

- **Answer**:
  The **Observer pattern** is a behavioral design pattern in which an object (the **subject**) maintains a list of its dependents (the **observers**) and notifies them of state changes. It is commonly used in event-driven systems, where changes in one object need to be reflected in others.

  **How the Observer pattern works**:

  - The subject provides methods to attach, detach, and notify observers.
  - When the state of the subject changes, it automatically notifies all attached observers, often by calling a method like `update()`.

  **Example** (Java):

  ```java
  interface Observer {
      void update(String message);
  }

  class ConcreteObserver implements Observer {
      public void update(String message) {
          System.out.println("Observer received message: " + message);
      }
  }

  class Subject {
      private List<Observer> observers = new ArrayList<>();

      public void attach(Observer observer) {
          observers.add(observer);
      }

      public void notifyAllObservers(String message) {
          for (Observer observer : observers) {
              observer.update(message);
          }
      }
  }
  ```

  **Publisher-Subscriber pattern**:

  - The **Publisher-Subscriber pattern** (or **Pub-Sub**) is a messaging pattern where publishers send messages (events) to a central broker, and subscribers receive only the messages they are interested in. The publisher and subscriber do not know each other directly.

  **Key difference**:

  - **Observer pattern**: The observers are tightly coupled to the subject, and the subject directly notifies each observer.
  - **Publisher-Subscriber pattern**: There is a message broker (or event bus) between the publishers and subscribers, decoupling them completely. The broker handles delivering events to subscribers based on their subscriptions.

  **Use case**:

  - Use the **Observer pattern** when there is a clear one-to-many dependency, and objects need to be notified of changes in another object.
  - Use the **Publisher-Subscriber pattern** for large-scale systems where decoupling publishers and subscribers is critical, such as in microservices architectures, where multiple services listen for events.

---

**Q8. What is the Strategy pattern, and when should you use it?**

- **Answer**:
  The **Strategy pattern** is a behavioral design pattern that defines a family of algorithms, encapsulates each one, and allows them to be interchangeable. The client can choose which algorithm to use at runtime without changing the code that uses the algorithm.

  **How it works**:

  - The Strategy pattern separates the behavior (algorithm) from the context (the class using the algorithm), allowing the algorithm to be swapped dynamically.

  **When to use the Strategy pattern**:

  1. **When multiple algorithms exist**: Use the Strategy pattern when you have several algorithms that can be applied to a given task, and you want to select the appropriate algorithm dynamically.
  2. **When avoiding conditional logic**: If your code contains a large number of conditional statements to select different algorithms, the Strategy pattern allows you to replace these with a more flexible solution.

  **Example** (Java):

  ```java
  interface PaymentStrategy {
      void pay(int amount);
  }

  class CreditCardStrategy implements PaymentStrategy {
      public void pay(int amount) {
          System.out.println("Paid " + amount + " using credit card.");
      }
  }

  class PayPalStrategy implements PaymentStrategy {
      public void pay(int amount) {
          System.out.println("Paid " + amount + " using PayPal.");
      }
  }

  class PaymentContext {
      private PaymentStrategy strategy;

      public void setPaymentStrategy(PaymentStrategy strategy) {
          this.strategy = strategy;
      }

      public void executePayment(int amount) {
          strategy.pay(amount);
      }
  }
  ```

  **Use case**: The Strategy pattern is useful when you need to switch between different algorithms dynamically, such as selecting payment methods, sorting algorithms, or compression strategies in a system.

---

### **5. Real-World Design Patterns and Best Practices**

**Q9. How would you apply the Command pattern to implement undo/redo functionality?**

- **Answer**:
  The **Command pattern** is a behavioral design pattern in which a command is encapsulated as an object. This allows the client to parameterize, queue, and execute commands, as well as provide **undo/redo** functionality.

  **How the Command pattern works**:

  - **Command**: Encapsulates a request as an object, which includes information about the action to be performed, the method to invoke, and any associated data.
  - **Invoker**: Executes the command.
  - **Receiver**: The object that performs the actual action.
  - **Undo/Redo**: Each command object stores the state necessary to reverse its execution.

  **Steps to implement undo/redo**:

  1. Each command class must implement an `execute()` method (for performing the action) and an `undo()` method (to reverse the action).
  2. Maintain a history of commands in a stack to enable the undo and redo functionality.

  **Example** (Java):

  ```java
  interface Command {
      void execute();
      void undo();
  }

  class LightOnCommand implements Command {
      private Light light;

      LightOnCommand(Light light) {
          this.light = light;
      }

      public void execute() {
          light.on();
      }

      public void undo() {
          light.off();
      }
  }

  class Light {
      public void on() {
          System.out.println("Light is on");
      }

      public void off() {
          System.out.println("Light is off");
      }
  }

  class RemoteControl {
      private Stack<Command> commandHistory = new Stack<>();

      public void pressButton(Command command) {
          command.execute();
          commandHistory.push(command);
      }

      public void undoLastCommand() {
          if (!commandHistory.isEmpty()) {
              Command lastCommand = commandHistory.pop();
              lastCommand.undo();
          }
      }
  }
  ```

  **Use case**: The Command pattern is ideal for scenarios requiring undo/redo functionality, such as text editors, drawing applications, or transactional systems where operations need to be reversible.

---

**Q10. How would you apply the Decorator pattern in a logging system to add features like timestamps and log levels?**

- **Answer**:
  The **Decorator pattern** is used to add additional responsibilities to an object dynamically. In the context of a logging system, the Decorator pattern allows you to extend the functionality of a basic logger by adding features like timestamps, log levels, and formatting, without modifying the original logger class.

  **How to apply the Decorator pattern**:

  - The base logger provides a simple logging mechanism.
  - Each decorator adds specific functionality (e.g., timestamps, log levels) to the base logger while maintaining the same interface.

  **Example** (Java):

  ```java
  interface Logger {
      void log(String message);
  }

  class BasicLogger implements Logger {
      public void log(String message) {
          System.out.println(message);
      }
  }

  class TimestampLoggerDecorator implements Logger {
      private Logger logger;

      TimestampLoggerDecorator(Logger logger) {
          this.logger = logger;


  }

        public void log(String message) {
            String timestamp = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date());
            logger.log(timestamp + " " + message);
        }
    }

    class LogLevelDecorator implements Logger {
        private Logger logger;
        private String logLevel;

        LogLevelDecorator(Logger logger, String logLevel) {
            this.logger = logger;
            this.logLevel = logLevel;
        }

        public void log(String message) {
            logger.log("[" + logLevel + "] " + message);
        }
    }
  ```

  **Use case**: The Decorator pattern is ideal in scenarios where you want to add optional features to a core component, such as a logging system where you might need to add timestamps, log levels, or different formats dynamically, depending on the environment or user preferences.
