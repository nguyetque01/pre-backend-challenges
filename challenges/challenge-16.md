# Challenge 16: API Versioning

## Mục tiêu
Học cách version API để maintain backward compatibility.

## Yêu cầu
1. Implement versioning bằng URL path (e.g., /api/v1/users).
2. Tạo v1 và v2 của một API endpoint với changes.
3. Sử dụng Express routers cho từng version.
4. Document versioning strategy.

## Gợi ý
- Router: `const v1Router = express.Router(); app.use('/api/v1', v1Router);`
- V2 có thêm fields hoặc changes response format.

## Kiểm tra
- Call cả v1 và v2 endpoints và so sánh responses.

## Tài liệu tham khảo
- [API Versioning Strategies](https://www.xmatters.com/blog/blog/2017/05/24/api-versioning)