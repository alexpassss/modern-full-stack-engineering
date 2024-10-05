### **JavaScript Interview Questions**

---

### **1. Basic JavaScript Syntax and Core Concepts**

**Q1. What are the different data types in JavaScript?**

- **Answer:** JavaScript has **7 primitive data types** and **1 non-primitive type**:
  - **Primitive types**:
    - **Number**: Represents numeric values (both integers and floating-point numbers). Example: `let age = 25;`.
    - **String**: Represents textual data. Example: `let name = "John";`.
    - **Boolean**: Represents logical values: `true` or `false`. Example: `let isActive = true;`.
    - **Null**: Represents intentional absence of any value. Example: `let user = null;`.
    - **Undefined**: Represents uninitialized variables. Example: `let x; console.log(x); // undefined`.
    - **Symbol**: A unique and immutable data type often used as keys for object properties. Example: `let sym = Symbol('desc');`.
    - **BigInt**: Used to represent integers larger than `Number.MAX_SAFE_INTEGER`. Example: `let bigNum = BigInt(12345678901234567890);`.
  - **Non-primitive type**:
    - **Object**: Used to store collections of data and more complex entities. Example:
      ```javascript
      let user = {
        name: "John",
        age: 30,
      };
      ```

---

**Q2. Explain the difference between `var`, `let`, and `const` in JavaScript.**

- **Answer:**

  - **`var`**:
    - Declares a variable that is either globally scoped or function-scoped.
    - **Hoisted** to the top of its scope (initialized with `undefined`).
    - Can be re-declared and updated.
    ```javascript
    var x = 10;
    var x = 20; // Re-declaration allowed
    ```
  - **`let`**:
    - Introduced in ES6 (ES2015).
    - Block-scoped, meaning it’s confined to the block, statement, or expression where it is defined.
    - Cannot be re-declared in the same scope but can be updated.
    ```javascript
    let x = 10;
    x = 20; // Allowed
    let x = 30; // Error: re-declaration
    ```
  - **`const`**:

    - Block-scoped.
    - Cannot be re-declared or updated after it has been initialized.
    - It does not make objects immutable—**only the reference** to the object is immutable.

    ```javascript
    const y = 50;
    y = 100; // Error: Cannot re-assign

    const obj = { name: "John" };
    obj.name = "Jane"; // Allowed: Object properties can be modified.
    ```

  **Key difference**: `var` is function-scoped and prone to hoisting issues, while `let` and `const` are block-scoped and do not have the same hoisting behavior.

---

**Q3. What is the `this` keyword in JavaScript, and how does its behavior differ in various contexts?**

- **Answer:**

  - The **`this` keyword** refers to the object it belongs to, but its value depends on the **context**:
    1. **In global context** or in a simple function call, `this` refers to the **global object** (`window` in browsers, `global` in Node.js).
    ```javascript
    console.log(this); // window (in browser)
    ```
    2. **Inside a method** of an object, `this` refers to the **object** the method belongs to.
    ```javascript
    const user = {
      name: "Alice",
      greet() {
        console.log(this.name); // 'Alice'
      },
    };
    user.greet();
    ```
    3. **In an event handler**, `this` refers to the **DOM element** that fired the event.
    4. **With arrow functions**, `this` retains the value from its **lexical scope** (where the arrow function was defined), not where it’s called. Arrow functions do not have their own `this`.

  **Key point**: `this` behaves differently depending on whether the function is regular or an arrow function, and based on where and how the function is called.

---

### **2. Functions and Closures**

**Q4. What is a closure in JavaScript, and how does it work?**

- **Answer:** A **closure** is a feature in JavaScript where an inner function has access to variables in its **outer function’s scope**, even after the outer function has returned.

  **Example**:

  ```javascript
  function outer() {
    let counter = 0; // Outer function variable
    return function inner() {
      counter++; // Inner function accesses outer function's variable
      console.log(counter);
    };
  }

  const count = outer(); // count is a closure
  count(); // 1
  count(); // 2
  ```

  **How it works**: Even though `outer()` finishes executing, the inner function (`inner()`) still has access to `counter` because of the closure. The function retains the reference to its outer lexical environment.

  **Use cases**: Closures are often used to create **private variables**, maintain state across function calls, and in functional programming patterns.

