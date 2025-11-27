# Challenge 1: Hello World với Node.js

## Mục tiêu
Làm quen với môi trường Node.js, cài đặt và chạy một script cơ bản.

## Yêu cầu
1. Cài đặt Node.js (nếu chưa có).
2. Tạo một file `hello.js`.
3. Viết code để in ra "Hello World" trên console.
4. Chạy script bằng lệnh `node hello.js`.

## Bài tập bổ sung
1. **In biến**: Tạo biến `name` với giá trị tên của bạn và in ra "Hello, [name]!".
2. **Sử dụng process.argv**: Nhận tên từ command line arguments và in "Hello, [arg]!".
3. **Tạo module**: Tạo file `greetings.js` với hàm `sayHello(name)` và import vào `hello.js`.
4. **Sử dụng setTimeout**: In "Hello World" sau 2 giây.
5. **Đọc file**: Tạo file `message.txt` với nội dung "Hello from file!" và đọc in ra.

## Gợi ý
- Sử dụng `console.log()` để in ra.
- Kiểm tra phiên bản Node.js bằng `node --version`.
- process.argv: `const name = process.argv[2] || 'World';`
- Module: `module.exports = { sayHello };`
- setTimeout: `setTimeout(() => console.log('Hello World'), 2000);`
- File: `const fs = require('fs'); fs.readFile('message.txt', 'utf8', (err, data) => console.log(data));`

## Kiểm tra
- Output: "Hello World"
- Các bài tập bổ sung: Kiểm tra output tương ứng.

## Tài liệu tham khảo
- [Node.js Getting Started](https://nodejs.org/en/docs/guides/getting-started-guide/)