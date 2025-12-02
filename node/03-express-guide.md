# Hướng Dẫn Express.js Cho Người Học Backend: Framework Web Chuyên Sâu

## Giới Thiệu: Express.js Trong Series Học Backend
Xin chào! Trong phần "Phía Sau Website", chúng ta biết Express.js là framework đơn giản hóa Node.js, cung cấp routing và middleware để xây web apps nhanh. Phần 01 so sánh Node.js với .NET, nhấn mạnh Node.js phù hợp real-time và APIs. Phần 02 học Node.js thuần: modules, HTTP servers, async programming. Giờ, chúng ta áp dụng kiến thức đó vào Express.js: Học cách xây APIs chuyên nghiệp, xử lý middleware, routing, và nâng cao như auth, templates. Đây là bước thực hành cho backend devs, từ Node thuần sang framework hiệu quả.

### Tại Sao Học Express Chuyên Sâu?
- **Đơn giản hóa Node.js**: Thay code HTTP phức tạp bằng routing/middleware dễ.
- **Xây APIs nhanh**: RESTful APIs cho apps modern.
- **Mở rộng kiến thức**: Từ phần 02, giờ thêm abstraction.
- **Ví dụ vui**: Như từ lái xe tay sang tự động – vẫn lái, nhưng tiện hơn!

### Khi Nào Dùng Express?
- REST APIs, web apps.
- Prototyping nhanh.
- Microservices với Node.js.

