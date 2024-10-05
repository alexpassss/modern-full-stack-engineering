### NestJS Interview Questions

---

**Q1. What is NestJS, and what are its key features?**

- **Answer**:
  NestJS is a progressive Node.js framework for building efficient and scalable server-side applications using TypeScript. It leverages the power of modern JavaScript and provides a rich set of features, including:
  - **Modular Architecture**: Encourages the development of modular applications with features grouped into modules.
  - **Dependency Injection**: Provides a built-in dependency injection system for better organization and testing.
  - **Asynchronous Programming**: Supports asynchronous programming with Promises and Observables.
  - **Middleware Support**: Allows the integration of middleware for handling requests and responses.
  - **GraphQL and REST Support**: Provides easy setup and integration for both RESTful and GraphQL APIs.
  - **Extensive Testing Utilities**: Built-in support for unit and end-to-end testing.

---

**Q2. Explain the modular architecture of NestJS. How does it benefit application development?**

- **Answer**:
  NestJS uses a modular architecture, where the application is divided into modules that encapsulate related functionality. Each module can contain controllers, providers, and services.

  **Benefits**:

  - **Separation of Concerns**: Modules help to separate different functionalities of the application, improving maintainability and readability.
  - **Reusability**: Modules can be reused across different parts of the application or even in different applications.
  - **Encapsulation**: Each module can expose only the necessary components, keeping implementation details hidden.
  - **Scalability**: Makes it easier to scale the application by adding new modules without affecting existing functionality.

---

**Q3. What are controllers in NestJS, and what is their purpose?**

- **Answer**:
  Controllers in NestJS are responsible for handling incoming requests and returning responses to the client. They define routes for the application and delegate the processing of requests to the appropriate services.

  **Purpose**:

  - **Routing**: Controllers map HTTP requests to specific handler methods using decorators like `@Get()`, `@Post()`, etc.
  - **Request Handling**: Process requests, validate input, and return responses.
  - **Delegation**: Invoke services to perform business logic or data manipulation, separating concerns between the controller and the underlying logic.

  Example:

  ```typescript
  import { Controller, Get } from "@nestjs/common";

  @Controller("users")
  export class UsersController {
    @Get()
    findAll() {
      // Logic to retrieve users
    }
  }
  ```

---

**Q4. Explain the role of services in NestJS. How do they differ from controllers?**

- **Answer**:
  Services in NestJS are classes that contain business logic and data access functionality. They are typically annotated with the `@Injectable()` decorator, allowing them to be injected into controllers or other services.

  **Differences from Controllers**:

  - **Purpose**: Controllers are focused on handling HTTP requests and responses, while services contain the business logic and interact with data sources.
  - **Reusability**: Services can be reused across multiple controllers, promoting code reuse and separation of concerns.

  Example:

  ```typescript
  import { Injectable } from "@nestjs/common";

  @Injectable()
  export class UsersService {
    findAll() {
      // Logic to retrieve users from database
    }
  }
  ```

---

**Q5. What is dependency injection in NestJS, and how does it work?**

- **Answer**:
  Dependency injection (DI) is a design pattern used to create and manage dependencies in an application. In NestJS, DI is handled through the use of providers, which can be services, repositories, or any class that can be instantiated.

  **How it Works**:

  - **Providers**: Any class decorated with `@Injectable()` can be registered as a provider and can be injected into other classes (controllers or services).
  - **Constructor Injection**: Dependencies are typically injected through the constructor of a class, allowing NestJS to resolve and provide the required instances.

  Example:

  ```typescript
  import { Controller, Get } from "@nestjs/common";
  import { UsersService } from "./users.service";

  @Controller("users")
  export class UsersController {
    constructor(private readonly usersService: UsersService) {}

    @Get()
    findAll() {
      return this.usersService.findAll();
    }
  }
  ```

---

**Q6. How does NestJS support asynchronous programming?**

- **Answer**:
  NestJS supports asynchronous programming through the use of Promises and async/await syntax, allowing developers to write non-blocking code for handling requests and responses.

  - **Async Functions**: Methods in controllers or services can be defined as `async`, enabling the use of the `await` keyword for asynchronous operations.
  - **Observables**: NestJS also integrates with RxJS, allowing developers to use Observables for managing asynchronous data streams.

  Example of an async function in a service:

  ```typescript
  @Injectable()
  export class UsersService {
    async findAll(): Promise<User[]> {
      return await this.userRepository.find();
    }
  }
  ```

---

**Q7. Explain how middleware works in NestJS.**

- **Answer**:
  Middleware in NestJS is a function that is executed during the request-response cycle. It can perform tasks such as logging, authentication, validation, or modifying the request/response objects.

  **How it Works**:

  - Middleware functions can be defined using the `@Middleware()` decorator or implemented as a class that implements the `NestMiddleware` interface.
  - Middleware can be applied globally or to specific routes.

  Example of a simple logging middleware:

  ```typescript
  import { Injectable, NestMiddleware } from "@nestjs/common";

  @Injectable()
  export class LoggerMiddleware implements NestMiddleware {
    use(req: Request, res: Response, next: Function) {
      console.log(`Request...`);
      next();
    }
  }
  ```

