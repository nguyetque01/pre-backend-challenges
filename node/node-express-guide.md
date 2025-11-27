# Node.js và Express.js trong Phát triển Backend

## Giới thiệu

### Tư duy Phát triển Backend
- **Separation of Concerns**: Tách biệt logic, data, presentation.
- **RESTful APIs**: Endpoints không trạng thái, dựa trên tài nguyên.
- **Error Handling**: Quản lý lỗi tập trung.
- **Security First**: Validate input, xác thực người dùng.
- **Performance**: Caching, optimization, monitoring.
- **Scalability**: Mở rộng ngang/dọc, microservices.

### Tổng quan Node.js
Node.js là runtime JavaScript chạy trên server, cho phép xây dựng backend có thể mở rộng. Express.js là framework phổ biến nhất cho Node.js, giúp tạo APIs nhanh chóng.

**Tại sao Node.js cho Backend?**
- **JavaScript everywhere**: Một ngôn ngữ cho cả frontend và backend.
- **Non-blocking I/O**: Xử lý requests đồng thời hiệu quả.
- **NPM ecosystem**: Hàng triệu packages sẵn có.
- **Real-time apps**: WebSockets, streaming dễ dàng.

## Phần 1: JavaScript Cơ bản

### Lý thuyết JavaScript
- **Event Loop**: Single-threaded, non-blocking.
- **Modules**: CommonJS vs ES6 modules.
- **Streams**: Readable, Writable, Transform.
- **Child Processes**: Fork, spawn, exec.
- **File System**: Async operations.
- **HTTP Module**: Built-in server.

#### Best Practices JavaScript
- Sử dụng async/await thay vì callbacks.
- Xử lý lỗi đúng cách với try/catch.
- Tránh blocking operations.
- Sử dụng environment variables.
- Giám sát memory usage.

### Bài tập JavaScript Cơ bản (1-10)
1. Tạo script in "Hello World" với console.log.
2. Đọc file text async và in nội dung.
3. Tạo HTTP server trả về "Hello Node.js".
4. Sử dụng fs.createReadStream để stream file lớn.
5. Fork child process để chạy command.
6. Tạo module export function tính tổng array.
7. Sử dụng path module để join paths.
8. Handle errors trong async function.
9. Tạo timer với setTimeout/setInterval.
10. Parse JSON từ file và log properties.

## Phần 2: Express.js Framework

### Lý thuyết Express
- **Middleware**: app.use(), next().
- **Routing**: app.get(), app.post(), etc.
- **Request/Response**: req.body, res.json().
- **Static Files**: express.static().
- **Error Handling**: next(err).
- **CORS, Security**: helmet, cors packages.

#### Best Practices Express
- Structure app với routes, controllers, models.
- Validate input với Joi/express-validator.
- Sử dụng middleware cho logging, auth.
- Xử lý 404 và errors một cách graceful.
- Rate limiting cho security.
- Áp dụng OOP patterns: Controllers as classes.

### Bài tập Express Cơ bản (1-10)
1. **Tạo Express app cơ bản**: Khởi tạo Express app, tạo route GET `/api/health` trả về JSON `{"status": "OK", "timestamp": new Date().toISOString()}`. Test với Postman.
2. **Body parser middleware**: Tạo route POST `/api/users` nhận JSON body `{name, email}`, validate required fields, trả về user object với id tự động.
3. **Custom logging middleware**: Tạo middleware ghi log request (method, URL, timestamp, response time) cho mọi request. Sử dụng console.log với màu sắc.
4. **Route parameters**: Tạo routes `/api/users/:id` (GET, PUT, DELETE). Validate id là number, handle trường hợp user không tồn tại (404).
5. **Query parameters & pagination**: Tạo route GET `/api/users` hỗ trợ query `?page=1&limit=10&search=name`. Implement pagination và search cơ bản.
6. **Static file serving**: Setup static file serving cho thư mục `public/`, tạo route `/api/uploads` để upload file với multer, serve images đã upload.
7. **Error handling middleware**: Tạo global error handler catch tất cả errors, format response `{success: false, error: message, code: statusCode}`.
8. **CORS & security**: Setup CORS cho specific origins, thêm helmet security headers, rate limiting 100 requests/hour per IP.
9. **Authentication middleware**: Implement basic auth với username/password, tạo middleware `authRequired`, protect routes `/api/admin/*`.
10. **Input validation**: Sử dụng Joi để validate user input (email format, password strength, required fields), trả về detailed error messages.

