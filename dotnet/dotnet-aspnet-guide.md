# .NET và ASP.NET Core trong Phát triển Backend

## Giới thiệu

### Tư duy Phát triển Backend
- **Separation of Concerns**: Tách biệt logic, data, presentation.
- **RESTful APIs**: Endpoints không trạng thái, dựa trên tài nguyên.
- **Error Handling**: Quản lý lỗi tập trung.
- **Security First**: Validate input, xác thực người dùng.
- **Performance**: Caching, optimization, monitoring.
- **Scalability**: Mở rộng ngang/dọc, microservices.

### Tổng quan .NET
.NET là framework đa nền tảng của Microsoft, cho phép xây dựng backend scalable. ASP.NET Core là framework web phổ biến nhất cho .NET, giúp tạo APIs nhanh chóng.

**Tại sao .NET cho Backend?**
- **Strongly Typed**: Type safety, IntelliSense.
- **Cross-platform**: Chạy trên Windows, Linux, macOS.
- **High Performance**: Compiled to native code.
- **Enterprise Ready**: Mạnh mẽ cho large-scale apps.
- **NuGet ecosystem**: Hàng triệu packages.

## Phần 1: C# Cơ bản

### Lý thuyết C#
- **CLR & JIT**: Common Language Runtime, Just-In-Time compilation.
- **LINQ**: Language Integrated Query.
- **Async/Await**: Asynchronous programming.
- **Generics**: Type-safe collections.
- **Delegates & Events**: Function pointers, event-driven.
- **Reflection**: Runtime type inspection.

#### Best Practices C#
- Sử dụng async/await cho I/O operations.
- Implement IDisposable cho resource management.
- Sử dụng generics thay vì object.
- Exception handling với try/catch/finally.
- Naming conventions: PascalCase cho types, camelCase cho variables.

### Bài tập C# Cơ bản (1-10)
1. Tạo console app in "Hello World" với Console.WriteLine.
2. Đọc file text async và in nội dung.
3. Tạo HTTP server trả về "Hello .NET".
4. Sử dụng StreamReader để read file lớn.
5. Start process để chạy command.
6. Tạo class export method tính tổng array.
7. Sử dụng Path.Combine để join paths.
8. Handle exceptions trong async method.
9. Tạo timer với Timer class.
10. Deserialize JSON từ file và log properties.

## Phần 2: ASP.NET Core Framework

### Lý thuyết ASP.NET Core
- **Middleware**: app.Use(), next().
- **Routing**: MapGet(), MapPost(), etc.
- **Dependency Injection**: Built-in DI container.
- **Configuration**: appsettings.json, environment variables.
- **Logging**: ILogger interface.
- **CORS, Security**: CORS, authentication middleware.

#### Best Practices ASP.NET Core
- Structure app với Controllers, Services, Repositories.
- Validate input với Data Annotations/FluentValidation.
- Sử dụng middleware cho logging, auth.
- Xử lý exceptions với Exception Filters.
- Rate limiting cho security.
- Áp dụng SOLID patterns.

### Bài tập ASP.NET Core Cơ bản (1-10)
1. **Tạo ASP.NET Core app cơ bản**: Khởi tạo Web API project, tạo endpoint GET `/api/health` trả về JSON `{"status": "OK", "timestamp": DateTime.UtcNow}`. Test với Postman.
2. **Model Binding**: Tạo endpoint POST `/api/users` nhận JSON body `{Name, Email}`, validate required fields, trả về user object với Id tự động.
3. **Custom logging middleware**: Tạo middleware ghi log request (method, URL, timestamp, response time) cho mọi request. Sử dụng ILogger.
4. **Route parameters**: Tạo routes `/api/users/{id}` (GET, PUT, DELETE). Validate id là int, handle trường hợp user không tồn tại (404).
5. **Query parameters & pagination**: Tạo route GET `/api/users` hỗ trợ query `?page=1&limit=10&search=name`. Implement pagination và search cơ bản.
6. **Static file serving**: Setup static file serving cho thư mục `wwwroot/`, tạo endpoint `/api/uploads` để upload file, serve files đã upload.
7. **Exception handling**: Tạo global exception handler catch tất cả exceptions, format response `{success: false, error: message, code: statusCode}`.
8. **CORS & security**: Setup CORS cho specific origins, authentication middleware, rate limiting.
9. **Authentication middleware**: Implement JWT auth, tạo middleware `Authorize`, protect routes `/api/admin/*`.
10. **Input validation**: Sử dụng Data Annotations để validate input (email format, password strength), trả về detailed error messages.