---

**Q8. How do you handle validation in NestJS?**

- **Answer**:
  Validation in NestJS can be handled using the `class-validator` library in conjunction with DTOs (Data Transfer Objects). By defining validation rules in DTOs, you can ensure that incoming data meets the required criteria.

  **Steps to Implement**:

  1. Create a DTO class and define validation decorators from the `class-validator` library.
  2. Use the `ValidationPipe` to automatically validate incoming requests based on the defined rules.

  Example:

  ```typescript
  import { IsString, IsInt } from 'class-validator';

  export class CreateUserDto {
      @IsString()
      readonly name: string;

      @IsInt()
      readonly age: number;
  }

  @Post()
  async create(@Body(new ValidationPipe()) createUserDto: CreateUserDto) {
      // Create user logic
  }
  ```

---

**Q9. What are the advantages of using GraphQL with NestJS?**

- **Answer**:
  Integrating GraphQL with NestJS offers several advantages:
  - **Type Safety**: NestJS uses TypeScript, enabling type-safe GraphQL schemas and resolvers.
  - **Modularity**: NestJS’s modular architecture complements GraphQL’s type system, making it easier to structure applications.
  - **Flexible Queries**: GraphQL allows clients to request exactly the data they need, reducing over-fetching and under-fetching issues.
  - **Built-in Support**: NestJS provides decorators and modules for easy integration with GraphQL, simplifying the setup process.

---

**Q10. How do you implement error handling in NestJS?**

- **Answer**:
  Error handling in NestJS can be implemented using built-in exception filters or custom filters to manage errors globally or at the controller level.

  - **Built-in Exception Filters**: NestJS provides a set of standard exception classes (e.g., `HttpException`, `NotFoundException`) that can be used to handle common errors.
  - **Custom Exception Filters**: Create custom filters by implementing the `ExceptionFilter` interface to handle specific errors and return formatted responses.

  Example of a custom exception filter:

  ```typescript
  import {
    ExceptionFilter,
    Catch,
    ArgumentsHost,
    HttpException,
  } from "@nestjs/common";
  import { Response } from "express";

  @Catch(HttpException)
  export class HttpExceptionFilter implements ExceptionFilter {
    catch(exception: HttpException, host: ArgumentsHost) {
      const ctx = host.switchToHttp();
      const response = ctx.getResponse<Response>();
      const status = exception.getStatus();
      const message = exception.getResponse();

      response.status(status).json({
        statusCode: status,
        timestamp: new Date().toISOString(),
        message,
      });
    }
  }
  ```

---

**Q11. What is the use of decorators in NestJS?**

- **Answer**:
  Decorators in NestJS are special annotations used to add metadata to classes, methods, or properties. They play a crucial role in defining various elements of the application, such as:
  - **Controllers**: `@Controller()` decorator marks a class as a controller.
  - **Routes**: HTTP method decorators like `@Get()`, `@Post()`, etc., define route handlers for specific HTTP requests.
  - **Providers**: `@Injectable()` decorator marks a class as a provider that can be injected into other classes.
  - **Pipes**:

`@Pipe()` decorator indicates that a class is a custom pipe for transforming or validating input.

---

**Q12. Explain the purpose of `@Inject()` and how dependency injection works in NestJS.**

- **Answer**:
  The `@Inject()` decorator is used to specify which provider to inject into a class, especially when using tokens or when the type is not sufficient for resolving the dependency.

  **How Dependency Injection Works**:

  - **Provider Registration**: Classes annotated with `@Injectable()` are registered as providers in a module.
  - **Constructor Injection**: Dependencies are typically injected through the constructor, allowing NestJS to resolve the appropriate instances when creating a class.

  Example of using `@Inject()`:

  ```typescript
  import { Inject, Injectable } from "@nestjs/common";

  @Injectable()
  export class UsersService {
    constructor(
      @Inject("USERS_REPOSITORY")
      private readonly usersRepository: UsersRepository
    ) {}
  }
  ```

---

**Q13. What is the purpose of Guards in NestJS?**

- **Answer**:
  Guards in NestJS are used to implement authorization logic and protect routes or controllers from unauthorized access. They can check if a request should be handled or rejected based on specific conditions.

  **How it Works**:

  - Guards are classes that implement the `CanActivate` interface and define a `canActivate` method to determine whether a request should proceed.
  - They can be applied globally, at the controller level, or on specific routes.

  Example of a simple guard:

  ```typescript
  import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";

  @Injectable()
  export class AuthGuard implements CanActivate {
    canActivate(context: ExecutionContext): boolean {
      // Logic to determine if the request is authorized
      return true; // or false
    }
  }
  ```

---

**Q14. How does NestJS support testing, and what strategies do you recommend?**

