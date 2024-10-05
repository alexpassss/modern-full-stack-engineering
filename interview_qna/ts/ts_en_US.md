### **TypeScript Interview Questions**

---

### **1. Basic TypeScript Concepts**

**Q1. What is TypeScript, and how does it differ from JavaScript?**

- **Answer:**
  - **TypeScript** is a **superset of JavaScript** that adds **static typing** and other features, such as **interfaces**, **type annotations**, **generics**, and **enums**, to the language. TypeScript code is compiled into plain JavaScript, which can run in any environment that supports JavaScript.
  - **Key differences**:
    - **Static typing**: TypeScript allows developers to define types for variables, function parameters, and return values. This leads to better tooling, easier debugging, and fewer runtime errors.
    - **Compilation step**: TypeScript needs to be compiled (using the TypeScript compiler, `tsc`) into JavaScript before it can be executed by the browser or Node.js.
    - **ES6+ features**: TypeScript provides features like classes, modules, and async/await, often ahead of JavaScript versions.
    - **Type inference**: TypeScript can automatically infer types, reducing the need for explicit annotations.

---

**Q2. What are the benefits of using TypeScript in large-scale projects?**

- **Answer:**
  1. **Type Safety**: TypeScript enforces static typing, which helps catch type-related errors during development instead of at runtime.
  2. **Better Tooling**: TypeScript's type system enhances IDE support, such as autocompletion, navigation, and refactoring tools, leading to more productive development.
  3. **Code Readability and Maintainability**: Explicit types make the code easier to understand, reducing ambiguity and helping new developers onboard quickly.
  4. **Refactoring Confidence**: TypeScript enables safer refactoring because incorrect types or broken code paths are flagged by the compiler.
  5. **Modularity**: TypeScript's type system allows developers to define complex types and interfaces, promoting better modularity and code structure.
  6. **Interoperability with JavaScript**: Since TypeScript is a superset of JavaScript, developers can incrementally adopt TypeScript in existing JavaScript codebases.

---

**Q3. How do you compile TypeScript code, and what are some key `tsconfig.json` options?**

- **Answer:**

  - **Compiling TypeScript**: The TypeScript compiler (`tsc`) is used to compile `.ts` files into `.js` files. For example, to compile a file, you can run:
    ```bash
    tsc index.ts
    ```
  - **`tsconfig.json`**: This is the configuration file used to define TypeScript compiler options and the project's file structure. Key options include:
    - **`target`**: Specifies the ECMAScript version for the compiled JavaScript (e.g., `es5`, `es6`).
    - **`module`**: Defines the module system (`commonjs`, `esnext`, etc.).
    - **`strict`**: Enables all strict type-checking options (e.g., `strictNullChecks`, `strictFunctionTypes`).
    - **`outDir`**: Specifies the output directory for compiled JavaScript files.
    - **`baseUrl`** and **`paths`**: Configure module resolution and path aliases.
    - **`lib`**: Allows specifying which built-in libraries to include (e.g., `DOM`, `ES2020`).

  **Example `tsconfig.json`**:

  ```json
  {
    "compilerOptions": {
      "target": "es6",
      "module": "commonjs",
      "strict": true,
      "outDir": "./dist",
      "baseUrl": "./src",
      "paths": {
        "@models/*": ["models/*"]
      }
    },
    "include": ["src/**/*.ts"],
    "exclude": ["node_modules", "dist"]
  }
  ```

---

### **2. Types, Interfaces, and Generics**

**Q4. What is the difference between `interface` and `type` in TypeScript? When should you use one over the other?**

