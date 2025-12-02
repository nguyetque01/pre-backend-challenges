# Hướng Dẫn Các Loại Operations Trong Node.js Cho Người Mới: Ngôn Ngữ Xây Dựng Backend

## Giới Thiệu: Node.js Operations Là Gì Và Tại Sao Thú Vị?
Node.js operations như "công cụ" để xây dựng backend: HTTP requests, file handling, database queries, async tasks. Từ cơ bản (sync code), nâng cao (streams, clusters). Như một hộp đồ nghề, mỗi operation giải quyết vấn đề khác nhau.

### Tại Sao Học Các Loại Operations?
- **Mạnh mẽ cho apps**: Từ APIs đơn giản đến systems phức tạp.
- **Non-blocking**: Xử lý concurrent mà không lag.
- **Dễ bắt đầu**: Bắt đầu với basics, thêm dần.
- **Ví dụ vui**: Tưởng tượng Node như đầu bếp: Sync như nấu ăn tuần tự, async như multi-tasking!

### Khi Nào Dùng Node Operations?
- Web servers, APIs.
- Real-time apps (chat, gaming).
- Data processing, file uploads.

## Mục Lục
- [Giới Thiệu: Node.js Operations Là Gì Và Tại Sao Thú Vị?](#giới-thiệu-nodejs-operations-là-gì-và-tại-sao-thú-vị)
- [Phần 1: Synchronous Operations - Code Đơn Giản](#phần-1-synchronous-operations---code-đơn-giản)
- [Phần 2: Asynchronous Operations - Callbacks, Promises, Async/Await](#phần-2-asynchronous-operations---callbacks-promises-asyncawait)
- [Phần 3: HTTP Operations - Requests/Responses](#phần-3-http-operations---requestsresponses)
- [Phần 4: File System Operations - Đọc/Ghi Files](#phần-4-file-system-operations---đọcghi-files)
- [Phần 5: Database Operations - Queries](#phần-5-database-operations---queries)
- [Phần 6: Event-Driven Operations - Emit/Listen](#phần-6-event-driven-operations---emitlisten)
- [Phần 7: Stream Operations - Dữ Liệu Lớn](#phần-7-stream-operations---dữ-liệu-lớn)
- [Phần 8: Child Process Operations - Chạy Commands](#phần-8-child-process-operations---chạy-commands)
- [Phần 9: Timer Operations - Scheduling](#phần-9-timer-operations---scheduling)
- [Phần 10: Error Handling Operations - Robust Apps](#phần-10-error-handling-operations---robust-apps)
- [Tổng Kết](#tổng-kết)

## Phần 1: Synchronous Operations - Code Đơn Giản

### Sync Là Gì?
Sync như "hàng đợi": Code chạy tuần tự, chờ từng task.

#### Ví Dụ Thú Vị: Simple Calculations
- **Sync function**:
  ```javascript
  function add(a, b) {
    return a + b;
  }
  console.log(add(2, 3)); // 5
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Basic sync**: Function return value.
2. **Loops**: for loop calculations.
3. **Conditionals**: if/else logic.
4. **Arrays**: map, filter sync.
5. **Objects**: Create, modify.
6. **Strings**: Concat, split.
7. **Dates**: new Date().
8. **Math**: Math.random().
9. **JSON**: JSON.parse/stringify.
10. **Errors**: throw new Error().

## Phần 2: Asynchronous Operations - Callbacks, Promises, Async/Await

### Async Là Gì?
Async như "multi-tasking": Code không chờ, tiếp tục.

#### Ví Dụ Thú Vị: File Read
- **Callback**:
  ```javascript
  fs.readFile('file.txt', (err, data) => {
    console.log(data);
  });
  ```

- **Promise**:
  ```javascript
  fs.promises.readFile('file.txt').then(data => console.log(data));
  ```

- **Async/Await**:
  ```javascript
  const data = await fs.promises.readFile('file.txt');
  ```

#### Bài Tập Thực Hành
1. **Callback**: fs.readFile.
2. **Promise chain**: .then().catch().
3. **Async function**: async/await.
4. **Parallel**: Promise.all.
5. **Sequential**: await in loop.
6. **Error handling**: try/catch.
7. **Timeout**: setTimeout promise.
8. **Fetch**: node-fetch for HTTP.
9. **DB query**: Mock async query.
10. **Event loop**: setImmediate.

## Phần 3: HTTP Operations - Requests/Responses

### HTTP Là Gì?
HTTP như "thư tín": Gửi/nhận data qua web.

#### Ví Dụ Thú Vị: API Calls
- **GET request**:
  ```javascript
  const https = require('https');
  https.get('https://api.example.com/users', (res) => {
    res.on('data', (chunk) => console.log(chunk));
  });
  ```

- **POST with fetch**:
  ```javascript
  const response = await fetch('https://api.example.com/users', {
    method: 'POST',
    body: JSON.stringify({ name: 'Alice' })
  });
  ```

#### Bài Tập Thực Hành
1. **GET**: https.get().
2. **POST**: https.request().
3. **Headers**: Set Authorization.
4. **Body**: JSON.stringify.
5. **Response**: res.on('data').
6. **Errors**: req.on('error').
7. **Fetch API**: npm install node-fetch.
8. **Axios**: npm install axios.
9. **Proxy**: http-proxy.
10. **WebSockets**: ws library.

## Phần 4: File System Operations - Đọc/Ghi Files

### FS Là Gì?
FS như "thủ thư": Quản lý files.

#### Ví Dụ Thú Vị: Config Management
- **Read JSON**:
  ```javascript
  const config = JSON.parse(await fs.promises.readFile('config.json'));
  ```

- **Write log**:
  ```javascript
  await fs.promises.appendFile('log.txt', 'New entry\n');
  ```

#### Bài Tập Thực Hành
1. **Read file**: fs.readFile.
2. **Write file**: fs.writeFile.
3. **Append**: fs.appendFile.
4. **Directory**: fs.readdir.
5. **Create dir**: fs.mkdir.
6. **Copy**: fs.copyFile.
7. **Delete**: fs.unlink.
8. **Stats**: fs.stat.
9. **Watch**: fs.watch.
10. **Streams**: createReadStream.

## Phần 5: Database Operations - Queries

### DB Ops Là Gì?
DB ops như "tra cứu": CRUD với data.

#### Ví Dụ Thú Vị: User CRUD
- **MongoDB**:
  ```javascript
  const user = await User.findOne({ email: 'alice@example.com' });
  ```

- **SQL**:
  ```javascript
  const users = await pool.query('SELECT * FROM users');
  ```

#### Bài Tập Thực Hành
1. **Connect DB**: mongoose.connect().
2. **Create**: User.create().
3. **Read**: User.find().
4. **Update**: User.updateOne().
5. **Delete**: User.deleteOne().
6. **SQL insert**: pool.query(INSERT).
7. **SQL select**: SELECT.
8. **Transactions**: BEGIN/COMMIT.
9. **Joins**: INNER JOIN.
10. **Migrations**: Run migrations.

## Phần 6: Event-Driven Operations - Emit/Listen

### Events Là Gì?
Events như "đài phát thanh": Emit, listen.

#### Ví Dụ Thú Vị: Logger
- **Emitter**:
  ```javascript
  const emitter = new EventEmitter();
  emitter.on('log', (msg) => console.log(msg));
  emitter.emit('log', 'App started');
  ```

#### Bài Tập Thực Hành
1. **Basic event**: on/emit.
2. **Multiple listeners**: Nhiều on.
3. **Once**: emitter.once().
4. **Remove**: removeListener.
5. **Custom class**: class extends EventEmitter.
6. **Async events**: Emit with promise.
7. **HTTP events**: req.on('data').
8. **Stream events**: stream.on('end').
9. **Process events**: process.on('exit').
10. **Error events**: 'error'.

## Phần 7: Stream Operations - Dữ Liệu Lớn

### Streams Là Gì?
Streams như "ống nước": Xử lý data dần.

#### Ví Dụ Thú Vị: File Upload
- **Read stream**:
  ```javascript
  const stream = fs.createReadStream('large.txt');
  stream.on('data', (chunk) => console.log(chunk));
  ```

#### Bài Tập Thực Hành
1. **Read stream**: createReadStream.
2. **Write stream**: createWriteStream.
3. **Pipe**: stream.pipe().
4. **Transform**: zlib.createGzip().
5. **Duplex**: Custom duplex stream.
6. **HTTP streams**: req.pipe(res).
7. **Multipart**: multer for uploads.
8. **CSV parser**: csv-parser.
9. **WebSocket streams**: ws streams.
10. **Backpressure**: Handle slow consumers.

## Phần 8: Child Process Operations - Chạy Commands

### Child Processes Là Gì?
Child processes như "trợ lý": Chạy external commands.

#### Ví Dụ Thú Vị: Run Scripts
- **Exec**:
  ```javascript
  exec('ls -la', (err, stdout) => console.log(stdout));
  ```

- **Spawn**:
  ```javascript
  const child = spawn('node', ['script.js']);
  ```

#### Bài Tập Thực Hành
1. **Exec**: exec('echo hello').
2. **Spawn**: spawn('npm', ['start']).
3. **Fork**: fork('./worker.js').
4. **IPC**: send/receive messages.
5. **Stdio**: Pipe stdin/stdout.
6. **Kill**: child.kill().
7. **Cluster**: cluster.fork().
8. **Worker threads**: new Worker().
9. **Shell scripts**: Run bash scripts.
10. **Cross-platform**: Handle Windows/Linux.

## Phần 9: Timer Operations - Scheduling

### Timers Là Gì?
Timers như "đồng hồ": Chạy code sau thời gian.

#### Ví Dụ Thú Vị: Scheduled Tasks
- **setTimeout**:
  ```javascript
  setTimeout(() => console.log('Done'), 1000);
  ```

- **setInterval**:
  ```javascript
  setInterval(() => console.log('Tick'), 1000);
  ```

#### Bài Tập Thực Hành
1. **setTimeout**: Delay execution.
2. **setInterval**: Repeat task.
3. **clearTimeout**: Cancel timeout.
4. **clearInterval**: Stop interval.
5. **Promises**: Timeout promise.
6. **Scheduler**: node-schedule.
7. **Cron**: node-cron.
8. **Debounce**: Custom debounce.
9. **Throttle**: Custom throttle.
10. **Performance**: Measure timing.

## Phần 10: Error Handling Operations - Robust Apps

### Error Handling Là Gì?
Error handling như "bảo hiểm": Catch và handle errors.

#### Ví Dụ Thú Vị: Safe Code
- **Try/catch**:
  ```javascript
  try {
    riskyFunction();
  } catch (err) {
    console.error(err);
  }
  ```

- **Global handler**:
  ```javascript
  process.on('uncaughtException', (err) => {
    console.error('Uncaught:', err);
    process.exit(1);
  });
  ```

#### Bài Tập Thực Hành
1. **Try/catch**: Sync errors.
2. **Async errors**: Promise.catch().
3. **Global handlers**: uncaughtException.
4. **Custom errors**: class MyError.
5. **Validation**: Joi for input.
6. **Logging**: winston logger.
7. **Monitoring**: Sentry.
8. **Graceful shutdown**: Handle SIGTERM.
9. **Testing errors**: Throw in tests.
10. **Debugging**: --inspect flag.

## Tổng Kết

Trong chương này, chúng ta đã khám phá các loại operations chính trong Node.js, từ synchronous đơn giản đến asynchronous phức tạp, HTTP requests, file system, database queries, events, streams, child processes, timers, và error handling. Mỗi loại operation đều có vai trò quan trọng trong việc xây dựng backend applications mạnh mẽ và hiệu quả.

**Điểm Chính:**
- **Synchronous**: Đơn giản nhưng block, dùng cho tasks nhanh.
- **Asynchronous**: Non-blocking, dùng callbacks/promises/async-await cho I/O.
- **HTTP**: Xử lý requests/responses, middleware, REST APIs.
- **File System**: Đọc/ghi files, directories, permissions.
- **Database**: Connect, CRUD operations, ORMs, transactions.
- **Events**: Event-driven programming với EventEmitter.
- **Streams**: Xử lý data lớn hiệu quả, pipes, transforms.
- **Child Processes**: Chạy external commands, IPC, clustering.
- **Timers**: Scheduling tasks với setTimeout/setInterval.
- **Error Handling**: Try/catch, global handlers, logging, monitoring.

**Lời Khuyên:** Bắt đầu với synchronous để hiểu basics, rồi chuyển sang async. Thử nghiệm với REPL và build projects nhỏ. Đọc Node.js docs và practice thường xuyên để master operations.

Node.js operations như siêu năng lực! Khi master, bạn có thể xây dựng bất kỳ backend nào. Chúc học vui!</content>
<parameter name="filePath">d:\WorkSpace\Books\Pre-Backend-Challenges\node\05-node-operations-types.md