- **Answer**:
  NestJS has built-in support for testing through the use of testing utilities like `@nestjs/testing`. It allows for unit testing of components and integration testing of modules.

  **Strategies for Testing**:

  - **Unit Testing**: Use Jest (default testing framework) to write unit tests for individual components, services, and controllers.
  - **Mocking**: Utilize mocking to isolate dependencies during tests, allowing for focused testing of functionality.
  - **Integration Testing**: Test the entire module or application flow to ensure all components work together as expected.
  - **End-to-End Testing**: Use tools like Supertest or Cypress to perform end-to-end tests on the API.

  Example of a simple unit test:

  ```typescript
  import { Test, TestingModule } from "@nestjs/testing";
  import { UsersService } from "./users.service";

  describe("UsersService", () => {
    let service: UsersService;

    beforeEach(async () => {
      const module: TestingModule = await Test.createTestingModule({
        providers: [UsersService],
      }).compile();

      service = module.get<UsersService>(UsersService);
    });

    it("should be defined", () => {
      expect(service).toBeDefined();
    });
  });
  ```

---

**Q15. What are the best practices for structuring a NestJS application?**

- **Answer**:
  Best practices for structuring a NestJS application include:
  - **Modular Organization**: Organize the application into modules based on features or functionality to promote separation of concerns.
  - **Naming Conventions**: Use clear and consistent naming conventions for files and classes to enhance readability and maintainability.
  - **Centralized Configuration**: Use configuration modules to manage environment-specific settings and configurations centrally.
  - **Middleware and Guards**: Implement middleware and guards for cross-cutting concerns like logging and authentication.
  - **Consistent Error Handling**: Use custom exception filters for consistent error handling and logging throughout the application.

---

**Q16. How do you manage configurations in a NestJS application?**

- **Answer**:
  Configuration management in NestJS can be done using the `@nestjs/config` package, which provides a straightforward way to handle environment-specific settings.

  **Steps**:

  1. Install the package: `npm install @nestjs/config`.
  2. Create a `.env` file to store environment variables.
  3. Import the `ConfigModule` in the root module and load the environment variables.
  4. Use the `ConfigService` to access configuration values in services, controllers, and other parts of the application.

  Example:

  ```typescript
  import { Module } from "@nestjs/common";
  import { ConfigModule } from "@nestjs/config";

  @Module({
    imports: [ConfigModule.forRoot()],
  })
  export class AppModule {}
  ```

---

**Q17. What is the role of pipes in NestJS?**

- **Answer**:
  Pipes in NestJS are used for data transformation and validation. They can be applied to route handlers to modify input data before it reaches the controller.

  **Roles of Pipes**:

  - **Validation**: Validate incoming data against defined rules, ensuring data integrity.
  - **Transformation**: Transform input data into a desired format or structure (e.g., converting strings to numbers).
  - **Error Handling**: Handle validation errors gracefully and provide meaningful responses.

  Example of a simple validation pipe:

  ```typescript
  import {
    PipeTransform,
    Injectable,
    ArgumentMetadata,
    BadRequestException,
  } from "@nestjs/common";

  @Injectable()
  export class ValidationPipe implements PipeTransform {
    transform(value: any, metadata: ArgumentMetadata) {
      if (!value) {
        throw new BadRequestException("Validation failed");
      }
      return value; // Return transformed value
    }
  }
  ```

---

**Q18. How do you implement logging in a NestJS application?**

- **Answer**:
  Logging in a NestJS application can be implemented using the built-in logging service, `Logger`. You can log messages at different levels (log, error, warn, debug, verbose).

  **Implementation Steps**:

  - Use the `Logger` class to log messages in services, controllers, or middleware.
  - For advanced logging, integrate third-party logging libraries like Winston or Pino.

  Example:

  ```typescript
  import { Injectable, Logger } from "@nestjs/common";

  @Injectable()
  export class UsersService {
    private readonly logger = new Logger(UsersService.name);

    findAll() {
      this.logger.log("Retrieving all users");
      // Logic to retrieve users
    }
  }
  ```

---

**Q19. What is a Custom Decorator in NestJS, and how can you create one?**

- **Answer**:
  Custom decorators in NestJS are user-defined decorators that can be used to add metadata or functionality to classes or methods. They can be helpful for creating reusable functionality across the application.

  **Creating a Custom Decorator**:

  - Define a function that uses the `createParamDecorator` or `createDecorator` utility from NestJS.
  - The function can extract and process metadata from the request context.

  Example of a custom parameter decorator:

  ```typescript
  import { createParamDecorator, ExecutionContext } from "@nestjs/common";

  export const User = createParamDecorator(
    (data: unknown, ctx: ExecutionContext) => {
      const request = ctx.switchToHttp().getRequest();
      return request.user; // Extract user information from request
    }
  );
  ```

---

**Q20. How do you perform health checks in a NestJS application?**

- **Answer**:
  Health checks can be implemented in a NestJS application using a dedicated controller or middleware to expose health status endpoints.

  **Implementation Steps**:

  - Create a health check controller that returns the status of the application.
  - Optionally, check the status of dependencies (e.g., database, external services) to provide a comprehensive health report.

  Example:

  ```typescript
  import { Controller, Get } from "@nestjs/common";

  @Controller("health")
  export class HealthController {
    @Get()
    checkHealth() {
      return { status: "healthy" };
    }
  }
  ```
