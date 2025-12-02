# Hướng Dẫn Node.js Cơ Bản Cho Người Học Backend: Runtime JavaScript Chuyên Sâu

## Giới Thiệu: Node.js Trong Series Học Backend
Chào bạn! Trong phần trước "Phía Sau Website", chúng ta đã khám phá cách website hoạt động, vai trò của JavaScript (JS) và Node.js trong mô hình client-server. Bạn đã hiểu Node.js như một "cầu nối" giúp JS chạy trên server, với event loop xử lý requests nhanh chóng nhờ non-blocking I/O. Phần 01 so sánh Node.js với .NET và các backend khác, nhấn mạnh Node.js mạnh cho I/O và real-time, phù hợp startups và APIs. Bây giờ, chúng ta sẽ đi sâu vào Node.js: Học cách xây dựng servers, xử lý async, và tối ưu performance. Đây là bước chuyên sâu cho người học backend, từ lý thuyết sang thực hành.

### Tại Sao Học Node.js Chuyên Sâu?
- **Nền tảng backend**: Xây servers, APIs mà không cần framework phức tạp.
- **Hiểu async programming**: Cơ chế non-blocking làm Node.js khác biệt.
- **Chuẩn bị Express**: Phần 03 sẽ dùng kiến thức này để học framework.
- **Ví dụ vui**: Như học lái xe tay lái trước khi dùng tự động!

### Khi Nào Dùng Node.js Thuần?
- Prototypes, microservices nhỏ.
- Apps cần custom logic (không framework).
- Học để hiểu backend sâu.

