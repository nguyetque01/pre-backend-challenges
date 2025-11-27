# Hướng Dẫn Học Backend Cho Người Mới Bắt Đầu

Chào mừng bạn đến với hành trình học Backend! Tài liệu này cung cấp lộ trình từng bước để bạn nắm vững các khái niệm cơ bản và xây dựng kỹ năng thực tế. Giả sử bạn đã biết cơ bản về lập trình (như JavaScript hoặc C#).

## Mục Lục
1. [Chuẩn Bị](#1-chuẩn-bị)
2. [Bước 1: Học Cơ Bản](#2-bước-1-học-cơ-bản)
3. [Bước 2: Xây Dựng API Đơn Giản](#3-bước-2-xây-dựng-api-đơn-giản)
4. [Bước 3: Tích Hợp Database](#4-bước-3-tích-hợp-database)
5. [Bước 4: Thêm Authentication](#5-bước-4-thêm-authentication)
6. [Bước 5: Testing và Deployment](#6-bước-5-testing-và-deployment)
7. [Tài Nguyên Học Thêm](#7-tài-nguyên-học-thêm)
8. [Lời Khuyên Cuối Cùng](#8-lời-khuyên-cuối-cùng)

## 1. Chuẩn Bị

### Công Cụ Cần Thiết:
- **Ngôn Ngữ Lập Trình**: Chọn **JavaScript với Node.js** (dễ học, phổ biến) hoặc **C# với .NET** (enterprise, mạnh mẽ). Hướng dẫn tập trung vào cả hai.
- **Editor**: VS Code với extensions: Prettier, ESLint, GitLens (cho JS); C# extension (cho .NET).
- **Tools**: Git, Postman, Docker.
- **Tài Khoản**: **GitHub** hoặc **GitLab** (free), Heroku/AWS (free tier).

### Tư Duy:
- Học bằng thực hành: Code mỗi ngày.
- Xây dựng dự án nhỏ để áp dụng lý thuyết.
- Đọc tài liệu chính thức, không chỉ tutorial.
- Sử dụng GitHub/GitLab để lưu code, collaborate và showcase projects.

### Hướng Dẫn Git Cơ Bản:
Git giúp quản lý code và hợp tác. Cài đặt từ [git-scm.com](https://git-scm.com/), cấu hình user.name và user.email.

- Khởi tạo repo: `git init`
- Thêm file: `git add .` (hoặc `git add <file>` cho file cụ thể)
- Commit: `git commit -m "Initial commit"`
- Kiểm tra trạng thái: `git status`
- Xem lịch sử: `git log --oneline`
- Tạo repo trên GitHub/GitLab, liên kết: `git remote add origin <url>`
- Push: `git push -u origin main`

Để học chi tiết hơn về branching, merge, conflicts, xem phần "Hướng Dẫn Git và GitHub/GitLab" trong `backend-book.md`.

## 2. Bước 1: Học Cơ Bản

Bắt đầu với nền tảng. Đọc và hiểu các khái niệm trong `backend-essentials.md` (trong repo này).

### Những Gì Cần Học:
- **HTTP**: Methods, request/response, status codes, HTTPS.
- **Client-Server Flow**: Luồng request-response, các thành phần (client, web server, app server, database).
- **JSON**: Cấu trúc, parse/serialize.
- **API**: RESTful API, endpoints, versioning.

### Thực Hành:
- Sử dụng Postman để test HTTP requests.
- Viết script đơn giản gửi GET request và log response (sử dụng fetch trong JS hoặc HttpClient trong C#).
- Tham khảo `table-of-contents.md` để xem danh sách challenges và chọn bài tập liên quan.

### Mục Tiêu: Hiểu cách client và server giao tiếp.

## 3. Bước 2: Xây Dựng API Đơn Giản

Tạo API đầu tiên để áp dụng HTTP và JSON. Tham khảo `node/node-express-guide.md` trong repo cho hướng dẫn Express.js.

### Lựa Chọn Framework:
Bạn có thể chọn Node.js (dễ học) hoặc .NET (enterprise). Hướng dẫn dưới đây cung cấp song song cho cả hai.

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
- Tham khảo challenges trong `challenges/` để làm bài tập thực tế, như challenge-1.md.

### Với C# và ASP.NET Core

#### Công Cụ:
- .NET SDK + ASP.NET Core.

#### Các Bước:
1. Cài .NET SDK (free từ Microsoft).
2. Tạo project: `dotnet new webapi -n MyApi`.
3. Viết code cơ bản trong `Program.cs` hoặc `Controllers/WeatherForecastController.cs`:
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

### Mục Tiêu Chung: Xây dựng và test API cơ bản với framework đã chọn.

## 4. Bước 3: Tích Hợp Database

Lưu dữ liệu persistent thay vì array. Tham khảo `sql/sql-queries-types.md` trong repo cho SQL basics.

### Chọn Database:
- **MongoDB** (NoSQL): Linh hoạt, dễ scale, phù hợp cho dữ liệu không cấu trúc. Dùng với Node.js qua mongoose.
- **PostgreSQL** (SQL): Mạnh mẽ, ACID compliant, phù hợp cho dữ liệu quan hệ. Dùng với pg library hoặc EF Core cho .NET.
- **SQL Server**: Tương tự PostgreSQL, nhưng của Microsoft, dùng nếu làm .NET.

Bắt đầu với MongoDB cho dễ, hoặc PostgreSQL nếu muốn học SQL.

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

### Học Thêm: SQL queries nếu dùng PostgreSQL/SQL Server. Làm challenges liên quan DB trong `challenges/`.

### Mục Tiêu Chung: Lưu và truy xuất dữ liệu từ DB.

## 5. Bước 4: Thêm Authentication

Bảo mật API. Tham khảo phần Authentication trong `backend-essentials.md`.

### Với Node.js

#### Các Bước:
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

#### Các Bước:
- Sử dụng JWT: `dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer`.
- Tạo endpoints đăng ký/đăng nhập, middleware verify token.

### Mục Tiêu Chung: Bảo vệ API với JWT. Làm challenges về auth nếu có.

## 6. Bước 5: Testing và Deployment

Đảm bảo code ổn định và deploy lên production. Tham khảo phần Docker trong `backend-essentials.md`.

### Testing:
- **Node.js**: Cài Jest, viết unit tests.
- **.NET**: xUnit hoặc NUnit.
- Chạy `npm test` hoặc `dotnet test`.

### Deployment:
- Containerize với Docker (Dockerfile như trong essentials).
- **Push code lên GitHub/GitLab**: Tạo repo, `git init`, `git add .`, `git commit -m "Initial commit"`, `git push origin main`.
- Deploy lên Heroku: `heroku create`, `git push heroku main`.
- Hoặc dùng Vercel cho serverless, integrate với GitHub.

### Mục Tiêu: Code tested và app chạy online, code được lưu trên GitHub/GitLab. Hoàn thành một số challenges để thực hành full flow.

## 7. Tài Nguyên Học Thêm

- **Trong Repo Này**: `backend-essentials.md` (cơ bản), `table-of-contents.md` (danh sách challenges), `challenges/` (bài tập thực hành), `node/` (cho JS), `dotnet/` (cho .NET), `sql/` (hướng dẫn chuyên sâu).
- **Sách**: "Node.js Design Patterns", "RESTful Web APIs", "Pro ASP.NET Core".
- **Courses**: freeCodeCamp (JS), Udemy (Backend Masterclass), Microsoft Learn (.NET).
- **Docs**: MDN Web Docs, Express.js docs, learn.microsoft.com/dotnet.
- **Communities**: Stack Overflow, Reddit r/learnprogramming.
- **Projects**: Clone app như Todo List, Blog. Sử dụng challenges trong repo để bắt đầu.

## 8. Lời Khuyên Cuối Cùng

- **Thực Hành Liên Tục**: Xây dựng 3-5 projects nhỏ.
- **Debugging**: Học cách đọc error messages.
- **Scalability**: Nghĩ về performance sớm.
- **Networking**: Kết nối với cộng đồng dev.
- **Tự Tin**: Lỗi là bình thường, học từ đó.

Chúc bạn thành công trên con đường trở thành Backend Developer! Nếu gặp khó khăn, quay lại `backend-essentials.md` để ôn tập, và làm challenges trong `challenges/` để thực hành.