## Phần 3: OOP trong .NET

### Lý thuyết OOP
- **Classes & Objects**: Constructor, methods, properties.
- **Inheritance**: : base(), override.
- **Encapsulation**: Private fields, properties.
- **Polymorphism**: Virtual/override methods.
- **Abstraction**: Abstract classes, interfaces.

#### Best Practices OOP
- Áp dụng SOLID principles.
- Sử dụng interfaces cho contracts.
- Implement dependency injection.
- Tạo reusable classes.
- Thiết kế cho extensibility.

### Bài tập OOP Cơ bản (1-10)
1. **Class Fundamentals**: Tạo `User` class với constructor, properties (Id, Name, Email, CreatedAt), methods (ToJson(), UpdateProfile()). Implement encapsulation.
2. **Inheritance Hierarchy**: Tạo base `Animal` class, inherit `Dog` và `Cat` classes. Override `Speak()` method, add specific methods.
3. **Encapsulation & Validation**: Implement properties với validation (email format, password strength), private methods.
4. **Polymorphism**: Tạo `Shape` abstract class với abstract `Area()` và `Perimeter()` methods. Implement `Rectangle` và `Circle` classes.
5. **Abstract Classes & Interfaces**: Define `IDatabaseConnection` interface, abstract `BaseRepository` class, implement `UserRepository` và `ProductRepository`.
6. **Factory Pattern**: Implement `PaymentFactory` tạo payment processors (Stripe, PayPal), `NotificationFactory` cho email/SMS.
7. **Singleton Pattern**: Create `DatabaseConnection` singleton, `Logger` singleton, `CacheManager` singleton.
8. **Strategy Pattern**: Implement `ISortingStrategy` interface với `PriceSort`, `NameSort`, `DateSort` strategies.
9. **Observer Pattern**: Create `OrderSubject` với observers cho `EmailNotifier`, `InventoryUpdater`.
10. **SOLID Implementation**: Refactor code để apply SOLID principles.

## Phần 4: Thiết kế Source Code Backend

### Lý thuyết Architecture
- **MVC Pattern**: Models, Views, Controllers.
- **Layered Architecture**: Presentation, Business, Data.
- **Repository Pattern**: Abstract data access.
- **Dependency Injection**: Built-in DI.
- **SOLID Principles**: Single responsibility, etc.
- **Design Patterns**: Factory, Singleton, Strategy.

#### Best Practices Code Structure
- **Folder Structure**:
  ```
  Controllers/
  Models/
  Services/
  Repositories/
  Middleware/
  DTOs/
  Utils/
  ```
- **Naming Conventions**: PascalCase cho everything.
- **Exception Classes**: Custom exception types.
- **Logging**: Serilog với structured logs.
- **Testing**: xUnit, NUnit.

### Bài tập Thiết kế Source (1-10)
1. **MVC Structure**: Tạo folder structure MVC với `Controllers/UserController.cs`, `Models/User.cs`, routing. Implement CRUD.
2. **Service Layer**: Tạo `Services/UserService.cs` chứa business logic, inject vào controller.
3. **Repository Pattern**: Tạo `Repositories/IUserRepository.cs` interface, `UserRepository.cs` implementation.
4. **Custom Exception Classes**: Tạo `Exceptions/` với `ValidationException.cs`, `NotFoundException.cs`.
5. **Middleware Architecture**: Tạo middleware cho auth, validation, error handling, logging.
6. **Configuration Management**: Tạo `appsettings.json` cho different environments.
7. **Logging System**: Setup Serilog với multiple sinks (console, file), structured logging.
8. **Unit Testing**: Setup xUnit, viết tests cho UserService (mock repository), UserController.
9. **Integration Testing**: Setup test server, test full request/response cycle.
10. **SOLID Principles**: Refactor code để apply SOLID.

