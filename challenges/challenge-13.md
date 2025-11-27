# Challenge 13: Error Handling và Logging

## Mục tiêu
Học cách xử lý lỗi và logging trong ứng dụng Node.js.

## Yêu cầu
1. Cài đặt Winston: `npm install winston`.
2. Tạo middleware error handling cho Express app.
3. Implement logging cho requests, errors, và custom events.
4. Tạo custom error classes.

## Gợi ý
- Middleware error: `app.use((err, req, res, next) => { logger.error(err.message); res.status(500).send('Something went wrong!'); });`
- Winston logger: `const logger = winston.createLogger({ transports: [new winston.transports.File({ filename: 'error.log' })] });`

## Kiểm tra
- Gây lỗi trong app và kiểm tra logs.

## Tài liệu tham khảo
- [Winston Documentation](https://github.com/winstonjs/winston)