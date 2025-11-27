# Challenge 14: Security Best Practices

## Mục tiêu
Áp dụng các best practices bảo mật cho ứng dụng Node.js.

## Yêu cầu
1. Cài đặt Helmet, CORS, express-rate-limit: `npm install helmet cors express-rate-limit`.
2. Cấu hình Helmet để set security headers.
3. Enable CORS cho cross-origin requests.
4. Implement rate limiting cho API endpoints.
5. Validate input sử dụng Joi hoặc express-validator.

## Gợi ý
- Helmet: `app.use(helmet());`
- CORS: `app.use(cors());`
- Rate limit: `const limiter = rateLimit({ windowMs: 15 * 60 * 1000, max: 100 }); app.use(limiter);`

## Kiểm tra
- Test CORS, headers, và rate limiting.

## Tài liệu tham khảo
- [Helmet](https://helmetjs.github.io/)
- [CORS](https://www.npmjs.com/package/cors)
- [express-rate-limit](https://www.npmjs.com/package/express-rate-limit)