---

**Q5. Explain the difference between function declarations, function expressions, and arrow functions.**

- **Answer:**

  - **Function Declarations**:
    - Functions declared using the `function` keyword. They are **hoisted**, meaning they can be invoked before they are defined in the code.
    ```javascript
    function greet() {
      return "Hello";
    }
    ```
  - **Function Expressions**:
    - Functions assigned to a variable. These are **not hoisted**, meaning they can only be invoked after the definition.
    ```javascript
    const greet = function () {
      return "Hello";
    };
    ```
  - **Arrow Functions**:
    - Introduced in ES6, these are a concise way to write function expressions. They do not have their own `this` and are useful in situations where `this` should retain its lexical scope.
    ```javascript
    const greet = () => "Hello";
    ```

  **Key differences**:

  - **Syntax**: Arrow functions are more concise.
  - **`this` context**: Arrow functions do not bind their own `this`.
  - **Hoisting**: Function declarations are hoisted, but function expressions (including arrow functions) are not.

---

### **3. Object-Oriented Programming (OOP) in JavaScript**

**Q6. What is prototypal inheritance in JavaScript? How does it differ from classical inheritance?**

- **Answer:**
  **Prototypal inheritance** is the mechanism by which **JavaScript objects inherit properties and methods from another object**. Every object has an internal property called `[[Prototype]]` (accessible via `__proto__`), which points to another object. When trying to access a property or method, the JavaScript engine will search for it in the current object, and if not found, it will look up the prototype chain.

  **Example**:

  ```javascript
  const animal = {
    eat() {
      console.log("Eating");
    },
  };

  const dog = Object.create(animal); // dog inherits from animal
  dog.bark = function () {
    console.log("Barking");
  };

  dog.eat(); // Inherited from animal
  dog.bark(); // Defined in dog
  ```

  **Difference from classical inheritance**:

  - **Classical inheritance** (like in Java or C++) creates a **copy** of the parent class' methods in the child class.
  - **Prototypal inheritance** in JavaScript links objects directly to other objects without creating copies. It’s more flexible, allowing dynamic object composition at runtime.

  **ES6 Classes**: While ES6 introduced the `class` syntax, it’s syntactic sugar over prototypal inheritance. Under the hood, JavaScript still uses prototypes.

---

**Q7. Explain how the `class` syntax works in ES6. How is it different from function constructors?**

- **Answer:** The `class` syntax in ES6 provides a cleaner, more readable way to define constructor functions and prototype methods. However, **JavaScript classes are just syntactic sugar over prototypal inheritance**.

  **Example of a class**:

  ```javascript
  class Animal {
    constructor(name) {
      this.name = name;
    }

    speak() {
      console.log(`${this.name} makes a sound.`);
    }
  }

  const dog = new Animal("Dog");
  dog.speak(); // Dog makes a sound.
  ```

  **Differences from function constructors**:

  - **Syntax**: `class` syntax is more readable and formal.
  - **Hoisting**: Unlike function constructors, classes are **not hoisted**. You cannot use a class before it is declared.
  - **`class` methods are non-enumerable**: Methods defined in the `

class` body are non-enumerable, while methods added to a constructor's prototype are enumerable.

**Class Inheritance**:

- ES6 classes support inheritance via the `extends` keyword.
  ```javascript
  class Dog extends Animal {
    bark() {
      console.log(`${this.name} barks.`);
    }
  }
  ```

---

### **4. Asynchronous JavaScript**

**Q8. What is the difference between `setTimeout` and `setInterval`?**