## Mục Lục
- [Giới Thiệu: Express.js Là Gì?](#giới-thiệu-expressjs-là-gì)
- [Phần 1: Cơ Bản - Setup, Routing, Middleware](#phần-1-cơ-bản---setup-routing-middleware)
- [Phần 2: Middleware - Xử Lý Requests](#phần-2-middleware---xử-lý-requests)
- [Phần 3: Routing - Quản Lý Đường Dẫn](#phần-3-routing---quản-lý-đường-dẫn)
- [Phần 4: CRUD Operations - Tạo, Đọc, Sửa, Xóa](#phần-4-crud-operations---tạo-đọc-sửa-xóa)
- [Phần 5: Error Handling - Xử Lý Lỗi](#phần-5-error-handling---xử-lý-lỗi)
- [Phần 6: Nâng Cao - Authentication, Sessions, Templates](#phần-6-nâng-cao---authentication-sessions-templates)
- [Phần 7: API Documentation với Swagger/OpenAPI](#phần-7-api-documentation-với-swaggeropenapi)
- [Phần 8: Alternatives to Express - Nếu Không Dùng Express](#phần-8-alternatives-to-express---nếu-không-dùng-express)
- [Lưu Ý Cho Người Mới Học Express](#lưu-ý-cho-người-mới-học-express)
- [Tổng Kết](#tổng-kết)

## Phần 1: Cơ Bản - Setup, Routing, Middleware

### Setup: Cài Đặt Và Chạy
Express như setup workshop: Dễ dàng. Dùng package managers như npm, pnpm, yarn để quản lý.

#### Package.json Và Scripts
File định nghĩa project, dependencies, scripts.
```json
{
  "name": "express-app",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0"
  }
}
```
- **Package-lock.json**: Lock versions, tạo tự động.
- **Node_modules**: Folder chứa installed packages.

#### .env Và Environment Variables
Lưu config như port, secrets.
```javascript
require('dotenv').config();
const port = process.env.PORT || 3000;
```
- **Ví dụ**: PORT=3000, DB_URL=...

#### Nodemon: Auto-Restart
Cài `npm install -D nodemon`, script "dev" để restart khi thay đổi.

#### VS Code Extensions
- **Express.js Extension**: IntelliSense.
- **REST Client**: Test APIs.

#### Ví Dụ: Hello World App
- **Cài đặt**:
  ```bash
  npm init -y
  npm install express dotenv
  npm install -D nodemon
  ```

- **Tạo server**:
  ```javascript
  require('dotenv').config();
  const express = require('express');
  const app = express();
  const port = process.env.PORT || 3000;

  app.get('/', (req, res) => {
    res.send('Hello World!');
  });

  app.listen(port, () => console.log(`Server on ${port}`));
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Init project**: npm init -y, install express.
2. **Scripts**: Thêm "start", "dev" vào package.json.
3. **.env**: Tạo file, set PORT=3000.
4. **Nodemon**: Cài và dùng script dev.
5. **Package-lock**: Xem sau install.
6. **Node_modules**: List contents.
7. **VS Code**: Cài extensions.
8. **Basic route**: GET /hello.
9. **Multiple routes**: /users, /posts.
10. **Run dev**: npm run dev, test routes.

## Phần 2: Middleware - Xử Lý Requests

### Middleware Là Gì?
Middleware như "trạm kiểm soát": Chạy giữa request và response.

#### Ví Dụ: Logger Và Auth
- **Logger**:
  ```javascript
  app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
  });
  ```

- **JSON parser**:
  ```javascript
  app.use(express.json());
  ```

#### Bài Tập Thực Hành
1. **Custom middleware**: Log requests.
2. **Body parser**: express.json().
3. **CORS**: npm install cors.
4. **Helmet**: Security headers.
5. **Morgan**: HTTP logger.
6. **Auth middleware**: Check token.
7. **Error middleware**: (err, req, res, next).
8. **Route middleware**: Apply to specific routes.
9. **Third-party**: Compression, rate limiting.
10. **Custom error**: Throw errors.

## Phần 3: Routing - Quản Lý Đường Dẫn

### Routing Là Gì?
Routing như "bản đồ": Định tuyến requests đến handlers.

#### Ví Dụ: API Routes
- **Basic routing**:
  ```javascript
  app.get('/api/users', (req, res) => {
    res.json([{ id: 1, name: 'Alice' }]);
  });
  ```

- **Router module**:
  ```javascript
  const router = express.Router();
  router.get('/', getUsers);
  app.use('/api/users', router);
  ```

#### Bài Tập Thực Hành
1. **Route params**: /users/:id.
2. **Query params**: req.query.
3. **Body data**: req.body.
4. **Headers**: req.headers.
5. **Router separation**: userRoutes.js.
6. **Nested routes**: /users/:id/posts.
7. **Route groups**: app.route('/users').
8. **Wildcard**: /files/*.
9. **Regex routes**: /users/:id(\d+).
10. **Mounting**: app.use('/api/v1', apiRouter).

## Phần 4: CRUD Operations - Tạo, Đọc, Sửa, Xóa

### CRUD Là Gì?
CRUD như quản lý database: Create, Read, Update, Delete.

#### Ví Dụ: User Management
- **Create**:
  ```javascript
  app.post('/users', (req, res) => {
    const user = { id: Date.now(), ...req.body };
    users.push(user);
    res.status(201).json(user);
  });
  ```

- **Read**:
  ```javascript
  app.get('/users/:id', (req, res) => {
    const user = users.find(u => u.id == req.params.id);
    res.json(user);
  });
  ```

#### Bài Tập Thực Hành
1. **Create user**: POST /users.
2. **Read all**: GET /users.
3. **Read one**: GET /users/:id.
4. **Update**: PUT /users/:id.
5. **Delete**: DELETE /users/:id.
6. **Validation**: Check required fields.
7. **In-memory DB**: Array for users.
8. **Status codes**: 200, 201, 404, 400.
9. **Error responses**: { error: 'User not found' }.
10. **Pagination**: /users?page=1&limit=10.

## Phần 5: Error Handling - Xử Lý Lỗi

### Error Handling Là Gì?
Error handling như "bảo hiểm": Đảm bảo app không crash.

#### Ví Dụ: Safe API
- **Async errors**:
  ```javascript
  app.get('/users/:id', async (req, res, next) => {
    try {
      const user = await getUser(req.params.id);
      res.json(user);
    } catch (err) {
      next(err);
    }
  });
  ```

- **Global handler**:
  ```javascript
  app.use((err, req, res, next) => {
    res.status(500).json({ error: err.message });
  });
  ```

#### Bài Tập Thực Hành
1. **Sync errors**: Throw in route.
2. **Async errors**: try/catch.
3. **Custom errors**: class ValidationError.
4. **404 handler**: app.use((req, res) => res.status(404).send('Not Found')).
5. **Global error**: Catch all errors.
6. **Logging errors**: console.error.
7. **Client errors**: 400 for bad input.
8. **Server errors**: 500 for internal.
9. **Validation**: Joi or express-validator.
10. **Testing errors**: Supertest for routes.

## Phần 6: Nâng Cao - Authentication, Sessions, Templates

### Authentication: Xác Thực Người Dùng
Auth như "chìa khóa": Bảo vệ routes.

#### Sessions: Quản Lý Trạng Thái
Sessions như "phiếu ghi nhớ".

#### Templates: Render HTML
Templates như "mẫu": Pug, EJS.

#### Bài Tập Thực Hành
1. **JWT auth**: npm install jsonwebtoken.
2. **Login route**: POST /login.
3. **Protect routes**: Middleware check token.
4. **Sessions**: express-session.
5. **Cookies**: res.cookie.
6. **EJS templates**: app.set('view engine', 'ejs').
7. **Render views**: res.render('index').
8. **Partials**: Include header/footer.
9. **Static auth**: Hardcoded users.
10. **Logout**: Clear session/token.

## Phần 7: API Documentation với Swagger/OpenAPI

### Tại Sao Cần API Documentation?
API documentation như "sách hướng dẫn": Giúp frontend devs, clients hiểu cách dùng API. Swagger/OpenAPI là standard phổ biến, tạo docs interactive.

#### Swagger/OpenAPI Là Gì?
- **OpenAPI**: Specification để describe REST APIs.
- **Swagger**: Tools implement OpenAPI (Swagger UI, Swagger Editor).

#### Cài Đặt Và Setup
- **Cài đặt**: `npm install swagger-jsdoc swagger-ui-express`
- **Setup**:
  ```javascript
  const swaggerJsdoc = require('swagger-jsdoc');
  const swaggerUi = require('swagger-ui-express');

  const options = {
    definition: {
      openapi: '3.0.0',
      info: {
        title: 'Express API',
        version: '1.0.0',
      },
    },
    apis: ['./routes/*.js'], // Paths to files with annotations
  };

  const specs = swaggerJsdoc(options);
  app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(specs));
  ```

#### Documenting Routes
Dùng JSDoc comments để describe endpoints.

- **Ví dụ**:
  ```javascript
  /**
   * @swagger
   * /users:
   *   get:
   *     summary: Get all users
   *     responses:
   *       200:
   *         description: List of users
   *         content:
   *           application/json:
   *             schema:
   *               type: array
   *               items:
   *                 type: object
   *                 properties:
   *                   id:
   *                     type: integer
   *                   name:
   *                     type: string
   */
  app.get('/users', (req, res) => {
    res.json(users);
  });
  ```

#### Bài Tập Thực Hành
1. **Setup Swagger**: Cài đặt, serve tại /api-docs.
2. **Document GET /users**: Thêm JSDoc comment.
3. **Document POST /users**: Với request body schema.
4. **Schemas**: Define User schema.
5. **Responses**: 200, 404, 400.
6. **Auth**: Document Bearer token.
7. **Parameters**: Path params, query params.
8. **Tags**: Group endpoints.
9. **Examples**: Request/response examples.
10. **Test docs**: Truy cập /api-docs, test endpoints.

## Phần 8: Alternatives to Express - Nếu Không Dùng Express

### Quan Hệ Giữa Node.js Và Express
Node.js là "trái tim" - runtime JavaScript cho server, cung cấp core modules như `http`, `fs`, `events`. Express là framework "áo khoác" - built on top of Node's `http` module, cung cấp abstractions như routing, middleware để dễ code hơn. Không có Express, bạn vẫn dùng Node thuần, nhưng Express làm mọi thứ nhanh và tiện hơn.

**Ví dụ vui**: Node.js như động cơ xe, Express như thân xe - động cơ chạy được, nhưng thân xe làm xe hoàn chỉnh!

### Tại Sao Cần Alternatives?
Express tốt cho beginners, nhưng có thể chậm cho high-performance apps, hoặc thiếu features advanced. Alternatives cung cấp performance cao hơn, built-in features, hoặc syntax modern.

### Các Alternatives Phổ Biến

#### 1. Vanilla Node.js (Thuần Node)
- **Là gì?**: Dùng trực tiếp `http` module của Node.js.
- **Ưu điểm**: Không dependencies, lightweight, full control.
- **Nhược điểm**: Verbose, phải tự code routing, parsing.
- **Khi nào dùng**: Small apps, learning purposes, hoặc khi cần tối ưu max.
- **Ví dụ**:
  ```javascript
  const http = require('http');
  const server = http.createServer((req, res) => {
    if (req.url === '/api/users') {
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify([{ id: 1, name: 'Alice' }]));
    } else {
      res.writeHead(404);
      res.end('Not Found');
    }
  });
  server.listen(3000);
  ```

#### 2. Koa.js
- **Là gì?**: Framework minimal, modern, dùng async/await native.
- **Ưu điểm**: Lightweight, async-first, extensible với koa-* packages.
- **Nhược điểm**: Ít built-in features hơn Express.
- **Khi nào dùng**: Apps cần async/await clean, hoặc muốn minimal framework.
- **Ví dụ**:
  ```javascript
  const Koa = require('koa');
  const app = new Koa();
  app.use(async (ctx) => {
    ctx.body = 'Hello Koa';
  });
  app.listen(3000);
  ```

#### 3. Fastify
- **Là gì?**: Framework high-performance, JSON schema validation built-in.
- **Ưu điểm**: Rất nhanh (nhanh hơn Express 2-3x), low overhead, great for APIs.
- **Nhược điểm**: Learning curve cao hơn, ecosystem nhỏ hơn Express.
- **Khi nào dùng**: High-throughput APIs, microservices.
- **Ví dụ**:
  ```javascript
  const fastify = require('fastify')();
  fastify.get('/', async (request, reply) => {
    return { hello: 'world' };
  });
  fastify.listen(3000);
  ```

#### 4. Hapi.js
- **Là gì?**: Framework enterprise, configuration-driven.
- **Ưu điểm**: Robust, good for large teams, built-in caching, auth.
- **Nhược điểm**: Heavy, complex setup.
- **Khi nào dùng**: Enterprise apps, cần structure strict.
- **Ví dụ**:
  ```javascript
  const Hapi = require('@hapi/hapi');
  const server = Hapi.server({ port: 3000 });
  server.route({
    method: 'GET',
    path: '/',
    handler: (request, h) => {
      return 'Hello Hapi';
    }
  });
  server.start();
  ```

#### 5. Restify
- **Là gì?**: Framework cho REST APIs, inspired by Express.
- **Ưu điểm**: Tuned for APIs, built-in versioning, throttling.
- **Nhược điểm**: Ít dùng cho web apps, ecosystem nhỏ.
- **Khi nào dùng**: Pure REST APIs, microservices.

### So Sánh Alternatives

| Framework | Performance | Learning Curve | Features | Ecosystem | Best For |
|-----------|-------------|----------------|----------|-----------|----------|
| **Express** | Trung bình | Dễ | Routing, middleware | Lớn nhất | Beginners, general apps |
| **Vanilla Node** | Cao | Khó | Minimal | Core Node | Learning, small apps |
| **Koa** | Cao | Trung bình | Async/await | Trung bình | Modern apps, minimal |
| **Fastify** | Rất cao | Trung bình | Validation, speed | Nhỏ | High-performance APIs |
| **Hapi** | Trung bình | Khó | Enterprise features | Trung bình | Large teams, enterprise |
| **Restify** | Cao | Trung bình | REST-focused | Nhỏ | REST APIs |

### Khi Nào Chọn Alternative?
- **Dùng Vanilla Node**: Học Node internals, hoặc apps siêu nhỏ.
- **Dùng Koa**: Nếu thích async/await, muốn lightweight.
- **Dùng Fastify**: Nếu cần speed max, JSON APIs.
- **Dùng Hapi/Restify**: Nếu enterprise, cần built-in security/auth.
- **Giữ Express**: Nếu beginner, hoặc ecosystem lớn.

#### Bài Tập Thực Hành
1. **Vanilla Node server**: Tạo server với http module, handle /users route.
2. **Koa app**: Install koa, tạo route với async.
3. **Fastify API**: Tạo GET /hello, measure response time.
4. **Compare performance**: Benchmark Express vs Fastify với load test.
5. **Migrate from Express**: Chuyển simple Express app sang Koa.
6. **Hapi route**: Tạo route với validation.
7. **Restify API**: Tạo REST endpoint.
8. **Hybrid**: Dùng Express cho web, Fastify cho APIs.
9. **Custom framework**: Build mini-framework on Node http.
10. **Choose one**: Pick alternative, build small app.

## Lưu Ý Cho Người Mới Học Express
- **Bắt đầu với basics**: Routing, middleware.
- **Thử với Postman**: Test APIs.
- **Practive với projects**: Build simple blog API.
- **Đọc docs vui**: [Express docs](https://expressjs.com/) có examples.
- **Lỗi thường gặp**: Forget next() in middleware.

## Tổng Kết: Kết Thúc Series Node.js, Bước Sang Học Tiếp
Trong series Node.js này, chúng ta đã học từ cơ bản websites (00-how-websites-work.md), so sánh Node.js với .NET (01-node-vs-other-backends.md), Node.js thuần (02-node-basics-guide.md), đến Express.js (03-express-guide.md). Bạn giờ master xây APIs với Node.js: Từ HTTP servers thuần, routing/middleware, CRUD, auth, đến alternatives. Thực hành bài tập để củng cố!

Tiếp theo, học SQL để kết nối databases (series SQL), hoặc thử challenges để áp dụng kiến thức thực tế. Express như công cụ backend mạnh mẽ – giờ bạn sẵn sàng xây apps chuyên nghiệp. Chúc học vui, và hẹn gặp ở phần tiếp theo!</content>
<parameter name="filePath">d:\WorkSpace\Books\Pre-Backend-Challenges\node\03-express-guide.md