## Phần 3: OOP trong Node.js

### Lý thuyết OOP
- **Classes & Objects**: Constructor, methods, properties.
- **Inheritance**: extends, super().
- **Encapsulation**: Private fields, getters/setters.
- **Polymorphism**: Method overriding.
- **Abstraction**: Abstract classes, interfaces.

#### Best Practices OOP
- Áp dụng SOLID principles với OOP.
- Sử dụng interfaces cho contract definitions.
- Implement dependency injection.
- Tạo reusable classes.
- Thiết kế cho extensibility.

### Bài tập OOP Cơ bản (1-10)
1. **Class Fundamentals**: Tạo `User` class với constructor, properties (id, name, email, createdAt), methods (toJSON(), updateProfile()). Implement encapsulation với private fields.
2. **Inheritance Hierarchy**: Tạo base `Animal` class, extend thành `Dog` và `Cat` classes. Override `speak()` method, add specific methods (`fetch()` cho Dog, `scratch()` cho Cat).
3. **Encapsulation & Validation**: Implement getters/setters cho `User` class với validation (email format, password strength), private methods cho internal logic.
4. **Polymorphism**: Tạo `Shape` abstract class với `area()` và `perimeter()` abstract methods. Implement `Rectangle` và `Circle` classes với proper polymorphism.
5. **Abstract Classes & Interfaces**: Define `DatabaseConnection` interface, create abstract `BaseRepository` class, implement concrete `UserRepository` và `ProductRepository`.
6. **Factory Pattern**: Implement `PaymentFactory` tạo different payment processors (Stripe, PayPal, BankTransfer), `NotificationFactory` cho email/SMS/push notifications.
7. **Singleton Pattern**: Create `DatabaseConnection` singleton, `Logger` singleton với multiple transports, `CacheManager` singleton với Redis connection.
8. **Strategy Pattern**: Implement `SortingStrategy` interface với `PriceSort`, `NameSort`, `DateSort` strategies. Use trong product filtering system.
9. **Observer Pattern**: Create `OrderSubject` với observers cho `EmailNotifier`, `InventoryUpdater`, `AnalyticsTracker`. Notify on order status changes.
10. **SOLID Implementation**: Refactor existing code để apply SOLID principles: Single Responsibility (mỗi class 1 concern), Open/Closed (extend via inheritance), Liskov Substitution (subtypes interchangeable), Interface Segregation (client-specific interfaces), Dependency Inversion (depend on abstractions).

## Phần 4: Thiết kế Source Code Backend

### Lý thuyết Architecture
- **MVC Pattern**: Models, Views, Controllers.
- **Layered Architecture**: Presentation, Business, Data.
- **Repository Pattern**: Abstract data access.
- **Dependency Injection**: Loose coupling.
- **SOLID Principles**: Single responsibility, Open/closed, etc.
- **OOP Patterns**: Factory, Singleton, Strategy, Observer.

#### Best Practices Code Structure
- **Folder Structure**:
  ```
  src/
    controllers/
    models/
    routes/
    middleware/
    services/
    repositories/
    utils/
    config/
  ```
- **Naming Conventions**: camelCase cho variables, PascalCase cho classes.
- **Error Classes**: Custom error types.
- **Logging**: Structured logs với levels.
- **Testing**: Unit, integration, e2e.

