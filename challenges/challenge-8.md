# Challenge 8: Testing với Jest

## Mục tiêu
Học cách viết unit tests và integration tests cho ứng dụng Node.js sử dụng Jest.

## Yêu cầu
1. Cài đặt Jest: `npm install --save-dev jest supertest`.
2. Viết tests cho các hàm utility (ví dụ: hàm tính tổng, validate email).
3. Viết integration tests cho API endpoints (sử dụng supertest cho Express routes).
4. Chạy tests: `npm test`.

## Gợi ý
- Tạo file test: `sum.test.js`
- Test cơ bản: `expect(sum(1, 2)).toBe(3);`
- Mock functions nếu cần.
- Integration test: `request(app).get('/api/users').expect(200);`

## Kiểm tra
- Chạy `npm test` và đảm bảo tất cả tests pass.

## Tài liệu tham khảo
- [Jest Documentation](https://jestjs.io/docs/getting-started)
- [Supertest](https://www.npmjs.com/package/supertest)