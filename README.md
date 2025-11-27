# Pre-Backend Course Guide

## Giới thiệu
Chào mừng bạn đến với khóa học Pre-Backend! Khóa học này được thiết kế để chuẩn bị cho bạn kiến thức cơ bản về phát triển backend, bao gồm Node.js, SQL, NoSQL và các công nghệ liên quan. Bạn sẽ học qua các bài giảng, bài tập thực hành và dự án nhỏ để củng cố kiến thức.

## Mục tiêu khóa học
- Hiểu rõ các khái niệm cơ bản và nâng cao của backend development.
- Thành thạo Node.js để xây dựng ứng dụng server-side mạnh mẽ và scalable.
- Học cách làm việc chuyên sâu với cơ sở dữ liệu PostgreSQL (SQL) và MongoDB (NoSQL).
- Phát triển kỹ năng giải quyết vấn đề thực tế thông qua các challenge và dự án.
- Áp dụng các best practices như testing, security, và deployment.

## Nội dung khóa học

### 1. Node.js Basics và Advanced
- Cài đặt Node.js và npm, quản lý phiên bản với nvm.
- Modules, require, exports, ES6 modules.
- Asynchronous programming: callbacks, promises, async/await, event loop.
- Xây dựng HTTP server với Express.js: middleware, routing, error handling.
- Advanced: Streams, child processes, clustering cho scalability.

### 2. PostgreSQL Databases (SQL)
- Giới thiệu Relational Databases và ACID properties.
- Cài đặt và sử dụng PostgreSQL: psql, pgAdmin.
- Cú pháp SQL nâng cao: JOINs, subqueries, indexes, views, stored procedures.
- Thiết kế database schema: normalization, relationships, constraints.
- Quy tắc chung: Mỗi bảng sử dụng UUID làm primary key, và cần có các trường created_at, updated_at, created_by, updated_by để tracking audit.
- Transactions, concurrency, và optimization.
- Kết nối và truy vấn với Node.js sử dụng pg hoặc Sequelize ORM.

### 3. NoSQL Databases (MongoDB)
- Sự khác biệt giữa SQL và NoSQL: khi nào dùng gì.
- MongoDB: Documents, Collections, Indexes, Aggregation Pipeline.
- CRUD operations, schema validation, replication.
- Kết nối MongoDB với Node.js sử dụng Mongoose: models, middleware, validation.

### 4. Các chủ đề chuyên sâu và tổng quát
- RESTful APIs và GraphQL.
- Authentication (JWT, OAuth), Authorization (RBAC), Sessions.
- Security: CORS, Helmet, rate limiting, input validation.
- Error handling, logging với Winston, monitoring.
- Testing: Unit tests với Jest, integration tests, TDD.
- Deployment: Docker, Kubernetes, CI/CD với GitHub Actions.
- Performance: Caching (Redis), load balancing, profiling.
- Best practices: Code structure, environment variables, API versioning.
- File uploads, email sending, scheduling tasks, WebSockets.

## Tài liệu tham khảo
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Express.js Guide](https://expressjs.com/en/guide/routing.html)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Sequelize ORM](https://sequelize.org/)
- [MongoDB Manual](https://docs.mongodb.com/manual/)
- [Mongoose Documentation](https://mongoosejs.com/docs/)
- [Jest Testing](https://jestjs.io/)
- [Docker Docs](https://docs.docker.com/)

Ngoài ra, xem file `sql/sql-queries-types.md` cho chi tiết về các loại truy vấn SQL và bài tập.

## Challenges và Bài tập
Trong thư mục này, bạn sẽ tìm thấy các challenge thực tế để áp dụng kiến thức đã học, bao gồm từ cơ bản Node.js, database, đến advanced topics như authentication, testing, deployment, caching, GraphQL, và microservices. Mỗi challenge bao gồm:
- Mô tả yêu cầu.
- Dữ liệu mẫu.
- Hướng dẫn giải quyết.

Hãy bắt đầu với challenge đầu tiên và dần dần tiến bộ!

## Cách sử dụng
1. Clone repository này về máy.
2. Cài đặt dependencies: `npm install`
3. Chạy các challenge theo hướng dẫn trong từng thư mục.

## Liên hệ
Nếu có câu hỏi, hãy tạo issue trên GitHub hoặc liên hệ với giảng viên.

Chúc bạn học tập hiệu quả!