- **Answer:**

  - **Interface**:
    - Defines the shape of an object, which can include properties and methods.
    - **Extendable**: Interfaces can be extended, allowing for composition of types.
    - **Declaration merging**: Multiple declarations of the same interface will be merged.
    ```typescript
    interface User {
      name: string;
      age: number;
    }
    ```
  - **Type alias** (`type`):

    - Can represent any type, including **primitives**, **unions**, **tuples**, and **intersection types**.
    - **Not extendable** like interfaces, but can still compose types using union (`|`) or intersection (`&`).

    ```typescript
    type User = {
      name: string;
      age: number;
    };

    type Status = "active" | "inactive"; // Type alias for union type
    ```

  **When to use `interface` vs `type`**:

  - Use **`interface`** when defining object shapes, especially when you need to **extend** or **merge** them.
  - Use **`type`** when defining more complex types, such as **unions**, **intersections**, or **primitive types**.

---

**Q5. How do generics work in TypeScript, and why are they useful? Provide an example.**

- **Answer:** **Generics** in TypeScript allow you to write functions, classes, or interfaces that can work with **multiple types** while retaining type safety. Generics are especially useful for **reusability** and **type flexibility** without losing the advantages of static typing.

  **Example of generic function**:

  ```typescript
  function identity<T>(value: T): T {
    return value;
  }

  const num = identity<number>(42); // num: number
  const str = identity<string>("hello"); // str: string
  ```

  **Benefits of generics**:

  - **Type safety**: Generics ensure that the types passed into the function or class are retained and enforced throughout.
  - **Reusability**: A single function or class can handle multiple types without having to rewrite the logic for each type.
  - **Flexibility**: They work well with more complex data structures (e.g., collections, arrays).

  **Example of generic interface**:

  ```typescript
  interface KeyValuePair<K, V> {
    key: K;
    value: V;
  }

  const pair: KeyValuePair<string, number> = { key: "age", value: 25 };
  ```

---

**Q6. How would you use `keyof` and `in` to create types that map over an object’s properties dynamically?**

- **Answer:**

  - **`keyof`**: Creates a union type of the keys of an object type. It is useful for **type-safe property access**.

    ```typescript
    interface Person {
      name: string;
      age: number;
    }

    type PersonKeys = keyof Person; // "name" | "age"
    ```

  - **`in`**: Used in mapped types to iterate over the keys of an object, allowing dynamic creation of new types.

    ```typescript
    type ReadOnly<T> = {
      readonly [K in keyof T]: T[K];
    };

    const person: ReadOnly<Person> = { name: "John", age: 30 };
    person.name = "Alice"; // Error: Cannot assign to 'name' because it is a read-only property.
    ```

  **Example using both `keyof` and `in`**:

  ```typescript
  type Partial<T> = {
    [K in keyof T]?: T[K];
  };

  const partialPerson: Partial<Person> = { name: "John" }; // `age` is optional
  ```

  **Use case**: These utilities help in **creating flexible and reusable types**, such as `Partial`, `Readonly`, or `Pick`, without duplicating code.

---

### **3. Advanced Typing Features**

**Q7. What are mapped types in TypeScript, and when would you use them?**

- **Answer:** **Mapped types** allow you to create new types by transforming each property of an existing type. This is done by **mapping over the keys** of a type using `in` and applying transformations (like making properties optional, readonly, etc.).

  **Example** of creating a mapped type:

  ```typescript
  type Optional<T> = {
    [K in keyof T]?: T[K];
  };

  interface User {
    id: number;
    name: string;
    email: string;
  }

  const partialUser: Optional<User> = { name: "Alice" }; // `id` and `email` are optional
  ```

  **Common use cases**:

  - **Partial types** (`Partial<T>`) where all properties of `T` are optional.
  - **Readonly types** (`Readonly<T>`) where all properties of `T` are read-only.
  - **Pick/Exclude types**

to extract or exclude certain properties from an object type.

---

**Q8. How does TypeScript's `never` type work, and when would you use it?**

- **Answer:** The **`never` type** represents values that **never occur**. It is used for functions that **never return** (such as functions that throw exceptions or run forever), and it can also be used in **exhaustiveness checking**.

  **Examples**:

  - **Functions that never return**:

    ```typescript
    function throwError(message: string): never {
      throw new Error(message);
    }
    ```

  - **Exhaustiveness checks**:

    ```typescript
    type Animal = "dog" | "cat";

    function handleAnimal(animal: Animal) {
      switch (animal) {
        case "dog":
          return "Dog barks";
        case "cat":
          return "Cat meows";
        default:
          const exhaustiveCheck: never = animal; // `animal` must be `never`
          throw new Error("Unhandled animal type");
      }
    }
    ```

  **Use case**: The `never` type is used in **type-safe error handling** and **ensuring that all cases in a union are handled** exhaustively.