### Bài tập Thiết kế Source (1-10)
1. **MVC Structure**: Tạo folder structure MVC với `controllers/UserController.js`, `models/User.js`, `routes/userRoutes.js`. Implement CRUD operations theo MVC pattern.
2. **Service Layer**: Tạo `services/UserService.js` chứa business logic (validation, data processing), tách biệt từ controller. Implement dependency injection.
3. **Repository Pattern**: Tạo `repositories/UserRepository.js` abstract data access, implement in-memory storage. Add methods: `findAll()`, `findById()`, `create()`, `update()`, `delete()`.
4. **Custom Error Classes**: Tạo `errors/` folder với `ValidationError.js`, `NotFoundError.js`, `AuthenticationError.js`. Extend từ Error class với status codes.
5. **Middleware Architecture**: Tạo middleware folder với `auth.js`, `validation.js`, `errorHandler.js`, `logger.js`. Implement middleware chain cho authentication flow.
6. **Configuration Management**: Tạo `config/` folder với `database.js`, `server.js`, `environment.js`. Use environment variables cho different environments (dev, test, prod).
7. **Logging System**: Setup Winston logger với multiple transports (console, file), log levels (error, warn, info, debug), structured logging với metadata.
8. **Unit Testing**: Setup Jest, viết unit tests cho UserService (mock repository), UserController (mock service), achieve 80% code coverage.
9. **Integration Testing**: Setup Supertest cho API testing, test full request/response cycle, database integration tests với test database.
10. **SOLID Principles**: Refactor code để apply SOLID: Single Responsibility (mỗi class 1 job), Open/Closed (extend không modify), Liskov Substitution, Interface Segregation, Dependency Inversion.

## Phần 5: Database Integration

### Lý thuyết Database
- **SQL vs NoSQL**: Khi nào dùng gì.
- **ORM/ODM**: Sequelize, Mongoose, TypeORM.
- **Connection Pooling**: Efficient connections.
- **Migrations**: Schema versioning.
- **Transactions**: ACID properties.
- **Indexing**: Performance optimization.

#### Best Practices Database
- **Connection Management**: Pool configuration.
- **Error Handling**: Database-specific errors.
- **Query Optimization**: N+1 problem, eager loading.
- **Data Validation**: Schema validation.
- **Backup & Recovery**: Disaster recovery.

### Bài tập Database (1-10)
1. **PostgreSQL Setup**: Cài đặt PostgreSQL, tạo database `ecommerce_dev`, setup Sequelize với connection pooling (min: 2, max: 10, acquire: 30000).
2. **User Model & Associations**: Tạo User model với fields (id, email, password, firstName, lastName, role), associations với Order và Address models.
3. **CRUD Operations**: Implement full CRUD cho User model với proper error handling, validation (email format, password strength), soft delete.
4. **Database Migrations**: Tạo migration files cho tạo tables, add columns, indexes. Use seeders để populate initial data (admin user, categories).
5. **Transaction Management**: Implement order creation với transaction (create order, update inventory, create payment record), rollback on failure.
6. **MongoDB Integration**: Setup MongoDB với Mongoose, tạo Product schema với variants, reviews, images. Implement text search với indexes.
7. **Data Validation**: Server-side validation với Joi, custom validators cho email, phone, credit card. Database-level constraints.
8. **Query Optimization**: Implement eager loading cho relationships, add database indexes, optimize N+1 queries, use raw SQL cho complex queries.
9. **Database Backup**: Script để backup PostgreSQL (pg_dump) và MongoDB (mongodump), restore scripts, automated backup với cron.
10. **Database Monitoring**: Setup connection monitoring, slow query logging, connection pool stats, database health checks.

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
1. **API Design & Documentation**: Design REST API cho e-commerce (products, categories, orders, users). Use OpenAPI/Swagger cho documentation, implement versioning (/v1/), HATEOAS links.
2. **JWT Authentication**: Implement JWT authentication với access/refresh tokens, password hashing (bcrypt), login/logout, token refresh, secure cookie storage.
3. **Role-Based Authorization**: Setup RBAC với roles (admin, seller, customer), permissions (read, write, delete), middleware guards, resource ownership validation.
4. **Database Relationships**: Design normalized database schema (users, products, categories, orders, order_items, reviews), implement foreign keys, cascading deletes.
5. **Redis Caching**: Setup Redis cho session storage, API response caching (products list, user profile), cache invalidation strategies, cache warming.
6. **File Upload System**: Implement file upload với Multer, cloud storage (AWS S3), image optimization (sharp), multiple file types, upload progress tracking.
7. **Email Service**: Setup email service với Nodemailer, templates (handlebars), email queues (Bull), confirmation emails, password reset, order notifications.
8. **Real-time Notifications**: Implement WebSocket với Socket.IO cho order status updates, inventory alerts, chat system, real-time analytics dashboard.
9. **Docker Containerization**: Create Dockerfile cho Node.js app, docker-compose cho full stack (app, postgres, mongo, redis), multi-stage builds, environment configs.
10. **Cloud Deployment**: Deploy to AWS/Heroku với CI/CD (GitHub Actions), environment variables, health checks, monitoring (PM2), SSL certificates, domain setup.

