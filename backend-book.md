# Học Backend Từ Cơ Bản Đến Nâng Cao - Hướng Dẫn Hoàn Chỉnh

## Giới Thiệu
Chào mừng bạn đến với hành trình học Backend! Tài liệu này cung cấp lộ trình từng bước để bạn nắm vững các khái niệm cơ bản và xây dựng kỹ năng thực tế. Giả sử bạn đã biết cơ bản về lập trình (như JavaScript hoặc C#). Repo này bao gồm sách hướng dẫn chi tiết, lộ trình học tập, bài tập thực hành (challenges), và tài liệu chuyên sâu về Node.js, .NET, và SQL.

**Mục tiêu:**
- Nắm vững khái niệm cơ bản và nâng cao của Backend development.
- Học cách xây dựng API, tích hợp database, thêm authentication, testing, và deployment.
- Thực hành qua challenges để áp dụng kiến thức.
- Chọn framework: Node.js (dễ học, phổ biến) hoặc .NET (enterprise, mạnh mẽ).

**Cách Sử Dụng Repo Để Tự Học:**
1. **Bắt Đầu với Lý Thuyết**: Đọc phần Lý Thuyết Cơ Bản dưới đây.
2. **Theo Lộ Trình Học**: Làm theo các bước trong phần Lộ Trình Học.
3. **Thực Hành với Challenges**: Xem `table-of-contents.md` và thư mục `challenges/`.
4. **Đi Sâu với Tài Liệu Chuyên Sâu**: Đọc `node/`, `dotnet/`, `sql/`.
5. **Thực Hành Dự Án**: Xây dựng projects nhỏ, sử dụng Git để lưu trên GitHub/GitLab.

**Phương Pháp Học:**
- Học bằng thực hành: Code mỗi ngày.
- Xây dựng dự án nhỏ để áp dụng lý thuyết.
- Đọc tài liệu chính thức, không chỉ tutorial.
- Sử dụng GitHub/GitLab để lưu code, collaborate và showcase projects.
- Thực hành liên tục: Xây dựng 3-5 projects nhỏ.
- Debugging: Học cách đọc error messages.
- Scalability: Nghĩ về performance sớm.
- Networking: Kết nối với cộng đồng dev.

## Mục Lục
### Phần 1: Lý Thuyết Cơ Bản
1. [Giới Thiệu Về Backend](#1-giới-thiệu-về-backend)
2. [HTTP và Client-Server Flow](#2-http-và-client-server-flow)
3. [API và JSON](#3-api-và-json)
4. [Swagger/OpenAPI](#4-swaggeropenapi)
5. [Database Cơ Bản](#5-database-cơ-bản)
6. [Authentication & Authorization](#6-authentication--authorization)

### Phần 2: Frameworks và Tools
7. [Frameworks và Tools Phổ Biến](#7-frameworks-và-tools-phổ-biến)
8. [Xây Dựng API Đơn Giản](#8-xây-dựng-api-đơn-giản)
9. [Tích Hợp Database](#9-tích-hợp-database)
10. [Authentication & Authorization](#10-authentication--authorization)
11. [Testing và Deployment](#11-testing-và-deployment)

### Phần 3: Lộ Trình Học và Tài Liệu
12. [Lộ Trình Học Backend](#12-lộ-trình-học-backend)
13. [Challenges và Bài Tập](#13-challenges-và-bài-tập)
14. [Tài Nguyên Học Thêm](#14-tài-nguyên-học-thêm)

### Phụ Lục
15. [Bộ Bài Tập Tư Duy Backend và Dự Án Thực Tế](#15-bộ-bài-tập-tư-duy-backend-và-dự-án-thực-tế)
16. [Tóm Tắt và Kết Luận](#16-tóm-tắt-và-kết-luận)

---

## 1. Giới Thiệu Về Backend

Backend là phần xử lý logic phía server, quản lý dữ liệu và giao tiếp với frontend.

**Khái niệm chính:**
- Server-side logic
- Database management
- API development
- Security và performance

## 2. HTTP và Client-Server Flow

### HTTP (HyperText Transfer Protocol)

HTTP là giao thức truyền tải siêu văn bản, là nền tảng của World Wide Web. Nó định nghĩa cách các máy khách (client) và máy chủ (server) giao tiếp qua mạng.

#### Các Phương Thức HTTP Chính:
- **GET**: Lấy dữ liệu từ server.
- **POST**: Gửi dữ liệu mới lên server.
- **PUT**: Cập nhật dữ liệu hiện có.
- **DELETE**: Xóa dữ liệu.
- **PATCH**: Cập nhật một phần dữ liệu.

#### Cấu Trúc HTTP Request:
- **Request Line**: Phương thức, URL, phiên bản HTTP.
- **Headers**: Thông tin bổ sung (ví dụ: Content-Type, Authorization).
- **Body**: Dữ liệu gửi kèm (thường cho POST/PUT).

#### Cấu Trúc HTTP Response:
- **Status Line**: Phiên bản HTTP, mã trạng thái, lý do.
- **Headers**: Thông tin phản hồi.
- **Body**: Dữ liệu trả về.

### Cấu Trúc Chi Tiết HTTP Request/Response

#### Cấu Trúc HTTP Request:
Một HTTP request bao gồm ba phần chính:

1. **Request Line**:
   - Phương thức HTTP (GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD).
   - URL (Uniform Resource Locator), bao gồm protocol (http/https), domain, path, query parameters.
   - Phiên bản HTTP (thường là HTTP/1.1 hoặc HTTP/2).

   Ví dụ: `GET /api/users?page=1 HTTP/1.1`

2. **Headers**:
   - Các cặp key-value cung cấp thông tin bổ sung.
   - Ví dụ:
     - `Host: api.example.com` – Tên miền đích.
     - `User-Agent: Mozilla/5.0` – Thông tin về client.
     - `Content-Type: application/json` – Loại dữ liệu trong body (cho POST/PUT).
     - `Authorization: Bearer <token>` – Token xác thực.
     - `Accept: application/json` – Loại dữ liệu mong muốn trong response.
     - `Cache-Control: no-cache` – Hướng dẫn về caching.

3. **Body** (Tùy chọn):
   - Dữ liệu gửi kèm, thường cho POST/PUT/PATCH.
   - Có thể là JSON, XML, form data, file upload.
   - Ví dụ JSON body: `{"name": "Nguyen", "email": "nguyen@example.com"}`

#### Cấu Trúc HTTP Response:
Một HTTP response cũng gồm ba phần:

1. **Status Line**:
   - Phiên bản HTTP.
   - Mã trạng thái (status code) và lý do ngắn gọn.
   - Ví dụ: `HTTP/1.1 200 OK`

2. **Headers**:
   - Thông tin phản hồi.
   - Ví dụ:
     - `Content-Type: application/json` – Loại dữ liệu trong body.
     - `Content-Length: 1024` – Kích thước body.
     - `Set-Cookie: sessionId=abc123` – Thiết lập cookie.
     - `Cache-Control: max-age=3600` – Hướng dẫn caching.

3. **Body**:
   - Dữ liệu trả về, có thể là JSON, HTML, XML, file, etc.
   - Ví dụ: `{"users": [{"id": 1, "name": "Nguyen"}]}`

#### Ví Dụ Hoàn Chỉnh:
- **Request**:
  ```
  POST /api/users HTTP/1.1
  Host: api.example.com
  Content-Type: application/json
  Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

  {"name": "Nguyen", "email": "nguyen@example.com"}
  ```

- **Response**:
  ```
  HTTP/1.1 201 Created
  Content-Type: application/json
  Location: /api/users/123

  {"id": 123, "name": "Nguyen", "email": "nguyen@example.com"}
  ```

#### Các Phương Thức HTTP Chi Tiết:
- **GET**: Lấy dữ liệu, không có body, idempotent (lặp lại không thay đổi).
- **POST**: Tạo tài nguyên mới, có body, không idempotent.
- **PUT**: Cập nhật toàn bộ tài nguyên, có body, idempotent.
- **PATCH**: Cập nhật một phần, có body, không idempotent.
- **DELETE**: Xóa tài nguyên, không có body, idempotent.
- **HEAD**: Giống GET nhưng chỉ lấy headers, không body.
- **OPTIONS**: Kiểm tra các phương thức được hỗ trợ.

#### Mã Trạng Thái Chi Tiết:
- **1xx (Informational)**: 100 Continue, 101 Switching Protocols.
- **2xx (Success)**: 200 OK, 201 Created, 204 No Content.
- **3xx (Redirection)**: 301 Moved Permanently, 302 Found, 304 Not Modified.
- **4xx (Client Error)**: 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 422 Unprocessable Entity.
- **5xx (Server Error)**: 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable.

### Các Nội Dung Backend Thường Làm

Backend không chỉ nhận request và trả response, mà còn xử lý nhiều logic phức tạp để đảm bảo ứng dụng hoạt động hiệu quả, bảo mật và scalable. Dưới đây là các nội dung chính mà Backend developers thường thực hiện:

#### 1. **Xử Lý Request và Validation**:
   - Parse dữ liệu từ request (JSON, form data, query params).
   - Validate input: Kiểm tra định dạng, ràng buộc (required fields, data types, length).
   - Sanitize dữ liệu để tránh injection attacks (SQL injection, XSS).
   - Ví dụ: Sử dụng thư viện như Joi (Node.js) hoặc DataAnnotations (.NET) để validate.

#### 2. **Business Logic**:
   - Thực hiện logic nghiệp vụ: Tính toán, xử lý quy trình (workflow).
   - Tương tác với database: CRUD operations, queries phức tạp.
   - Gọi external APIs hoặc services (payment gateways, email services).
   - Ví dụ: Tính tổng đơn hàng, kiểm tra inventory trước khi đặt hàng.

#### 3. **Database Management**:
   - Thiết kế schema (tables, relationships).
   - Viết queries: SELECT, INSERT, UPDATE, DELETE; JOINs, aggregations.
   - Optimize performance: Indexing, caching, connection pooling.
   - Migration: Cập nhật schema mà không mất dữ liệu.

#### 4. **Authentication và Authorization**:
   - Xác thực user: Login, logout, password reset.
   - Ủy quyền: Kiểm tra quyền truy cập (roles, permissions).
   - Sử dụng JWT, OAuth, sessions.
   - Bảo mật: Hash passwords, rate limiting, CORS.

#### 5. **Error Handling và Logging**:
   - Catch và xử lý errors: Trả về appropriate status codes và messages.
   - Logging: Ghi lại requests, errors, performance metrics (sử dụng Winston cho Node.js, Serilog cho .NET).
   - Monitoring: Track uptime, response times với tools như PM2, Application Insights.

#### 6. **Caching và Performance**:
   - Cache dữ liệu thường dùng: Redis, in-memory cache.
   - Optimize queries, sử dụng pagination.
   - Load balancing, horizontal scaling.

#### 7. **Security**:
   - Bảo vệ chống attacks: CSRF, XSS, SQL injection.
   - Encryption: HTTPS, encrypt sensitive data.
   - Compliance: GDPR, PCI-DSS nếu cần.

#### 8. **API Design và Documentation**:
   - Thiết kế RESTful/GraphQL APIs.
   - Tài liệu với Swagger/OpenAPI.
   - Versioning APIs để backward compatibility.

#### 9. **Testing**:
   - Unit tests: Test functions riêng lẻ.
   - Integration tests: Test toàn bộ flow.
   - End-to-end tests: Simulate user interactions.

#### 10. **Deployment và DevOps**:
    - Containerization: Docker.
    - CI/CD: GitHub Actions, Jenkins.
    - Hosting: AWS, Azure, Heroku.
    - Monitoring production: Logs, alerts.

#### 11. **Maintenance và Optimization**:
    - Refactor code để maintainability.
    - Update dependencies, patch security vulnerabilities.
    - Performance tuning: Profiling, optimizing bottlenecks.

#### Ví Dụ Workflow Backend:
1. Nhận request từ client.
2. Validate và parse data.
3. Kiểm tra auth.
4. Thực hiện business logic (query DB, tính toán).
5. Trả response hoặc handle error.
6. Log event.

Những nội dung này giúp Backend không chỉ "chạy" mà còn robust, secure và scalable. Khi học, tập trung vào từng phần và áp dụng qua projects nhỏ.

### Client-Server Flow (Luồng Client-Server)

Mô hình client-server là kiến trúc mạng nơi client (trình duyệt, ứng dụng) gửi yêu cầu đến server, và server xử lý rồi trả về phản hồi. Đây là nền tảng của hầu hết các ứng dụng web và mobile.

#### Sơ Đồ Tổng Quan Client-Server Flow:

```
[Client (Browser/Mobile App)]
         |
         | HTTP Request (GET/POST/PUT/DELETE)
         v
[Web Server (e.g., Nginx/Apache)]
         |
         | Forward Request
         v
[Application Server (e.g., Node.js/Express, C#/ASP.NET Core)]
         |
         | Query/Process
         v
[Database (e.g., MySQL, MongoDB)]
         |
         | Return Data
         v
[Application Server]
         |
         | Send Response
         v
[Web Server]
         |
         | HTTP Response (JSON/HTML/Status Code)
         v
[Client]
         |
         | Render/Update UI
```

#### Mô Tả Các Thành Phần Chính:

1. **Client (Máy Khách)**:
   - Là thiết bị hoặc ứng dụng gửi yêu cầu (ví dụ: trình duyệt web, app mobile).
   - Gửi HTTP request với phương thức, URL, headers, body.
   - Nhận và xử lý response để hiển thị dữ liệu.

2. **Web Server (Máy Chủ Web)**:
   - Nhận request từ client qua internet.
   - Chịu trách nhiệm routing, load balancing, SSL/TLS encryption (HTTPS).
   - Ví dụ: Nginx, Apache. Chuyển request đến application server.

3. **Application Server (Máy Chủ Ứng Dụng)**:
   - Xử lý logic nghiệp vụ: parse request, validate data, thực hiện tính toán, truy vấn database.
   - Tạo response dựa trên kết quả.
   - Ví dụ: Node.js với Express, C# với ASP.NET Core.

4. **Database (Cơ Sở Dữ Liệu)**:
   - Lưu trữ dữ liệu persistent.
   - Application server truy vấn để lấy/cập nhật dữ liệu.
   - Ví dụ: Relational (MySQL, PostgreSQL) hoặc NoSQL (MongoDB, Redis).

5. **Network (Mạng)**:
   - Kết nối client và server qua internet/intranet.
   - Sử dụng giao thức TCP/IP, với HTTP/HTTPS ở tầng ứng dụng.

#### Luồng Cơ Bản:
1. **Client gửi HTTP request**: Client (ví dụ: trình duyệt) gửi yêu cầu đến server qua URL. Request bao gồm phương thức HTTP, headers và body nếu cần.
2. **Server nhận và xử lý request**: Server phân tích request, thực hiện logic nghiệp vụ (có thể truy vấn database, gọi API bên thứ ba, tính toán).
3. **Server gửi HTTP response**: Server trả về dữ liệu dưới dạng JSON/XML/HTML, kèm theo status code và headers.
4. **Client nhận và xử lý response**: Client hiển thị dữ liệu, cập nhật UI hoặc thực hiện hành động tiếp theo.

#### Ví Dụ Luồng Đơn Giản:
- Người dùng nhập URL vào trình duyệt (client).
- Trình duyệt gửi GET request đến server.
- Server truy vấn database và trả về HTML/JSON.
- Trình duyệt render trang web.

#### Các Loại Flow:
- **Synchronous (Đồng Bộ)**: Client chờ response từ server trước khi tiếp tục. Phù hợp cho các tác vụ đơn giản.
- **Asynchronous (Bất Đồng Bộ)**: Client không chờ, có thể gửi nhiều request song song. Sử dụng AJAX, WebSockets cho real-time updates.

#### Stateless vs Stateful:
- **Stateless**: Mỗi request độc lập, server không lưu trạng thái client (dễ scale, nhưng cần authentication mỗi lần).
- **Stateful**: Server lưu trạng thái client (ví dụ: session), phức tạp hơn nhưng phù hợp cho ứng dụng cần duy trì trạng thái.

#### Bảo Mật Trong Flow:
- Sử dụng HTTPS để mã hóa dữ liệu.
- Authentication: JWT, OAuth.
- Rate limiting để tránh DDoS.

#### Đặc Điểm:
- **Stateless**: Mỗi request độc lập, server không lưu trạng thái client.
- **Scalable**: Có thể thêm nhiều server để xử lý tải.
- **Security**: Cần bảo mật dữ liệu truyền tải (HTTPS).

## 3. API và JSON

### API (Application Programming Interface)

API là tập hợp các quy tắc và giao thức cho phép các ứng dụng phần mềm giao tiếp với nhau. Trong Backend, API thường là RESTful API hoặc GraphQL.

#### RESTful API:
- Sử dụng HTTP methods.
- Resources được định danh bằng URL (ví dụ: `/users`, `/products`).
- Stateless, cacheable.

#### Ví Dụ API Endpoint:
- GET /api/users: Lấy danh sách người dùng.
- POST /api/users: Tạo người dùng mới.
- PUT /api/users/1: Cập nhật người dùng có ID 1.

#### Thiết Kế API Tốt:
- Sử dụng đúng HTTP status codes.
- Versioning (ví dụ: /v1/api/users).
- Authentication/Authorization.

### JSON (JavaScript Object Notation)

JSON là định dạng dữ liệu nhẹ, dễ đọc và dễ phân tích. Được sử dụng rộng rãi để trao đổi dữ liệu giữa client và server.

#### Cấu Trúc JSON:
```json
{
  "name": "Nguyễn Văn A",
  "age": 25,
  "email": "a@example.com",
  "skills": ["JavaScript", "Node.js", "SQL"]
}
```

#### Đặc Điểm:
- Key-value pairs.
- Hỗ trợ: string, number, boolean, null, object, array.
- Không hỗ trợ comment hoặc function.

#### Sử Dụng Trong Backend:
- Parse JSON từ request body.
- Serialize object thành JSON để response.

## 4. Swagger/OpenAPI

Swagger là công cụ để thiết kế, xây dựng và tài liệu hóa API. Hiện tại là OpenAPI Specification.

#### Lợi Ích:
- Tạo tài liệu API tự động.
- Test API trực tiếp từ giao diện web.
- Generate code cho client/server từ spec.

#### Cách Sử Dụng:
- Viết YAML/JSON spec mô tả API.
- Sử dụng Swagger UI để hiển thị tài liệu.
- Integrate với framework như Express.js qua swagger-jsdoc.

#### Ví Dụ Spec Cơ Bản:
```yaml
openapi: 3.0.0
info:
  title: Sample API
  version: 1.0.0
paths:
  /users:
    get:
      summary: Get all users
      responses:
        '200':
          description: Success
```

## 5. Database Cơ Bản

Database là nơi lưu trữ dữ liệu cho ứng dụng. Backend thường tương tác với database để lưu và truy xuất dữ liệu.

#### SQL vs NoSQL:
- **SQL (Relational)**: Sử dụng bảng, quan hệ. Ví dụ: MySQL, PostgreSQL. Phù hợp cho dữ liệu có cấu trúc.
- **NoSQL**: Linh hoạt hơn, không có schema cố định. Ví dụ: MongoDB (document), Redis (key-value). Phù hợp cho dữ liệu lớn, không cấu trúc.

#### Các Hoạt Động Cơ Bản:
- **CRUD**: Create, Read, Update, Delete.
- **Query**: SELECT, INSERT, UPDATE, DELETE trong SQL; find, insert trong MongoDB.

#### Ví Dụ SQL Query:
```sql
SELECT * FROM users WHERE age > 18;
INSERT INTO users (name, email) VALUES ('Nguyen', 'nguyen@example.com');
```

#### Kết Nối Database Trong Code:
- Sử dụng ORM như Sequelize (Node.js) hoặc Entity Framework (.NET) để tương tác dễ dàng.

## 7. Authentication & Authorization

Authentication (Xác thực) là kiểm tra danh tính người dùng, Authorization (Ủy quyền) là kiểm tra quyền truy cập.

#### Phương Pháp Cơ Bản:
- **Basic Auth**: Username/Password qua header.
- **JWT (JSON Web Tokens)**: Token chứa thông tin user, không cần lưu session trên server.
- **OAuth**: Cho phép ứng dụng truy cập tài nguyên của user từ provider khác (Google, Facebook).

#### Ví Dụ JWT Flow:
1. User đăng nhập, server tạo JWT.
2. Client gửi JWT trong header cho mỗi request.
3. Server verify JWT để xác thực.

#### Bảo Mật:
- Hash password (bcrypt).
- Sử dụng HTTPS.
- Refresh tokens để tránh lộ JWT.

## 7. Frameworks và Tools Phổ Biến

Frameworks giúp phát triển nhanh hơn bằng cách cung cấp cấu trúc sẵn.

#### Frameworks Backend:
- **Node.js với Express.js**: Nhẹ, nhanh cho API, phù hợp cho JavaScript developers.
- **C# với ASP.NET Core**: Enterprise-level, scalable, mạnh mẽ cho .NET ecosystem.

#### Tools Hỗ Trợ:
- **Git**: Version control, commands cơ bản: git add, commit, push.
- **Postman**: Test API endpoints.
- **VS Code**: Editor phổ biến với extensions cho debugging.

#### Hướng Dẫn Git và GitHub/GitLab:
Git là hệ thống quản lý phiên bản phân tán, giúp theo dõi thay đổi code và hợp tác. GitHub/GitLab là nền tảng hosting repositories.

##### Cài Đặt và Cơ Bản:
- Download từ [git-scm.com](https://git-scm.com/), cấu hình: `git config --global user.name "Name"` và `git config --global user.email "email"`.
- Lệnh cơ bản: `git init`, `git add .`, `git commit -m "msg"`, `git status`, `git log --oneline`.

##### Làm Việc với Remote:
- Tạo repo trên GitHub/GitLab, liên kết: `git remote add origin <url>`.
- Push: `git push -u origin main`.
- Clone: `git clone <url>`.

##### Branch và Merge:
- Tạo branch: `git checkout -b <name>`.
- Merge: `git merge <branch>`.
- Pull Request trên GitHub/GitLab để review.

##### Best Practices:
- Commit thường xuyên với message rõ ràng.
- Sử dụng branch cho features.
- Push lên remote để backup.

Xem docs: [git-scm.com](https://git-scm.com/docs), [github.com/docs](https://docs.github.com).

#### Lựa Chọn Framework:
Bạn có thể chọn một trong hai: Node.js (dễ học, phổ biến) hoặc .NET (mạnh mẽ, enterprise). Hướng dẫn dưới đây sẽ cung cấp song song cho cả hai.

#### Ví Dụ Code Cơ Bản:
- **Với Express.js (Node.js)**:
  ```javascript
  const express = require('express');
  const app = express();
  app.get('/api/hello', (req, res) => res.json({ message: 'Hello World!' }));
  app.listen(3000, () => console.log('Server running on port 3000'));
  ```

- **Với ASP.NET Core (.NET)**:
  ```csharp
  var builder = WebApplication.CreateBuilder(args);
  var app = builder.Build();
  app.MapGet("/api/hello", () => new { message = "Hello World!" });
  app.Run();
  ```

## 8. Xây Dựng API Đơn Giản

### Với Node.js và Express.js

#### Công Cụ:
- Node.js + Express.js.

#### Các Bước:
1. Cài đặt Node.js/npm.
2. Tạo project: `npm init -y` và cài `express`.
3. Viết code cơ bản:
   ```javascript
   const express = require('express');
   const app = express();
   app.use(express.json());

   app.get('/api/hello', (req, res) => res.json({ message: 'Hello World!' }));

   app.listen(3000, () => console.log('Server running on port 3000'));
   ```
4. Chạy server: `node app.js`.
5. Test với Postman: GET http://localhost:3000/api/hello.

#### Thêm Chức Năng:
- POST endpoint để tạo "user" (lưu trong array tạm thời).
- Sử dụng Swagger để tài liệu API (swagger-jsdoc + swagger-ui-express).

### Với C# và ASP.NET Core

#### Công Cụ:
- .NET SDK + ASP.NET Core.

#### Các Bước:
1. Cài .NET SDK.
2. Tạo project: `dotnet new webapi -n MyApi`.
3. Viết code cơ bản trong `Program.cs`:
   ```csharp
   var builder = WebApplication.CreateBuilder(args);
   var app = builder.Build();

   app.MapGet("/api/hello", () => new { message = "Hello World!" });

   app.Run();
   ```
4. Chạy: `dotnet run`.
5. Test với Postman: GET http://localhost:5000/api/hello.

#### Thêm Chức Năng:
- POST endpoint để tạo "user".
- Sử dụng Swagger/OpenAPI.

#### Mục Tiêu Chung: Xây dựng và test API cơ bản với framework đã chọn.

## 9. Tích Hợp Database

### Với Node.js

#### Các Bước Cho MongoDB:
1. Cài MongoDB local hoặc dùng MongoDB Atlas (free).
2. Cài mongoose: `npm install mongoose`.
3. Tạo model User:
   ```javascript
   const mongoose = require('mongoose');
   const userSchema = new mongoose.Schema({ name: String, email: String });
   module.exports = mongoose.model('User', userSchema);
   ```
4. Kết nối DB: `mongoose.connect('mongodb://localhost:27017/myapp');`
5. Thêm CRUD endpoints: GET /users, POST /users, etc.
6. Test với Postman.

#### Các Bước Cho PostgreSQL:
1. Cài PostgreSQL local hoặc dùng ElephantSQL (free).
2. Cài pg: `npm install pg`.
3. Tạo table User:
   ```sql
   CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(255), email VARCHAR(255));
   ```
4. Kết nối DB:
   ```javascript
   const { Pool } = require('pg');
   const pool = new Pool({ connectionString: 'postgresql://user:pass@localhost:5432/myapp' });
   ```
5. Thêm CRUD queries: SELECT, INSERT, UPDATE, DELETE.
6. Test với Postman.

### Với .NET

#### Ví dụ với PostgreSQL:
1. Cài packages: `dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL`.
2. Tạo model User:
   ```csharp
   public class User { public int Id { get; set; } public string Name { get; set; } public string Email { get; set; } }
   ```
3. Kết nối DB trong `Program.cs`.
4. Thêm CRUD endpoints.

#### Với MongoDB:
- Sử dụng MongoDB.Driver.

#### Mục Tiêu Chung: Lưu và truy xuất dữ liệu từ DB.

## 10. Authentication & Authorization

### Với Node.js
1. Cài bcryptjs và jsonwebtoken.
2. Tạo endpoint đăng ký: Hash password, lưu user.
3. Tạo endpoint đăng nhập: Verify password, tạo JWT.
4. Middleware để verify JWT cho protected routes.
   ```javascript
   const jwt = require('jsonwebtoken');
   const auth = (req, res, next) => {
     const token = req.header('Authorization').replace('Bearer ', '');
     try {
       req.user = jwt.verify(token, 'secret');
       next();
     } catch (e) { res.status(401).send('Unauthorized'); }
   };
   ```

### Với .NET
- Sử dụng JWT: `dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer`.
- Tạo endpoints đăng ký/đăng nhập, middleware verify token.

#### Mục Tiêu Chung: Bảo vệ API với JWT.

## 11. Testing và Deployment

### Testing:
- **Node.js**: Cài Jest, viết unit tests.
- **.NET**: xUnit hoặc NUnit.
- Chạy `npm test` hoặc `dotnet test`.

### Deployment:
- Containerize với Docker (Dockerfile như trong essentials).
- Push code lên GitHub/GitLab: Tạo repo, `git init`, `git add .`, `git commit -m "Initial commit"`, `git push origin main`.
- Deploy lên Heroku: `heroku create`, `git push heroku main`.
- Hoặc dùng Vercel cho serverless, integrate với GitHub.

#### Containerization với Docker:
Docker là nền tảng container hóa cho phép đóng gói ứng dụng và dependencies vào container để chạy nhất quán trên mọi môi trường.

##### Khái Niệm Cơ Bản:
- **Image**: Template chỉ đọc chứa code, runtime, libraries.
- **Container**: Instance chạy của image.
- **Dockerfile**: Script để build image.

##### Lệnh Cơ Bản:
- `docker build -t myapp .`: Build image từ Dockerfile.
- `docker run -p 3000:3000 myapp`: Chạy container.
- `docker-compose up`: Chạy multi-container app.

##### Lợi Ích Cho Backend:
- Environment consistency (dev, staging, prod).
- Easy scaling và deployment.
- Isolation giữa services.

##### Ví Dụ Dockerfile Cho Node.js App:
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

##### Ví Dụ Dockerfile Cho .NET App:
```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app .
EXPOSE 80
ENTRYPOINT ["dotnet", "MyApi.dll"]
```

#### Mục Tiêu: Code tested và app chạy online, code được lưu trên GitHub/GitLab.

## 12. Lộ Trình Học Backend

Testing đảm bảo chất lượng, deployment đưa app lên production.

### Testing:
- Cài Jest (cho JS) hoặc xUnit (.NET).
- Viết unit tests cho functions, integration tests cho API.
- Chạy `npm test` hoặc `dotnet test`.

### Deployment:
- Containerize với Docker (Dockerfile như trong essentials).
- Push code lên GitHub/GitLab: Tạo repo, `git init`, `git add .`, `git commit -m "Initial commit"`, `git push origin main`.
- Deploy lên Heroku: `heroku create`, `git push heroku main`.
- Hoặc dùng Vercel cho serverless, integrate với GitHub.

#### Containerization với Docker:
Docker là nền tảng container hóa cho phép đóng gói ứng dụng và dependencies vào container để chạy nhất quán trên mọi môi trường.

##### Khái Niệm Cơ Bản:
- **Image**: Template chỉ đọc chứa code, runtime, libraries.
- **Container**: Instance chạy của image.
- **Dockerfile**: Script để build image.

##### Lệnh Cơ Bản:
- `docker build -t myapp .`: Build image từ Dockerfile.
- `docker run -p 3000:3000 myapp`: Chạy container.
- `docker-compose up`: Chạy multi-container app.

##### Lợi Ích Cho Backend:
- Environment consistency (dev, staging, prod).
- Easy scaling và deployment.
- Isolation giữa services.

##### Ví Dụ Dockerfile Cho Node.js App:
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

#### Mục Tiêu: Code tested và app chạy online, code được lưu trên GitHub/GitLab.

## 12. Lộ Trình Học Backend

Hướng dẫn từng bước học Backend cho người mới bắt đầu. Lộ trình này giúp bạn nắm vững từ cơ bản đến nâng cao qua thực hành.

### Chuẩn Bị
**Công Cụ Cần Thiết:**
- **Ngôn Ngữ Lập Trình**: Chọn **JavaScript với Node.js** (dễ học, phổ biến) hoặc **C# với .NET** (enterprise, mạnh mẽ).
- **Editor**: VS Code với extensions: Prettier, ESLint, GitLens (cho JS); C# extension (cho .NET).
- **Tools**: Git, Postman, Docker.
- **Tài Khoản**: GitHub hoặc GitLab (free), Heroku/AWS (free tier).

**Hướng Dẫn Git Cơ Bản:**
Git giúp quản lý code và hợp tác. Cài đặt từ [git-scm.com](https://git-scm.com/), cấu hình user.name và user.email.
- Khởi tạo repo: `git init`
- Thêm file: `git add .` (hoặc `git add <file>` cho file cụ thể)
- Commit: `git commit -m "Initial commit"`
- Kiểm tra trạng thái: `git status`
- Xem lịch sử: `git log --oneline`
- Tạo repo trên GitHub/GitLab, liên kết: `git remote add origin <url>`
- Push: `git push -u origin main`
Để chi tiết hơn, xem phần "Hướng Dẫn Git và GitHub/GitLab" ở trên.

### Bước 1: Học Cơ Bản
Bắt đầu với nền tảng. Đọc Phần 1: Lý Thuyết Cơ Bản ở trên.
**Những Gì Cần Học:**
- HTTP: Methods, request/response, status codes, HTTPS.
- Client-Server Flow: Luồng request-response, các thành phần.
- JSON: Cấu trúc, parse/serialize.
- API: RESTful API, endpoints, versioning.
**Thực Hành:**
- Sử dụng Postman để test HTTP requests.
- Viết script gửi GET request (fetch trong JS hoặc HttpClient trong C#).
- Làm challenges liên quan trong `challenges/`.
**Mục Tiêu:** Hiểu cách client và server giao tiếp.

### Bước 2: Xây Dựng API Đơn Giản
Tạo API đầu tiên. Tham khảo Phần 2: Frameworks và Tools.
**Lựa Chọn Framework:** Node.js (dễ) hoặc .NET (enterprise).
**Với Node.js và Express.js:**
1. Cài Node.js/npm.
2. Tạo project: `npm init -y` và cài `express`.
3. Code cơ bản:
   ```javascript
   const express = require('express');
   const app = express();
   app.use(express.json());
   app.get('/api/hello', (req, res) => res.json({ message: 'Hello World!' }));
   app.listen(3000, () => console.log('Server running on port 3000'));
   ```
4. Chạy: `node app.js`.
5. Test với Postman.
**Với C# và ASP.NET Core:**
1. Cài .NET SDK.
2. Tạo project: `dotnet new webapi -n MyApi`.
3. Code:
   ```csharp
   var builder = WebApplication.CreateBuilder(args);
   var app = builder.Build();
   app.MapGet("/api/hello", () => new { message = "Hello World!" });
   app.Run();
   ```
4. Chạy: `dotnet run`.
**Mục Tiêu:** Xây dựng và test API cơ bản.

### Bước 3: Tích Hợp Database
Lưu dữ liệu persistent. Tham khảo Phần 2.
**Chọn Database:** MongoDB (NoSQL) hoặc PostgreSQL (SQL).
**Với Node.js:**
- MongoDB: Cài mongoose, tạo model, kết nối.
- PostgreSQL: Cài pg, tạo table, queries.
**Với .NET:** Sử dụng EF Core hoặc MongoDB.Driver.
**Mục Tiêu:** Lưu và truy xuất dữ liệu từ DB.

### Bước 4: Thêm Authentication
Bảo mật API. Tham khảo Phần 2.
**Với Node.js:** Cài bcryptjs, jsonwebtoken, tạo endpoints đăng ký/đăng nhập, middleware JWT.
**Với .NET:** Sử dụng JWT package.
**Mục Tiêu:** Bảo vệ API với JWT.

### Bước 5: Testing và Deployment
Đảm bảo ổn định và deploy. Tham khảo Phần 2: Testing và Deployment.
**Mục Tiêu:** Code tested, app online, code trên GitHub/GitLab.

## 13. Challenges và Bài Tập

Để thực hành kiến thức, tham khảo các bài tập trong repo:
- Xem danh sách tổng quan trong `table-of-contents.md`.
- Chi tiết từng challenge trong thư mục `challenges/` (từ challenge-1.md đến challenge-20.md).
- Mỗi challenge có mô tả, yêu cầu, dữ liệu mẫu và hướng dẫn giải quyết.
- Bắt đầu từ challenge cơ bản, làm tuần tự để củng cố lý thuyết.

## 15. Bộ Bài Tập Tư Duy Backend và Dự Án Thực Tế

Xem chi tiết trong file `backend-thinking-exercises.md`.

## 16. Tóm Tắt và Kết Luận

## 14. Tài Nguyên Học Thêm

### Trong Repo Này:
- `table-of-contents.md`: Danh sách challenges.
- `challenges/`: Bài tập thực hành (challenge-1.md đến challenge-20.md).
- `node/`: `node-express-guide.md` – Hướng dẫn chi tiết Node.js, Express.js, OOP, Database, Testing, Projects.
- `dotnet/`: `dotnet-aspnet-guide.md` – Hướng dẫn tương tự cho .NET, ASP.NET Core.
- `sql/`: `sql-queries-types.md` – Cơ bản SQL, các loại truy vấn, bài tập.

### Bên Ngoài Repo:
- **Sách**: "Node.js Design Patterns", "RESTful Web APIs", "Pro ASP.NET Core".
- **Courses**: freeCodeCamp (JS), Udemy (Backend Masterclass), Microsoft Learn (.NET).
- **Docs**: MDN Web Docs, Express.js docs, learn.microsoft.com/dotnet.
- **Communities**: Stack Overflow, Reddit r/learnprogramming.
- **Projects**: Clone app như Todo List, Blog. Sử dụng challenges để bắt đầu.

### Phương Pháp Học:
- Học bằng thực hành: Code mỗi ngày.
- Xây dựng dự án nhỏ để áp dụng lý thuyết.
- Đọc tài liệu chính thức.
- Sử dụng GitHub/GitLab để lưu code, collaborate.
- Thực hành liên tục: Xây dựng 3-5 projects nhỏ.
- Debugging: Học đọc error messages.
- Scalability: Nghĩ về performance sớm.
- Networking: Kết nối cộng đồng dev.