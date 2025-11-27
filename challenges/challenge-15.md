# Challenge 15: Environment Variables và Configuration

## Mục tiêu
Học cách quản lý configuration và environment variables.

## Yêu cầu
1. Cài đặt dotenv: `npm install dotenv`.
2. Tạo file .env với các biến như PORT, DATABASE_URL, JWT_SECRET.
3. Load .env trong app: `require('dotenv').config();`
4. Sử dụng config trong code thay vì hardcode values.
5. Tạo config validation.

## Gợi ý
- .env: `PORT=3000\nDATABASE_URL=postgres://...\nJWT_SECRET=secret`
- Usage: `const port = process.env.PORT || 3000;`

## Kiểm tra
- Chạy app với khác nhau .env và kiểm tra behavior.

## Tài liệu tham khảo
- [dotenv](https://www.npmjs.com/package/dotenv)