## Phần 7: TypeScript trong Node.js

### Lý thuyết TypeScript
- **Static Typing**: Type annotations, interfaces.
- **Advanced Types**: Union, intersection, generics.
- **Decorators**: Metadata, framework integration.
- **Compilation**: tsc, ts-node for development.
- **Configuration**: tsconfig.json setup.

#### TypeScript Best Practices
- Tận dụng TypeScript cho type safety.
- Sử dụng generics cho type-safe collections.
- Setup decorators cho metadata.
- Sử dụng union types và intersection types.
- Tạo typed error classes.
- Implement observer pattern với TypeScript.

### Bài tập TypeScript (1-15)
1. **TypeScript Setup**: Khởi tạo project với TypeScript, cấu hình `tsconfig.json` (target: ES2020, strict: true, decorators), setup `ts-node` cho development.
2. **Interface & Types**: Tạo interfaces cho API responses (`ApiResponse<T>`, `User`, `Product`), union types cho status (`'active' | 'inactive'`), utility types (`Partial<T>`, `Pick<T>`).
3. **Generic Classes**: Implement generic `Repository<T>` class với CRUD methods, type-safe query builders, generic constraints (`T extends BaseEntity`).
4. **Decorator Implementation**: Tạo decorators cho route definitions (`@Get()`, `@Post()`), validation (`@Required()`, `@Email()`), logging (`@LogExecutionTime()`).
5. **Advanced Types**: Use intersection types cho combined interfaces, conditional types, mapped types, template literal types cho API paths.
6. **Module Augmentation**: Extend Express types cho custom properties (`req.user`, `req.session`), add custom middleware types, type-safe error handling.
7. **Type Guards**: Implement type guards cho runtime type checking (`isUser()`, `isProduct()`), discriminated unions cho API responses.
8. **Error Handling**: Create typed error classes (`HttpError`, `ValidationError`), error middleware với proper typing, global error handler với TypeScript.
9. **Dependency Injection**: Setup IoC container với `inversify`, typed service registration, constructor injection, scoped dependencies.
10. **Database Types**: Typed database queries với generics, entity decorators (`@Entity()`, `@Column()`), repository interfaces với type safety.
11. **API Types**: Strongly typed API clients, request/response types, validation schemas với `joi` + TypeScript, OpenAPI type generation.
12. **Testing Types**: Typed test utilities, mock factories với generics, assertion helpers, end-to-end test types.
13. **Configuration Types**: Environment variable types, configuration validation, typed config objects, runtime config loading.
14. **Middleware Types**: Generic middleware types, typed request handlers, custom response types, authentication middleware với TypeScript.
15. **Production Setup**: TypeScript compilation optimization, source maps, declaration files, type checking in CI/CD, performance monitoring.

## Phần 8: Dự án E-commerce Hoàn chỉnh

### Lý thuyết Phát triển Dự án
- **Planning**: Thu thập requirements, user stories, technical specifications, thiết kế architecture.
- **Development**: Phương pháp Agile/Scrum, phát triển iterative, code reviews, version control (Git flow).
- **Testing**: Unit testing, integration testing, E2E testing, performance testing, security testing.
- **Deployment**: CI/CD pipelines, containerization (Docker), orchestration (Kubernetes), cloud platforms (AWS/Heroku).
- **Maintenance**: Monitoring (application metrics, error tracking), logging, performance optimization, security updates.
- **E-commerce Specific**: Xử lý thanh toán, quản lý inventory, order fulfillment, tích hợp customer service, tuân thủ quy định (PCI DSS, GDPR).