## Phần 5: Database Integration

### Lý thuyết Database
- **EF Core**: ORM cho .NET.
- **SQL vs NoSQL**: Khi nào dùng gì.
- **Migrations**: Schema versioning.
- **Transactions**: ACID properties.
- **Indexing**: Performance optimization.

#### Best Practices Database
- **Connection Management**: Connection strings.
- **Error Handling**: Database-specific errors.
- **Query Optimization**: Include, ThenInclude.
- **Data Validation**: Fluent API.
- **Backup & Recovery**: SQL Server tools.

### Bài tập Database (1-10)
1. **SQL Server Setup**: Cài SQL Server, tạo database `ecommerce_dev`, setup EF Core.
2. **User Model & Associations**: Tạo User model với EF, associations với Order, Address.
3. **CRUD Operations**: Implement full CRUD với EF, error handling, validation.
4. **Database Migrations**: Tạo migrations cho tables, add columns, seed data.
5. **Transaction Management**: Implement order creation với transaction.
6. **MongoDB Integration**: Setup MongoDB.Driver, tạo Product collection.
7. **Data Validation**: Server-side validation với FluentValidation.
8. **Query Optimization**: Eager loading, indexes, optimize queries.
9. **Database Backup**: Scripts cho backup SQL Server.
10. **Database Monitoring**: Connection monitoring, slow query logging.

## Phần 6: Áp dụng Tư duy Backend

### Lý thuyết Backend Thinking
- **API Design**: REST, versioning, documentation.
- **Database Design**: Normalization, relationships.
- **Security**: Authentication, authorization, encryption.
- **Performance**: Indexing, caching, optimization.
- **Monitoring**: Logs, metrics, alerts.
- **Deployment**: Containerization, orchestration.
- **OOP in Backend**: Domain models, services, repositories.

#### Best Practices Tư duy Full-stack
- **User-Centric**: Nghĩ từ góc nhìn người dùng.
- **Scalable Design**: Lập kế hoạch cho sự phát triển.
- **Maintainable Code**: Code sạch, có tài liệu.
- **Secure by Default**: Defense in depth.
- **Testable Code**: Dễ dàng test.
- **Observable Systems**: Logs, metrics.

### Bài tập Tư duy Backend (1-10)
1. **API Design & Documentation**: Design REST API, use Swashbuckle cho Swagger.
2. **JWT Authentication**: Implement JWT với access/refresh tokens.
3. **Role-Based Authorization**: Setup RBAC với policies.
4. **Database Relationships**: Design normalized schema.
5. **Redis Caching**: Setup Redis cho sessions, caching.
6. **File Upload System**: Implement với IFormFile, cloud storage.
7. **Email Service**: Setup với MailKit, templates.
8. **Real-time Notifications**: SignalR cho WebSockets.
9. **Docker Containerization**: Dockerfile cho .NET app, docker-compose.
10. **Cloud Deployment**: Deploy to Azure với CI/CD.

## Phần 7: Advanced C# Features

### Lý thuyết Advanced C#
- **LINQ**: Query syntax, method syntax.
- **Async Streams**: IAsyncEnumerable.
- **Records**: Immutable data types.
- **Pattern Matching**: Switch expressions.
- **Source Generators**: Compile-time code generation.

#### Advanced Best Practices
- Sử dụng LINQ cho data manipulation.
- Implement async streams cho large data.
- Use records cho DTOs.
- Pattern matching cho clean code.
- Source generators cho performance.