- **Answer:**

  - **`setTimeout`**: Executes a function once after a specified delay (in milliseconds).
    ```javascript
    setTimeout(() => {
      console.log("Executed after 2 seconds");
    }, 2000);
    ```
  - **`setInterval`**: Executes a function repeatedly at a specified interval (in milliseconds) until it is cleared.

    ```javascript
    const intervalId = setInterval(() => {
      console.log("Executed every 2 seconds");
    }, 2000);

    // To stop the interval
    clearInterval(intervalId);
    ```

  **Use cases**:

  - Use `setTimeout` for **delayed one-time execution**.
  - Use `setInterval` for **repeated tasks** like polling data at regular intervals.

---

**Q9. What is the event loop in JavaScript? How does it work with the call stack and the callback queue?**

- **Answer:** The **event loop** is a mechanism that allows JavaScript to perform non-blocking operations, even though JavaScript is single-threaded. It works by managing the **call stack**, **callback queue**, and **microtask queue**.

  **How it works**:

  1. **Call stack**: The place where the JavaScript engine keeps track of function calls. Functions are pushed to the stack when invoked and popped off when they return a result.
  2. **Callback queue**: Functions waiting to be executed after an asynchronous operation (e.g., `setTimeout`) are placed in the callback queue.
  3. **Microtask queue**: Promises and `async`/`await` operations are pushed to the microtask queue, which has higher priority than the callback queue.
  4. **Event loop**: Constantly checks the call stack. If the call stack is empty, it moves callbacks from the callback or microtask queue into the call stack for execution.

  **Example**:

  ```javascript
  console.log("Start");

  setTimeout(() => {
    console.log("Timeout callback");
  }, 0);

  Promise.resolve().then(() => {
    console.log("Promise resolved");
  });

  console.log("End");
  ```

  **Output**:

  ```
  Start
  End
  Promise resolved
  Timeout callback
  ```

  The promise resolves before the `setTimeout` callback because **microtasks** (like promises) have higher priority than macrotasks (like `setTimeout`).

---

**Q10. What is the difference between callbacks, promises, and async/await?**

- **Answer:**

  - **Callbacks**: Functions passed as arguments to other functions, to be called once an operation is completed. This often leads to **callback hell** when handling multiple asynchronous operations.

    ```javascript
    function fetchData(callback) {
      setTimeout(() => {
        callback("Data fetched");
      }, 1000);
    }

    fetchData((result) => {
      console.log(result); // Data fetched
    });
    ```

  - **Promises**: A better way to handle asynchronous operations. A promise represents a value that may be available now, in the future, or never. Promises have three states: **pending**, **resolved**, or **rejected**.

    ```javascript
    const fetchData = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve("Data fetched");
      }, 1000);
    });

    fetchData
      .then((result) => console.log(result))
      .catch((error) => console.log(error));
    ```

  - **Async/Await**: Introduced in ES2017, `async`/`await` is syntactic sugar over promises. It allows writing asynchronous code in a more synchronous manner.

    ```javascript
    async function fetchData() {
      try {
        let result = await new Promise((resolve, reject) => {
          setTimeout(() => resolve("Data fetched"), 1000);
        });
        console.log(result);
      } catch (error) {
        console.log(error);
      }
    }

    fetchData();
    ```

  **Differences**:

  - **Callbacks** lead to **pyramid of doom** (callback hell) when chaining multiple asynchronous operations.
  - **Promises** flatten the code structure but can still get complicated with multiple `.then()` chains.
  - **Async/Await** offers cleaner syntax and better error handling via `try/catch` blocks.

---

### **5. Modern JavaScript (ES6+) Features**

**Q11. What are JavaScript modules, and how do you export and import them?**