---

**Q9. Explain conditional types in TypeScript.**

- **Answer:** **Conditional types** are a powerful feature in TypeScript that allow you to define types based on a condition. The syntax is similar to JavaScript's ternary operator (`condition ? trueType : falseType`), but it works with types.

  **Syntax**:

  ```typescript
  T extends U ? X : Y
  ```

  **Example**:

  ```typescript
  type IsString<T> = T extends string ? "yes" : "no";

  type Test1 = IsString<string>; // "yes"
  type Test2 = IsString<number>; // "no"
  ```

  **Use case**: Conditional types are useful for building **utility types** and **type transformations**, such as making types nullable, extracting properties from unions, or creating dynamic types based on input.

  **Example with conditional type utility**:

  ```typescript
  type Nullable<T> = T extends null | undefined ? never : T;

  type NotNullString = Nullable<string | null>; // string
  ```

---

### **4. TypeScript and JavaScript Interoperability**

**Q10. How does TypeScript handle interoperability with plain JavaScript libraries?**

- **Answer:** TypeScript is designed to interoperate seamlessly with JavaScript, allowing you to use JavaScript libraries, even when they lack type definitions.

  - **Type Declaration Files**: To add types to a JavaScript library, TypeScript uses **declaration files** (`.d.ts`). These provide type information without modifying the JavaScript code.

    - For most popular libraries, type declarations are available in **DefinitelyTyped** and can be installed via npm:
      ```bash
      npm install @types/lodash
      ```

  - **`any` type**: If no type definitions are available, you can use the **`any` type**, which disables type checking for the given value.

    ```typescript
    const someLibrary: any = require("some-library");
    ```

  - **`@ts-ignore`**: Suppresses TypeScript errors on the next line. Use this sparingly and as a last resort:
    ```typescript
    // @ts-ignore
    someFunctionFromUnTypedLibrary();
    ```

  **Use case**: TypeScript provides gradual typing adoption, allowing you to incrementally add types to existing JavaScript codebases or libraries that don’t have native TypeScript support.

---

### **5. Error Handling and Debugging**

**Q11. How does TypeScript help with error handling? What are the advantages of using `unknown` over `any` for error types?**

- **Answer:** TypeScript helps with **error handling** by ensuring type safety, even when dealing with error objects. While JavaScript traditionally uses `any` for errors, TypeScript introduces the **`unknown`** type, which is safer than `any`.

  - **`any`**: Using `any` disables all type checking, making it easy to overlook issues.
  - **`unknown`**: A more type-safe alternative to `any`. You cannot interact with an `unknown` value without first **narrowing** its type.

  **Example**:

  ```typescript
  function handleError(error: unknown) {
    if (error instanceof Error) {
      console.log(error.message);
    } else {
      console.log("Unknown error");
    }
  }
  ```

  **Advantages** of `unknown` over `any`:

  - Encourages **type narrowing** before performing operations, leading to more robust error handling.
  - Prevents unexpected behaviors caused by unchecked types, which can lead to runtime errors.

---

### **6. Performance, Optimization, and Tooling**

**Q12. How would you optimize the TypeScript compiler's performance in large-scale projects?**