## Mục Lục
- [Giới Thiệu: Node.js Trong Series Học Backend](#giới-thiệu-nodejs-trong-series-học-backend)
- [Phần 1: Setup Project Node.js - Tools Và Dependencies](#phần-1-setup-project-nodejs---tools-và-dependencies)
- [Phần 2: Cấu Trúc Dự Án Node.js - Tổ Chức Code](#phần-2-cấu-trúc-dự-án-nodejs---tổ-chức-code)
- [Phần 3: Cơ Bản - Modules, File System, HTTP](#phần-3-cơ-bản---modules-file-system-http)
- [Phần 4: File System - Đọc/Ghi Files](#phần-4-file-system---đọcghi-files)
- [Phần 5: HTTP Server - Xây Dựng Web Server](#phần-5-http-server---xây-dựng-web-server)
- [Phần 6: Asynchronous Programming - Callbacks, Promises, Async/Await](#phần-6-asynchronous-programming---callbacks-promises-asyncawait)
- [Phần 7: Events - Event-Driven Programming](#phần-7-events---event-driven-programming)
- [Phần 8: Nâng Cao - Buffers, Streams, Child Processes](#phần-8-nâng-cao---buffers-streams-child-processes)
- [Lưu Ý Cho Người Mới Học Node.js](#lưu-ý-cho-người-mới-học-nodejs)
- [Tổng Kết](#tổng-kết)

## Phần 1: Setup Project Node.js - Tools Và Dependencies
Trước khi bắt đầu code Node.js, việc setup project đúng cách là nền tảng cho phát triển hiệu quả. Phần này sẽ hướng dẫn chi tiết các công cụ, file cấu hình, và best practices để quản lý dependencies, scripts, và môi trường. Chúng ta sẽ khám phá vai trò của từng thành phần, tại sao chúng quan trọng, và cách sử dụng chúng trong thực tế.

### Tại Sao Setup Quan Trọng?
Setup tốt giúp:
- **Quản lý dependencies**: Dễ dàng thêm, cập nhật packages.
- **Tái tạo môi trường**: Mọi dev có setup giống nhau.
- **Tự động hóa tasks**: Scripts để chạy, test, build.
- **Bảo mật**: Ẩn secrets với .env.
- **Hiệu quả phát triển**: Tools như nodemon, extensions tăng tốc.

### Package Managers: npm, pnpm, yarn
Package managers là công cụ giúp bạn tải và quản lý "thư viện" (packages) cho Node.js. Như đi siêu thị mua nguyên liệu nấu ăn – bạn chọn, tải về, và dùng trong code. Có 3 phổ biến: npm (mặc định), pnpm, yarn. Ngoài ra, còn nvm để quản lý versions Node.js.

#### nvm (Node Version Manager)
nvm giúp bạn quản lý nhiều versions Node.js trên máy. Điều này hữu ích khi bạn cần switch giữa các versions khác nhau, ví dụ từ Node 16 lên 18 hoặc 20. Cách dùng đơn giản: Cài nvm, rồi chạy `nvm install 18`, `nvm use 18`. Ví dụ, `nvm install node` để cài latest, `nvm list` để xem versions có sẵn.

#### So Sánh Package Managers

| Manager | Vai Trò | Ưu Điểm | Nhược Điểm | Khi Nào Dùng? | Ví Dụ |
|---------|---------|----------|------------|---------------|-------|
| **npm** | Mặc định với Node.js, phổ biến nhất. | Hỗ trợ rộng, tích hợp sẵn, dễ dùng. | Chậm với nhiều packages, disk usage cao. | Beginners, projects đơn giản. | `npm install express` |
| **pnpm** | Hiệu quả, tiết kiệm disk. | Nhanh, dùng hard links chia sẻ code, ít space. | Ít phổ biến, setup phức tạp hơn. | Teams cần tiết kiệm disk, performance. | `pnpm install lodash` |
| **yarn** | Nhanh, reliable. | Offline install, deterministic (yarn.lock). | Cần cài riêng, ecosystem nhỏ hơn npm. | Enterprises, cần speed và consistency. | `yarn add axios` |

Cách chọn: Bắt đầu với npm vì nó dễ. Nếu thấy chậm, thử pnpm hoặc yarn. Đừng quên dùng nvm để quản lý versions Node.js.

### Scripts Trong Package.json
Scripts là cách để tự động hóa các tasks. Bạn định nghĩa chúng trong object "scripts" của package.json. Ví dụ cơ bản:

```json
"scripts": {
  "start": "node server.js",  // Chạy app production
  "dev": "nodemon server.js", // Dev với auto-restart
  "test": "jest",             // Chạy tests
  "build": "webpack",         // Build app
  "lint": "eslint .",         // Check code quality
  "clean": "rm -rf node_modules && npm install" // Clean và reinstall
}
```

Chạy bằng `npm run dev` (hoặc `npm start` cho start). Scripts giúp bạn không phải gõ dài dòng mỗi lần.

### Package.json: Cấu Trúc Project
File JSON này định nghĩa metadata và cấu hình project. Nó như "bản đồ" của project, liệt kê dependencies, scripts, v.v. Các phần chính:
- `name`: Tên project.
- `version`: Phiên bản (theo semantic versioning).
- `scripts`: Commands như "start", "test".
- `dependencies`: Packages cần cho runtime.
- `devDependencies`: Packages chỉ dùng khi dev (như nodemon).

Ví dụ:
```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "description": "Simple Node.js app",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0",
    "dotenv": "^16.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.20",
    "jest": "^29.0.0"
  },
  "keywords": ["node", "express"],
  "author": "Your Name",
  "license": "MIT"
}
```

Tạo bằng `npm init` (interactive) hoặc `npm init -y` (mặc định).

### Package-lock.json: Lock Dependencies
File này tự động tạo khi install packages. Nó "khóa" versions chính xác để đảm bảo mọi máy install giống nhau, tránh conflicts. Lưu exact versions và checksums. npm dùng package-lock.json, yarn dùng yarn.lock. Hãy commit file này để consistency.

### Node_modules: Folder Dependencies
Folder này chứa code của các packages đã install. Nó như "kho" lưu source code để require. Cấu trúc tree, có thể lớn, nên đừng commit (add vào .gitignore). Ví dụ, sau `npm install express`, node_modules/express chứa code.

### .env: Environment Variables
File text này lưu config và secrets. Nó giúp tách riêng khỏi code, và khác nhau per environment. Dùng key-value pairs, load bằng dotenv.

Ví dụ:
```
PORT=3000
DB_URL=mongodb://localhost:27017/myapp
SECRET_KEY=your-secret
```

Sử dụng:
```javascript
require('dotenv').config();
const port = process.env.PORT || 3000;
```

Lưu ý: Add .env vào .gitignore, dùng .env.example làm template.

### Port: Cấu Hình Server
Port như "cửa sổ" mà server "nghe" requests từ clients. Giống như số nhà, port giúp máy tính biết gửi data đến đâu. Port là số từ 0-65535, 0-1023 reserved (như 80 cho HTTP, 443 HTTPS). Localhost ("127.0.0.1" hoặc "localhost") là địa chỉ máy bạn, dùng khi server chạy local. Dev dùng port cao như 3000, 5000 để tránh conflict. Production, hosting như Heroku tự set PORT env var, bạn dùng process.env.PORT.

Ví dụ:
```javascript
const port = process.env.PORT || 3000; // Prod dùng env, dev dùng 3000
server.listen(port, () => console.log(`Server running on http://localhost:${port}`));
```

Khi deploy, hosting set PORT (ví dụ 8080), code adapt tự động. Đừng hardcode port. Test bằng mở browser gõ http://localhost:3000.

### Nodemon: Auto-Restart Server
Tool này restart app khi file thay đổi. Tăng tốc dev, không restart manual. Watch files, restart process. Cài `npm install -D nodemon`, script "dev": "nodemon server.js".

### VS Code Extensions Gợi Ý
Extensions cải thiện trải nghiệm dev:
- **Node.js Extension Pack**: IntelliSense, debug, snippets.
- **Prettier**: Auto-format code.
- **ESLint**: Lint JS, catch errors.
- **Thunder Client**: Test APIs trong VS Code.
- **GitLens**: Git integration.

### Tools Hỗ Trợ: Git, Postman, VS Code

#### Git: Version Control
Git là hệ thống quản lý phiên bản phân tán, giúp theo dõi thay đổi code và hợp tác. GitHub/GitLab là nền tảng hosting repositories.

##### Cài Đặt và Cơ Bản:
- Download từ [git-scm.com](https://git-scm.com/), cấu hình: `git config --global user.name "Name"` và `git config --global user.email "email"`.
- Lệnh cơ bản: `git init`, `git add .`, `git commit -m "msg"`, `git status`, `git log --oneline`.

##### Làm Việc với Remote:
- Tạo repo trên GitHub/GitLab, liên kết: `git remote add origin <url>`.
- Push: `git push -u origin main`.
- Clone: `git clone <url>`.

##### Workflow Chi Tiết:
- **Branching**: `git branch feature/login`, `git checkout feature/login` (hoặc `git switch -c feature/login`).
- **Merging**: `git checkout main`, `git merge feature/login`.
- **Resolving Conflicts**: Edit files, `git add`, `git commit`.
- **Rebasing**: `git rebase main` để clean history.
- **Stashing**: `git stash` để tạm lưu changes, `git stash pop` để lấy lại.

##### Best Practices:
- Commit thường xuyên với message rõ ràng (e.g., "feat: add user login").
- Sử dụng branch cho features.
- Push lên remote để backup.
- Pull trước khi push: `git pull --rebase`.

##### Thực Hành Git:
1. **Init repo**: `git init`, tạo file README.md, `git add README.md`, `git commit -m "Initial commit"`.
2. **Branch workflow**: Tạo branch `git checkout -b feature/add-api`, thay đổi code, commit, merge vào main.
3. **Remote push**: Liên kết GitHub, `git push origin main`.
4. **Collaborate**: Clone repo, tạo PR trên GitHub.
5. **Resolve conflict**: Tạo conflict, fix và commit.

#### Postman: Test APIs
Postman là tool để test và develop APIs. Gửi requests, inspect responses, tạo collections.

##### Cài Đặt và Sử Dụng:
- Download từ [postman.com](https://www.postman.com/downloads/).
- Tạo request: Chọn method (GET/POST), nhập URL, gửi.
- Collections: Nhóm requests, share với team.
- Environments: Variables cho dev/prod.

##### Tính Năng Chi Tiết:
- **Variables**: Global, environment, collection variables (e.g., {{base_url}} = http://localhost:3000).
- **Tests**: JavaScript để test responses: `pm.test("Status code is 200", () => pm.response.to.have.status(200));`.
- **Pre-request Scripts**: Chạy trước request, set variables.
- **Authorization**: JWT, Basic Auth, OAuth.
- **Mock Servers**: Simulate APIs.
- **API Documentation**: Generate docs từ collections.

##### Ví Dụ:
- GET http://localhost:3000/api/users
- POST với body JSON: {"name": "Alice"}, headers Content-Type: application/json.

##### Thực Hành Postman:
1. **Basic request**: Tạo GET request đến API public (e.g., jsonplaceholder.typicode.com/users).
2. **Collection**: Tạo collection "User API", thêm requests GET, POST, PUT, DELETE.
3. **Environment**: Tạo env "Dev" với base_url = http://localhost:3000, "Prod" với URL production.
4. **Tests**: Thêm test kiểm tra status 200, response JSON.
5. **Variables**: Sử dụng {{user_id}} trong requests.
6. **Auth**: Set JWT token trong Authorization tab.
7. **Runner**: Chạy collection để test nhiều requests.
8. **Mock**: Tạo mock server cho API chưa có.

#### VS Code: Editor Phổ Biến
VS Code là editor miễn phí, mạnh mẽ cho Node.js dev.

##### Extensions Quan Trọng:
- Node.js Extension Pack (đã đề cập).
- Git Graph: Visualize Git history.
- Live Server: Serve static files.

##### Cấu Hình và Tính Năng:
- **Settings**: JSON settings (Ctrl+,), e.g., "editor.formatOnSave": true.
- **Debugging**: Launch.json cho Node.js: {"type": "node", "request": "launch", "program": "${workspaceFolder}/server.js"}.
- **Integrated Terminal**: Ctrl + `, chạy commands.
- **Git Integration**: Source control panel, diff, commit trực tiếp.
- **Snippets**: Tạo custom snippets cho Node.js code.
- **Tasks**: tasks.json để run scripts (e.g., npm run dev).

##### Tips:
- Integrated terminal: Ctrl + `.
- Debug: Set breakpoints, F5 to run.
- Extensions marketplace: Search và install.

##### Thực Hành VS Code:
1. **Setup workspace**: Mở folder project, cài extensions Node.js Pack, Prettier.
2. **Debug Node.js**: Tạo launch.json, set breakpoint trong server.js, F5 debug.
3. **Git in VS Code**: Source control panel, stage, commit, push.
4. **Terminal**: Chạy `npm install`, `node server.js`.
5. **Snippets**: Tạo snippet cho console.log (prefix: cl, body: console.log('$1');).
6. **Tasks**: Tạo task run npm dev, bind key.
7. **Format code**: Cài Prettier, format on save.
8. **Linting**: Cài ESLint, fix errors.

#### Bài Tập Setup Chi Tiết
1. **Khởi tạo project**: Chạy `npm init -y`, xem package.json. Thêm "description" và "author".
2. **Cài dependencies**: `npm install express dotenv`, xem node_modules. Thêm script "start": "node server.js".
3. **Dev dependencies**: `npm install -D nodemon jest`, xem devDependencies.
4. **Scripts nâng cao**: Thêm "build": "npm run lint && npm test", "lint": "eslint .".
5. **Package-lock**: Sau install, xem package-lock.json, note versions locked.
6. **.env setup**: Tạo .env với PORT=3000, DB_HOST=localhost. Cài dotenv, load trong code.
7. **Port config**: Viết server.js dùng process.env.PORT, test ports khác.
8. **Nodemon**: Thêm script "dev", chạy `npm run dev`, thay đổi file xem auto-restart.
9. **Compare managers**: Cài yarn/pnpm, so sánh speed install express.
10. **VS Code**: Cài Node.js Extension Pack, test IntelliSense cho require('express').
11. **.gitignore**: Tạo file, add node_modules, .env, *.log.
12. **Environment**: Tạo .env.production, load khác cho prod.
13. **Scripts complex**: Thêm "clean": "rm -rf node_modules package-lock.json && npm install".
14. **Publish prep**: Thêm "main", "keywords", test `npm pack`.
15. **Debug setup**: Cài VS Code debugger, set breakpoints trong server.js.

## Phần 2: Cấu Trúc Dự Án Node.js - Tổ Chức Code

### Tại Sao Cần Cấu Trúc Dự Án?
Cấu trúc dự án như "bản đồ nhà": Giúp code dễ maintain, scale, và teamwork. Bad structure dẫn đến spaghetti code, khó debug. Good structure tách concerns, dùng patterns như MVC.

#### Nguyên Tắc Tổ Chức
- **Separation of Concerns**: Tách logic (routes, models, controllers).
- **Modularity**: Chia thành modules nhỏ.
- **Scalability**: Dễ thêm features.
- **Readability**: Code dễ hiểu, navigate.

### Cấu Trúc Cơ Bản Cho App Nhỏ
```
/my-node-app/
├── node_modules/          # Dependencies (ignore in git)
├── .env                   # Environment variables
├── .gitignore             # Files to ignore
├── package.json           # Project metadata
├── package-lock.json      # Locked dependencies
├── README.md              # Documentation
├── server.js              # Entry point
├── config/                # Config files
│   └── database.js
├── controllers/           # Business logic
│   └── userController.js
├── models/                # Data models
│   └── userModel.js
├── routes/                # API routes
│   └── userRoutes.js
├── middleware/            # Custom middleware
│   └── auth.js
├── utils/                 # Helper functions
│   └── helpers.js
└── tests/                 # Unit/integration tests
    └── user.test.js
```

#### Giải Thích Các Folder
- **config/**: Database connections, app settings.
- **controllers/**: Handle requests, call models.
- **models/**: Data structures, DB interactions.
- **routes/**: Define endpoints, map to controllers.
- **middleware/**: Auth, logging, validation.
- **utils/**: Reusable functions.
- **tests/**: Test files.

#### Ví Dụ: User API Với Cấu Trúc
- **models/userModel.js**:
  ```javascript
  const users = []; // Mock DB
  module.exports = {
    getAll: () => users,
    create: (user) => users.push(user),
  };
  ```

- **controllers/userController.js**:
  ```javascript
  const userModel = require('../models/userModel');
  exports.getUsers = (req, res) => {
    res.json(userModel.getAll());
  };
  ```

- **routes/userRoutes.js**:
  ```javascript
  const express = require('express');
  const router = express.Router();
  const userController = require('../controllers/userController');
  router.get('/', userController.getUsers);
  module.exports = router;
  ```

- **server.js**:
  ```javascript
  const express = require('express');
  const userRoutes = require('./routes/userRoutes');
  const app = express();
  app.use('/api/users', userRoutes);
  app.listen(3000);
  ```

#### Cấu Trúc Cho Apps Lớn: MVC Pattern
- **MVC**: Model-View-Controller.
  - **Model**: Data và logic.
  - **View**: Templates (cho web apps).
  - **Controller**: Handle requests.

#### Best Practices
- **Entry Point**: server.js hoặc app.js.
- **Environment Folders**: src/, dist/ cho build.
- **Naming**: camelCase cho files, PascalCase cho classes.
- **Imports**: Dùng absolute paths với path aliases.

#### Bài Tập Thực Hành
1. **Basic structure**: Tạo folders config, controllers, models, routes.
2. **User CRUD**: Implement create, read, update, delete với structure.
3. **Middleware folder**: Thêm auth middleware.
4. **Utils folder**: Helper functions như validateEmail.
5. **Tests folder**: Unit test cho models.
6. **MVC app**: Build simple blog với MVC.
7. **Path aliases**: Dùng module-alias cho @/controllers.
8. **Environment split**: src/ cho source, dist/ cho build.
9. **Documentation**: README.md với setup instructions.
10. **Refactor**: Chuyển monolithic code sang structured.

## Phần 3: Cơ Bản - Modules, File System, HTTP

### Modules: Import/Export Code
Modules như hộp chứa code: Chia nhỏ app thành file riêng.

#### Ví Dụ Thú Vị: Quản Lý Utils Trong App
- **Tạo module utils.js**:
  ```javascript
  function greet(name) {
    return `Hello, ${name}!`;
  }

  module.exports = { greet };
  ```

- **Sử dụng trong app.js**:
  ```javascript
  const { greet } = require('./utils');
  console.log(greet('Alice')); // Hello, Alice!
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Tạo module**: utils.js với function sum(a, b).
2. **Export multiple**: Thêm multiply, export cả hai.
3. **Require module**: app.js require utils và gọi functions.
4. **Built-in modules**: Dùng fs, path modules.
5. **NPM install**: npm install lodash, require và dùng.
6. **ES6 modules**: Thử import/export với .mjs.
7. **Circular dependencies**: Tránh require lẫn nhau.
8. **Module caching**: Thấy require cache.
9. **Custom module**: Tạo module với class.
10. **Publish NPM**: Tạo package.json và publish local.

## Phần 4: File System - Đọc/Ghi Files

### File System Là Gì?
fs module như "thủ thư": Đọc, ghi, xóa files.

#### Ví Dụ Thú Vị: Quản Lý Config Files
- **Đọc file**:
  ```javascript
  const fs = require('fs');
  fs.readFile('config.json', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(JSON.parse(data));
  });
  ```

- **Ghi file**:
  ```javascript
  fs.writeFile('output.txt', 'Hello World', (err) => {
    if (err) throw err;
    console.log('File written');
  });
  ```

#### Bài Tập Thực Hành
1. **Read file sync**: fs.readFileSync.
2. **Write file**: Ghi JSON object.
3. **Append file**: Thêm text vào file.
4. **Read directory**: fs.readdir.
5. **Create directory**: fs.mkdir.
6. **Copy file**: fs.copyFile.
7. **Delete file**: fs.unlink.
8. **Watch file**: fs.watch for changes.
9. **Streams**: fs.createReadStream for large files.
10. **Promises**: Dùng fs.promises cho async.

## Phần 5: HTTP Server - Xây Dựng Web Server

### HTTP Là Gì?
http module như "người gác cửa": Tạo server nhận requests.

#### Ví Dụ Thú Vị: Simple API Server
- **Tạo server**:
  ```javascript
  const http = require('http');
  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World');
  });
  server.listen(3000, () => console.log('Server on 3000'));
  ```

- **Handle routes**:
  ```javascript
  if (req.url === '/api/users') {
    res.end(JSON.stringify([{ id: 1, name: 'Alice' }]));
  }
  ```

#### Bài Tập Thực Hành
1. **Basic server**: Respond 'Hello'.
2. **JSON response**: Return JSON data.
3. **Query params**: Parse req.url for params.
4. **POST data**: Handle req.on('data') for body.
5. **Headers**: Set custom headers.
6. **Status codes**: 404 for not found.
7. **Multiple routes**: /users, /posts.
8. **Static files**: Serve HTML/CSS.
9. **Error handling**: Try/catch in handlers.
10. **HTTPS**: Dùng https module.

## Phần 6: Asynchronous Programming - Callbacks, Promises, Async/Await

### Async Là Gì?
Node.js non-blocking: Code chạy tiếp mà không chờ I/O.

#### Ví Dụ Thú Vị: Fetch Data Từ API
- **Callback**:
  ```javascript
  fs.readFile('file.txt', (err, data) => {
    if (err) return console.error(err);
    console.log(data);
  });
  ```

- **Promise**:
  ```javascript
  fs.promises.readFile('file.txt')
    .then(data => console.log(data))
    .catch(err => console.error(err));
  ```

- **Async/Await**:
  ```javascript
  async function readFile() {
    try {
      const data = await fs.promises.readFile('file.txt');
      console.log(data);
    } catch (err) {
      console.error(err);
    }
  }
  ```

#### Bài Tập Thực Hành
1. **Callback hell**: Nested callbacks.
2. **Promise chain**: .then().then().
3. **Async function**: async/await.
4. **Error handling**: try/catch.
5. **Parallel async**: Promise.all.
6. **Sequential**: await in loop.
7. **Timeout**: setTimeout with promise.
8. **Fetch API**: node-fetch for HTTP.
9. **Database async**: Mock DB query.
10. **Event loop**: Understand with setImmediate.

## Phần 7: Events - Event-Driven Programming

### Events Là Gì?
EventEmitter như "đài phát thanh": Emit events, listen với listeners.

#### Ví Dụ Thú Vị: Logger System
- **Tạo emitter**:
  ```javascript
  const EventEmitter = require('events');
  const logger = new EventEmitter();

  logger.on('log', (message) => {
    console.log(`Log: ${message}`);
  });

  logger.emit('log', 'App started');
  ```

#### Bài Tập Thực Hành
1. **Basic emit/on**: Log events.
2. **Multiple listeners**: Nhiều on cho 1 event.
3. **Once**: on vs once.
4. **Remove listener**: removeListener.
5. **Custom class**: Extend EventEmitter.
6. **Error events**: Handle 'error'.
7. **Async events**: Emit with data.
8. **Stream events**: fs stream events.
9. **HTTP events**: req/res events.
10. **Event loop**: process events.

## Phần 8: Nâng Cao - Buffers, Streams, Child Processes

### Buffers: Xử Lý Binary Data
Buffers như "hộp đựng bytes": Cho images, files.

#### Streams: Dữ Liệu Lớn
Streams như "ống nước": Đọc/ghi dần.

#### Child Processes: Chạy Commands
child_process như "trợ lý": Chạy shell commands.

#### Bài Tập Thực Hành
1. **Buffer create**: Buffer.from('hello').
2. **Buffer concat**: Ghép buffers.
3. **Read stream**: fs.createReadStream.
4. **Write stream**: Pipe to file.
5. **Transform stream**: zlib gzip.
6. **Child exec**: exec('ls').
7. **Spawn**: spawn('node', ['script.js']).
8. **Fork**: fork for IPC.
9. **Cluster**: cluster for multi-core.
10. **Worker threads**: worker_threads for CPU tasks.

## Lưu Ý Cho Người Mới Học Node.js
- **Bắt đầu với basics**: Học modules, fs, http trước.
- **Thử với REPL**: node -i để test code.
- **Practive với projects**: Tạo simple server.
- **Đọc docs vui**: [Node.js docs](https://nodejs.org/en/docs/) có guides.
- **Lỗi thường gặp**: Callback hell -> dùng promises/async.

## Tổng Kết
Hướng dẫn này đã đi sâu vào Node.js thuần: modules, file system, HTTP servers, async programming, events, và nâng cao như streams, buffers, child processes. Bạn giờ có nền tảng vững để xây servers tùy chỉnh. Thực hành bài tập để củng cố!

Tiếp theo, phần 03 (03-express-guide.md) sẽ học Express.js – framework đơn giản hóa Node.js cho web apps. Chúc học vui!