- **Answer:** **JavaScript modules** allow you to break code into smaller, reusable pieces. Modules help in organizing code, improving maintainability, and reducing global scope pollution.

  **Exporting**:

  - **Named exports**: Allows multiple exports per module.

    ```javascript
    // module.js
    export const name = "Alice";
    export function greet() {
      console.log("Hello, Alice");
    }
    ```

  - **Default export**: A single export per module. The default export does not require curly braces.
    ```javascript
    // module.js
    export default function greet() {
      console.log("Hello");
    }
    ```

  **Importing**:

  - **Named import**:

    ```javascript
    import { name, greet } from "./module.js";
    greet(); // Hello, Alice
    ```

  - **Default import**:
    ```javascript
    import greet from "./module.js";
    greet(); // Hello
    ```

  **Benefits of modules**:

  - Scope isolation (variables/functions declared in modules do not pollute the global scope).
  - Code reusability.
  - Dependency management.

---

**Q12. What are template literals in JavaScript? How do they differ from regular strings?**

- **Answer:** **Template literals** (introduced in ES6) are a more powerful way to work with strings. They allow for:

  - **Multiline strings**: Strings can span multiple lines without the need for concatenation.
  - **String interpolation**: Variables and expressions can be embedded directly within the string using `${}`.
  - **Tagged templates**: A feature that allows you to modify template literals with a function.

  **Example**:

  ```javascript
  const name = "Alice";
  const message = `Hello, ${name}!`; // String interpolation
  console.log(message); // Hello, Alice

  const multiline = `This is a
  multiline string.`;
  ```

  **Difference** from regular strings:

  - Regular strings require concatenation with `+` and do not support multiline strings easily.
  - Template literals simplify code and offer more flexibility for dynamic strings.

---

### **6. Error Handling and Debugging**

**Q13. How does error handling work in JavaScript? Explain `try...catch` and `finally`.**

- **Answer:** Error handling in JavaScript is done using the **`try...catch`** block, which allows you to catch and handle exceptions (errors) that occur during code execution. Additionally, `finally` can be used to execute code regardless of whether an error occurred or not.

  **Syntax**:

  ```javascript
  try {
    // Code that may throw an error
    throw new Error("Something went wrong");
  } catch (error) {
    // Handle the error
    console.log(error.message); // Something went wrong
  } finally {
    // Executes no matter what
    console.log("Cleanup code");
  }
  ```

  - **`try`**: Contains the code that might throw an exception.
  - **`catch`**: Catches the exception and handles it.
  - **`finally`**: Runs regardless of whether an exception was thrown or not. It's useful for cleanup tasks (e.g., closing a connection).

---

**Q14. What is the difference between `null` and `undefined` in JavaScript?**

- **Answer:**

  - **`undefined`**: A variable is `undefined` when it is declared but not initialized, or when a function doesn't return a value.

    ```javascript
    let x;
    console.log(x); // undefined
    ```

  - **`null`**: Explicitly represents "nothing" or "empty value". It's often used to deliberately assign a variable with no value.
    ```javascript
    let y = null;
    console.log(y); // null
    ```

  **Difference**:

  - `undefined` means the variable has been declared but has no value yet.
  - `null` is an intentional absence of value.

---

### **7. Performance Optimization and Best Practices**

**Q15. What is the difference between `==` and `===` in JavaScript?**

- **Answer:**
  - **`==` (Abstract Equality)**: Performs type coercion, meaning it converts values of different types to the same type before comparison.
    ```javascript
    console.log(1 == "1"); // true
    ```
  - **`===` (Strict Equality)**: Does not perform type coercion. It only returns `true` if both the type and value are the same.
    ```javascript
    console.log(1 === "1"); // false
    ```

**Recommendation**: Always use `===` to avoid unexpected results due to type coercion.

---

**Q16. What is debouncing and throttling in JavaScript?**