### Bài tập Advanced C# (1-15)
1. **LINQ Setup**: Use LINQ cho collections, join operations.
2. **Async Streams**: Implement IAsyncEnumerable cho streaming data.
3. **Records**: Create immutable DTOs với records.
4. **Pattern Matching**: Use switch expressions, property patterns.
5. **Source Generators**: Create simple source generator.
6. **Generic Constraints**: Advanced generics với constraints.
7. **Reflection**: Runtime type inspection, dynamic invocation.
8. **Expression Trees**: Build dynamic queries.
9. **Memory Management**: Span<T>, Memory<T> cho performance.
10. **Concurrent Programming**: ConcurrentDictionary, Parallel LINQ.
11. **Functional Programming**: Func, Action delegates, immutability.
12. **Metaprogramming**: Attributes, custom attributes.
13. **Code Analysis**: Roslyn analyzers.
14. **Benchmarking**: BenchmarkDotNet cho performance testing.
15. **Production Optimization**: AOT compilation, trimming.

## Phần 8: Dự án E-commerce Hoàn chỉnh

### Lý thuyết Phát triển Dự án
- **Planning**: Requirements, user stories, architecture design.
- **Development**: Agile/Scrum, iterative development, code reviews, Git flow.
- **Testing**: Unit, integration, E2E, performance, security testing.
- **Deployment**: CI/CD, Docker, Kubernetes, cloud platforms.
- **Maintenance**: Monitoring, logging, optimization, security updates.
- **E-commerce Specific**: Payment processing, inventory, order fulfillment, compliance.

### Bài tập Dự án E-commerce (1-20)

#### Phase 1: Project Setup & Core Features (1-5)
1. **Project Initialization**: Setup ASP.NET Core Web API, cấu hình Serilog, setup testing (xUnit), create folder structure.
2. **Database Design**: Design SQL Server schema, create migrations, setup MongoDB cho reviews.
3. **User Authentication**: Implement JWT auth, registration/login, password reset, email verification, roles.
4. **Product Management**: CRUD cho products, variants, search & filtering.
5. **Category System**: Hierarchical categories, CRUD, relationships.

#### Phase 2: Shopping Features (6-10)
6. **Shopping Cart**: Add to cart, update quantities, persistence, validation.
7. **Order Management**: Order creation, status tracking, history.
8. **Payment Integration**: Stripe/PayPal integration, webhooks.
9. **Inventory Management**: Stock tracking, alerts, updates.
10. **Shipping System**: Rates calculation, methods, tracking.

#### Phase 3: Advanced Features (11-15)
11. **Review & Rating System**: Reviews với ratings, moderation.
12. **Wishlist & Favorites**: User wishlists, notifications.
13. **Search & Filtering**: Full-text search, advanced filtering.
14. **Promotions & Discounts**: Coupons, discounts, scheduling.
15. **Email Notifications**: Order confirmations, templates.

#### Phase 4: Performance & Security (16-20)
16. **Caching Strategy**: Redis caching, invalidation.
17. **Security Implementation**: Validation, rate limiting, CORS.
18. **File Upload System**: Image upload, optimization, S3.
19. **Real-time Features**: SignalR cho updates, chat.
20. **Deployment & Monitoring**: Docker, CI/CD, monitoring.

#### Yêu cầu Kỹ thuật:
- **Architecture**: Clean Architecture
- **Code Quality**: 80%+ coverage, analyzers
- **Performance**: < 200ms response, 1000+ users
- **Security**: OWASP compliance
- **Scalability**: Indexing, optimization
- **Documentation**: Swagger, code docs

#### Tính năng Bonus:
- Multi-language support
- Mobile API optimization
- Admin dashboard
- Analytics
- Social login
- Recommendations

## Tài liệu tham khảo
- [.NET Docs](https://learn.microsoft.com/dotnet/)
- [ASP.NET Core Guide](https://learn.microsoft.com/aspnet/core/)
- [.NET Best Practices](https://learn.microsoft.com/dotnet/standard/best-practices)
- [Clean Code](https://www.oreilly.com/library/view/clean-code/9780136083238/)