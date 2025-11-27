# Challenge 2: Xây dựng HTTP Server

## Mục tiêu
Hiểu cách tạo một server HTTP đơn giản với Express.js.

## Yêu cầu
1. Cài đặt Express: `npm install express`.
2. Tạo file `server.js`.
3. Viết code để tạo server lắng nghe trên port 3000.
4. Tạo route GET `/` trả về JSON: `{"message": "Hello from Express!"}`.
5. Chạy server và test bằng browser hoặc curl.

## Bài tập bổ sung
1. **Thêm route POST**: Tạo route POST `/echo` nhận JSON body và trả về cùng data.
2. **Middleware logging**: Thêm middleware log mỗi request (method, URL, timestamp).
3. **Static files**: Serve static files từ folder `public` (tạo file `index.html`).
4. **Route parameters**: Tạo route GET `/user/:id` trả về `{"userId": id}`.
5. **Query parameters**: Tạo route GET `/search` nhận query `q` và trả về `{"query": q}`.

## Gợi ý
- Import Express: `const express = require('express');`
- Tạo app: `const app = express();`
- Định nghĩa route: `app.get('/', (req, res) => { res.json({...}); });`
- Lắng nghe: `app.listen(3000, () => console.log('Server running...'));`
- POST: `app.use(express.json()); app.post('/echo', (req, res) => res.json(req.body));`
- Logging: `app.use((req, res, next) => { console.log(`${req.method} ${req.url} ${new Date()}`); next(); });`
- Static: `app.use(express.static('public'));`
- Params: `app.get('/user/:id', (req, res) => res.json({ userId: req.params.id }));`
- Query: `app.get('/search', (req, res) => res.json({ query: req.query.q }));`

## Kiểm tra
- Truy cập http://localhost:3000/ và nhận JSON response.
- Test các routes bổ sung với curl hoặc Postman.

## Tài liệu tham khảo
- [Express.js Hello World](https://expressjs.com/en/starter/hello-world.html)