# Challenge 12: Microservices Basics

## Mục tiêu
Hiểu khái niệm microservices và xây dựng một hệ thống đơn giản với 2 services.

## Yêu cầu
1. Tạo 2 services riêng biệt: User Service và Order Service.
2. Sử dụng Express cho mỗi service.
3. Implement communication giữa services (sử dụng HTTP calls hoặc message queue đơn giản).
4. Chạy cả 2 services và test interaction.

## Gợi ý
- User Service: CRUD users.
- Order Service: Tạo orders, gọi User Service để validate user.
- Sử dụng axios cho HTTP calls: `const response = await axios.get('http://localhost:3001/users/' + userId);`

## Kiểm tra
- Tạo user qua User Service, tạo order qua Order Service và kiểm tra validation.

## Tài liệu tham khảo
- [Microservices Guide](https://microservices.io/)
- [Axios](https://axios-http.com/)