# Challenge 18: Email Sending với Nodemailer

## Mục tiêu
Học cách gửi emails từ Node.js app.

## Yêu cầu
1. Cài đặt Nodemailer: `npm install nodemailer`.
2. Cấu hình transporter (sử dụng Gmail hoặc service khác).
3. Tạo hàm gửi email (welcome, password reset, etc.).
4. Integrate vào authentication flow (e.g., send welcome email on register).

## Gợi ý
- Transporter: `const transporter = nodemailer.createTransporter({ service: 'gmail', auth: { user, pass } });`
- Send: `transporter.sendMail({ from, to, subject, text });`

## Kiểm tra
- Gửi email test và kiểm tra inbox.

## Tài liệu tham khảo
- [Nodemailer](https://nodemailer.com/)