### Bài tập Dự án E-commerce (1-20)

#### Phase 1: Project Setup & Core Features (1-5)
1. **Project Initialization**: Setup Node.js + TypeScript project, cấu hình ESLint + Prettier, setup testing (Jest + Supertest), create folder structure (MVC pattern).
2. **Database Design**: Design PostgreSQL schema cho e-commerce (users, products, categories, orders, reviews), create migrations, setup MongoDB cho product reviews.
3. **User Authentication**: Implement JWT authentication, user registration/login, password reset, email verification, role-based access (customer, admin, seller).
4. **Product Management**: CRUD operations cho products (name, description, price, images, categories, inventory), product variants (size, color), search & filtering.
5. **Category System**: Hierarchical categories, category CRUD, product-category relationships, category-based navigation.

#### Phase 2: Shopping Features (6-10)
6. **Shopping Cart**: Add to cart, update quantities, remove items, cart persistence, cart validation, guest cart vs user cart.
7. **Order Management**: Order creation từ cart, order status tracking (pending, confirmed, shipped, delivered), order history, order cancellation.
8. **Payment Integration**: Integrate Stripe/PayPal, payment methods (credit card, PayPal), payment status, webhooks handling, refund processing.
9. **Inventory Management**: Stock tracking, low stock alerts, automatic stock updates on orders, backorder handling, inventory reports.
10. **Shipping System**: Shipping rates calculation, shipping methods (standard, express), address management, shipping tracking integration.

#### Phase 3: Advanced Features (11-15)
11. **Review & Rating System**: Product reviews với ratings (1-5 stars), review moderation, review responses, average rating calculation.
12. **Wishlist & Favorites**: User wishlists, add/remove products, wishlist sharing, wishlist notifications for price drops.
13. **Search & Filtering**: Full-text search với Elasticsearch, advanced filtering (price range, category, brand), search suggestions, search analytics.
14. **Promotions & Discounts**: Coupon codes, percentage discounts, free shipping thresholds, promotion scheduling, discount validation.
15. **Email Notifications**: Order confirmations, shipping updates, password reset, promotional emails, email templates với Handlebars.

#### Phase 4: Performance & Security (16-20)
16. **Caching Strategy**: Redis caching cho products, categories, user sessions, API response caching, cache invalidation strategies.
17. **Security Implementation**: Input validation & sanitization, rate limiting, CORS setup, helmet security headers, SQL injection prevention.
18. **File Upload System**: Image upload cho products với optimization, cloud storage (AWS S3), CDN integration, image resizing.
19. **Real-time Features**: WebSocket cho order status updates, live chat support, real-time inventory updates, notification system.
20. **Deployment & Monitoring**: Docker containerization, CI/CD pipeline (GitHub Actions), monitoring (PM2, Winston), error tracking, performance optimization.

#### Yêu cầu Kỹ thuật:
- **Architecture**: Clean Architecture với separation of concerns
- **Code Quality**: 80%+ test coverage, ESLint compliance, TypeScript strict mode
- **Performance**: Response time < 200ms, handle 1000+ concurrent users
- **Security**: OWASP compliance, JWT security, input validation
- **Scalability**: Database indexing, query optimization, horizontal scaling ready
- **Documentation**: API documentation (Swagger), code documentation, deployment guides

#### Tính năng Bonus (Tùy chọn):
- Hỗ trợ đa ngôn ngữ (i18n)
- Tối ưu API cho mobile
- Admin dashboard
- Analytics & reporting
- Social login integration
- Recommendation engine

## Tài liệu tham khảo
- [Node.js Docs](https://nodejs.org/en/docs/)
- [Express.js Guide](https://expressjs.com/)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [Clean Code](https://www.oreilly.com/library/view/clean-code/9780136083238/)
