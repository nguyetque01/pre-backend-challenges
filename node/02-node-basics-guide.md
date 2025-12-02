# Hướng Dẫn Node.js Cơ Bản Cho Người Mới: Runtime JavaScript Thú Vị

## Giới Thiệu: Node.js Là Gì?
Node.js là môi trường chạy JavaScript trên server, như một "cỗ máy" để JS thoát khỏi browser. Thay vì chỉ frontend, Node.js cho phép bạn xây dựng servers, APIs, và apps backend. Nó dùng V8 engine của Chrome, nên nhanh và mạnh mẽ.

### Tại Sao Node.js Thú Vị?
- **JavaScript everywhere**: Code frontend và backend cùng ngôn ngữ.
- **Non-blocking I/O**: Xử lý hàng nghìn requests mà không lag.
- **NPM ecosystem**: Hàng triệu packages miễn phí.
- **Ví dụ vui**: Tưởng tượng JS như siêu anh hùng: Trước chỉ browser, giờ "bay" lên server!

### Khi Nào Dùng Node.js?
- Apps cần real-time (chat, gaming).
- APIs, microservices.
- Full-stack JS projects.

## Mục Lục
- [Giới Thiệu: Node.js Là Gì?](#giới-thiệu-nodejs-là-gì)
- [Phần 1: Cơ Bản - Modules, File System, HTTP](#phần-1-cơ-bản---modules-file-system-http)
- [Phần 2: File System - Đọc/Ghi Files](#phần-2-file-system---đọcghi-files)
- [Phần 3: HTTP Server - Xây Dựng Web Server](#phần-3-http-server---xây-dựng-web-server)
- [Phần 4: Asynchronous Programming - Callbacks, Promises, Async/Await](#phần-4-asynchronous-programming---callbacks-promises-asyncawait)
- [Phần 5: Events - Event-Driven Programming](#phần-5-events---event-driven-programming)
- [Phần 6: Nâng Cao - Buffers, Streams, Child Processes](#phần-6-nâng-cao---buffers-streams-child-processes)
- [Lưu Ý Cho Người Mới Học Node.js](#lưu-ý-cho-người-mới-học-nodejs)
- [Tổng Kết](#tổng-kết)

## Phần 1: Cơ Bản - Modules, File System, HTTP

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

## Phần 2: File System - Đọc/Ghi Files

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

## Phần 3: HTTP Server - Xây Dựng Web Server

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

## Phần 4: Asynchronous Programming - Callbacks, Promises, Async/Await

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

## Phần 5: Events - Event-Driven Programming

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

## Phần 6: Nâng Cao - Buffers, Streams, Child Processes

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
Hướng dẫn này đã giới thiệu cơ bản Node.js: modules, file system, HTTP, async, events, và nâng cao như streams, child processes. Bạn giờ có nền tảng để xây dựng servers đơn giản. Hãy thực hành bài tập để củng cố kiến thức!

Node.js như cánh cửa backend cho JS devs! Khi quen, bạn xây apps realtime. Chúc học vui!