- **Answer:** Optimizing TypeScript compiler performance is crucial for large-scale projects to avoid long build times. Some strategies include:

  1. **Use Incremental Compilation**: Enable incremental compilation in `tsconfig.json` to avoid recompiling unchanged files.

     ```json
     {
       "compilerOptions": {
         "incremental": true
       }
     }
     ```

  2. **Enable `skipLibCheck`**: Skipping type checks on declaration files (`.d.ts`) can significantly reduce build time.

     ```json
     {
       "compilerOptions": {
         "skipLibCheck": true
       }
     }
     ```

  3. **Use Project References**: Break the project into smaller modules using **project references**. This allows TypeScript to compile only the modified modules, improving build times.

     ```json
     {
       "references": [{ "path": "./module1" }, { "path": "./module2" }]
     }
     ```

  4. **Exclude Unnecessary Files**: Exclude tests, build directories, and unnecessary files from the compilation process using the `exclude` option in `tsconfig.json`.

     ```json
     {
       "exclude": ["node_modules", "dist", "tests"]
     }
     ```

  5. **Parallel Builds**: Use **build tools** like **Webpack** or **esbuild** that support parallel builds, reducing the overall time for bundling TypeScript.

---

### **7. TypeScript in Large-Scale Projects**

**Q13. How would you structure a large-scale TypeScript project for scalability and maintainability?**

- **Answer:** Structuring a large-scale TypeScript project involves organizing the codebase to ensure modularity, maintainability, and scalability. Best practices include:

  1. **Modularization**: Break the project into smaller, **feature-based modules**. Each module should have its own directory containing services, components, and tests.

     - Example structure:
       ```
       /src
       ├── /auth
       │   ├── auth.controller.ts
       │   └── auth.service.ts
       ├── /users
       │   ├── users.controller.ts
       │   └── users.service.ts
       ```

  2. **Use TypeScript Project References**: For large projects, break the project into **multiple TypeScript projects** using **project references**. This allows for better incremental builds.

     ```json
     {
       "references": [{ "path": "./moduleA" }, { "path": "./moduleB" }]
     }
     ```

  3. **Create a Shared Module for Types**: Place common types and interfaces in a shared directory to be reused across different modules. This reduces duplication and makes refactoring easier.

     ```typescript
     // src/types/user.types.ts
     export interface User {
       id: number;
       name: string;
     }
     ```

  4. **Use Path Aliases**: Configure **path aliases** in `tsconfig.json` to avoid long relative imports.

     ```json
     {
       "compilerOptions": {
         "baseUrl": "src",
         "paths": {
           "@auth/*": ["auth/*"],
           "@users/*": ["users/*"]
         }
       }
     }
     ```

  5. **Implement Strict Typing**: Ensure `strict` mode is enabled in `tsconfig.json` for maximum type safety and maintainability. This helps catch potential issues early in development.

  6. **Automated Testing and Linting**: Set up **automated unit tests** (e.g., with **Jest**) and **linting tools** (e.g., **ESLint**) to ensure code quality and consistency across modules.

---

### **8. Leadership and Best Practices**

**Q14. How do you ensure consistency and best practices across a team working on a TypeScript project?**

- **Answer:**

  - **Code Standards and Style Guides**: Establish a **TypeScript style guide** (e.g., based on **Airbnb** or **Google** TypeScript standards) to ensure a consistent coding style across the team. Use **ESLint** with TypeScript plugins for static code analysis.

    ```bash
    npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
    ```

  - **Enforce Strict Types**: Enable strict type-checking in `tsconfig.json` by setting `"strict": true`. This ensures that all team members adhere to best practices like handling `null` and `undefined` explicitly.
    ```json
    {
      "compilerOptions": {
        "
    ```

strict": true
}
}
```

- **Code Reviews**: Implement mandatory **code reviews** using GitHub pull requests. During reviews, focus on adherence to type safety, code readability, and reusability.

- **Automated Testing**: Ensure all code changes are tested by setting up a CI/CD pipeline that runs **unit tests** (e.g., **Jest**) and **type checks** before merging into the main branch.

- **Documentation**: Encourage the use of **JSDoc** or **TypeScript’s built-in documentation** features to document complex functions, types, and modules. This improves knowledge sharing and onboarding.

- **Refactoring and Continuous Improvement**: Encourage the team to regularly refactor code and ensure it adheres to TypeScript best practices, like avoiding the `any` type and leveraging more specific types and interfaces.
