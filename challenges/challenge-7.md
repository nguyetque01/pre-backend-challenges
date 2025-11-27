# Challenge 7: Authentication với JWT

## Mục tiêu
Học cách triển khai authentication cơ bản sử dụng JSON Web Tokens (JWT) trong Node.js với Express.

## Yêu cầu
1. Cài đặt các package cần thiết: `npm install express jsonwebtoken bcryptjs`.
2. Tạo server Express với các route:
   - POST /register: Đăng ký user mới (hash password với bcrypt).
   - POST /login: Đăng nhập và trả về JWT token.
   - GET /protected: Route bảo vệ, yêu cầu JWT token trong header.
3. Sử dụng middleware để verify JWT token.
4. Lưu trữ user trong memory (hoặc kết nối đến database nếu muốn nâng cao).

## Gợi ý
- Tạo secret key cho JWT: `const jwtSecret = 'your-secret-key';`
- Hash password: `const hashedPassword = await bcrypt.hash(password, 10);`
- Tạo token: `const token = jwt.sign({ userId: user.id }, jwtSecret, { expiresIn: '1h' });`
- Middleware verify: Kiểm tra header Authorization: Bearer <token>

## Kiểm tra
- Đăng ký user, đăng nhập để lấy token, truy cập route protected.

## Tài liệu tham khảo
- [JWT Documentation](https://jwt.io/)
- [bcryptjs](https://www.npmjs.com/package/bcryptjs)