- **Answer:**

  - **Debouncing**: Limits the rate at which a function is called. It ensures the function is executed only after a specified delay after the last call. It’s often used in scenarios like window resizing or text input.

    ```javascript
    function debounce(func, delay) {
      let timeoutId;
      return function (...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
          func.apply(this, args);
        }, delay);
      };
    }
    ```

  - **Throttling**: Ensures a function is called at most once in a specified period. It’s useful for actions like scroll or resize events.
    ```javascript
    function throttle(func, limit) {
      let inThrottle;
      return function (...args) {
        if (!inThrottle) {
          func.apply(this, args);
          inThrottle = true;
          setTimeout(() => (inThrottle = false), limit);
        }
      };
    }
    ```

  **Use cases**:

  - **Debouncing**: Used when you want to delay execution until the action is finished (e.g., search input).
  - **Throttling**: Used when you want to limit the number of executions per time unit (e.g., scroll events).

---

### **8. Testing and Code Quality**

**Q17. How would you test JavaScript code? What tools and frameworks do you use?**

- **Answer:**

  - **Unit Testing**: Focuses on testing individual functions or modules in isolation.

    - **Tools**: **Jest**, **Mocha**, **Jasmine** are popular testing frameworks for JavaScript.
    - **Example** (Jest):

      ```javascript
      function add(a, b) {
        return a + b;
      }

      test("adds 1 + 2 to equal 3", () => {
        expect(add(1, 2)).toBe(3);
      });
      ```

  - **Integration Testing**: Tests how different parts of the application work together.

    - **Tools**: **Cypress**, **Puppeteer**, **TestCafe** for browser-based testing.

  - **End-to-End (E2E) Testing**: Tests the entire flow of an application from the user’s perspective.
    - **Tools**: **Cypress**, **Selenium**.

  **Best practices**:

  - Use **Test-Driven Development (TDD)** when possible.
  - Aim for high **test coverage** but ensure quality over quantity.
  - Use **mocks** and **spies** to isolate dependencies during testing.

---

### **9. Leadership and Best Practices**

**Q18. How do you handle JavaScript code reviews and ensure best practices in a team?**

- **Answer:** In a team environment, code reviews are crucial for maintaining code quality and fostering knowledge sharing. Here’s how I handle JavaScript code reviews:

  1. **Establish clear guidelines**: Create a shared **JavaScript style guide** (e.g., using **ESLint** with a common configuration) to ensure consistency in code formatting and style.
  2. **Automate code quality checks**: Use tools like **ESLint** and **Prettier** for automatic linting and formatting checks. Integrate these into the **CI/CD pipeline** to ensure quality before merging.
  3. **Review functionality, not just syntax**: Focus on the **logic, performance, and security** aspects of the code, not just whether it conforms to style rules.
  4. **Encourage feedback**: Use code reviews as an opportunity to encourage open dialogue and **collaborative learning**. It’s important to make the process constructive and educational, especially for junior developers.
  5. **Refactor when necessary**: Encourage the team to refactor code when necessary, instead of just adding new features on top of existing code. This reduces technical debt and improves maintainability.

---

**Q19. How do you ensure that JavaScript code is scalable and maintainable in large projects?**

- **Answer:** To ensure that JavaScript code is scalable and maintainable in large projects, follow these principles:

  1. **Modularize code**: Break down functionality into **smaller, reusable modules**. Use ES6 **modules** or frameworks like **Webpack** or **Rollup** to manage dependencies.
  2. **Follow SOLID principles**: Apply **object-oriented design principles** like Single Responsibility, Open/Closed, and Dependency Injection where appropriate.
  3. **Use TypeScript or Flow**: Use **TypeScript** or **Flow** for static type checking, which helps catch type-related bugs early and makes the code more predictable and self-documenting.
  4. **Document the code**: Maintain **clear documentation** for complex functions, modules, or components. Use tools like **JSDoc** to document code for team members and future developers.
  5. **Automate testing**: Set up **unit, integration, and E2E tests** using tools like **Jest**, **Cypress**, and **Selenium**. Ensure that tests are run automatically in CI/CD pipelines.
  6. **Adopt a component-based architecture**: If using front-end libraries like **React**, adopt a **component-driven** approach, where UI components are reusable, testable, and maintainable.
