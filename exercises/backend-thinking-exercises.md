# Bộ Bài Tập Tư Duy Backend và Dự Án Thực Tế - Bài Tập Thực Tế Cho Học Viên

Để rèn luyện tư duy backend, giải quyết vấn đề thực tế và áp dụng kiến thức vào dự án, dưới đây là bộ bài tập nâng cao. Những bài này được thiết kế như bài tập thực tế để test kỹ năng của học viên, với yêu cầu cụ thể, hướng dẫn và tiêu chí đánh giá.

## Hướng Dẫn Chung Cho Học Viên
- **Thời gian**: Mỗi bài tập 1-2 tuần, tùy độ khó.
- **Công cụ**: Sử dụng Node.js/Express hoặc .NET/ASP.NET, Git, Postman.
- **Nộp bài**: Push code lên GitHub/GitLab, viết README với giải thích thiết kế.
- **Đánh giá**: Dựa trên code quality, documentation, testing, performance.

## Bài Tập Tư Duy và Giải Quyết Vấn Đề

### Bài Tập 1: Thiết Kế API cho Ứng Dụng E-commerce
**Mô tả**: Bạn là backend developer cho một startup e-commerce. Thiết kế RESTful API cho cửa hàng online với sản phẩm, giỏ hàng, thanh toán.

**Yêu cầu**:
- Endpoints: /products (CRUD), /cart (add/remove), /orders (create, list), /payments (process).
- Authentication: JWT cho users.
- Xử lý concurrency: Inventory không âm.
- Error handling: Appropriate status codes.

**Hướng dẫn**:
1. Vẽ ER diagram cho DB (products, users, orders, cart).
2. Viết OpenAPI spec.
3. Implement API với framework đã chọn.
4. Test với Postman.

**Tiêu chí đánh giá**:
- Hoàn thành: 40% (tất cả endpoints hoạt động).
- Code quality: 30% (clean, documented).
- Security: 20% (auth, validation).
- Performance: 10% (concurrency handling).

### Bài Tập 2: Tối Ưu Hóa Performance cho API Có Lưu Lượng Cao
**Mô tả**: API hiện tại chậm với 10k requests/phút do DB queries. Tối ưu hóa.

**Yêu cầu**:
- Giảm response time dưới 200ms.
- Sử dụng caching, indexing, load balancing.
- Đo lường cải thiện (trước/sau).

**Hướng dẫn**:
1. Profile current performance (use tools like Artillery).
2. Add Redis caching cho frequent queries.
3. Index DB columns.
4. Deploy với load balancer (nginx).

**Tiêu chí đánh giá**:
- Cải thiện: 50% (response time giảm >50%).
- Implementation: 30% (caching, indexing đúng).
- Documentation: 20% (giải thích optimizations).

### Bài Tập 3: Bảo Mật API Chống Attacks
**Mô tả**: API bị tấn công SQL injection, XSS, DDoS. Bảo mật nó.

**Yêu cầu**:
- Validate tất cả inputs.
- Rate limiting (max 100 req/min per IP).
- HTTPS, JWT secure.
- Test với OWASP ZAP.

**Hướng dẫn**:
1. Add input validation (Joi for Node.js, DataAnnotations for .NET).
2. Implement rate limiting middleware.
3. Configure HTTPS.
4. Run security tests.

**Tiêu chí đánh giá**:
- Security: 50% (pass OWASP tests).
- Implementation: 30% (middleware correct).
- Documentation: 20% (explain vulnerabilities fixed).

### Bài Tập 4: Migration Database Không Downtime
**Mô tả**: Thêm cột "email_verified" vào bảng users (1M records) mà không downtime.

**Yêu cầu**:
- Migration script.
- Blue-green deployment.
- Rollback plan.

**Hướng dẫn**:
1. Write migration (add column with default false).
2. Deploy to staging, test.
3. Use blue-green: Deploy new version, switch traffic.
4. Monitor và rollback nếu cần.

**Tiêu chí đánh giá**:
- No downtime: 40% (app available during migration).
- Migration: 30% (script correct, reversible).
- Deployment: 30% (blue-green implemented).

### Bài Tập 5: Xử Lý Asynchronous Tasks
**Mô tả**: Sau đăng ký user, gửi email welcome mà không block response.

**Yêu cầu**:
- Queue system (Bull for Node.js, Hangfire for .NET).
- Background job gửi email.
- Monitor queue.

**Hướng dẫn**:
1. Setup queue (Redis-based).
2. Add job to queue on user register.
3. Implement email sender.
4. Monitor với dashboard.

**Tiêu chí đánh giá**:
- Async: 40% (response không block).
- Implementation: 30% (queue correct).
- Monitoring: 30% (dashboard available).

## Dự Án Thực Tế

### Dự Án 1: Todo App API
**Mô tả**: Xây dựng API CRUD cho tasks, với auth.

**Yêu cầu**:
- Endpoints: GET/POST/PUT/DELETE /tasks.
- Auth: Register/login, JWT.
- DB: MongoDB hoặc PostgreSQL.

**Hướng dẫn**:
1. Setup project.
2. Design DB schema.
3. Implement auth.
4. Add CRUD, test.

**Tiêu chí đánh giá**:
- Functionality: 50% (all endpoints work).
- Auth: 30% (secure).
- Code: 20% (clean).

### Dự Án 2: Blog Platform
**Mô tả**: API cho blog với posts, comments, users.

**Yêu cầu**:
- File upload cho images.
- Search posts.
- Caching cho popular posts.

**Hướng dẫn**:
1. Setup project.
2. Add models (User, Post, Comment).
3. Implement upload (multer for Node.js).
4. Add search, caching (Redis).

**Tiêu chí đánh giá**:
- Features: 40% (upload, search, cache).
- Performance: 30% (caching effective).
- UI/API: 30% (well-designed).

### Dự Án 3: E-commerce Microservice
**Mô tả**: Microservices cho products, orders, payments.

**Yêu cầu**:
- 3 services riêng.
- API Gateway.
- Docker compose.

**Hướng dẫn**:
1. Design architecture.
2. Implement each service.
3. Setup gateway (Ocelot for .NET, Express for Node).
4. Dockerize và deploy.

**Tiêu chí đánh giá**:
- Architecture: 40% (services decoupled).
- Communication: 30% (gateway works).
- Deployment: 30% (Docker).

### Dự Án 4: Real-time Chat App
**Mô tả**: API với WebSockets cho chat rooms.

**Yêu cầu**:
- Rooms, messages.
- Real-time updates.
- Auth.

**Hướng dẫn**:
1. Setup WebSockets (Socket.io/SignalR).
2. Add rooms, messages.
3. Authenticate connections.
4. Test real-time.

**Tiêu chí đánh giá**:
- Real-time: 50% (messages instant).
- Features: 30% (rooms, auth).
- Scaling: 20% (handle multiple users).

### Dự Án 5: Analytics Dashboard
**Mô tả**: API thu thập logs, phân tích data.

**Yêu cầu**:
- Collect logs.
- Aggregation queries.
- Dashboard endpoint.

**Hướng dẫn**:
1. Setup logging (Winston/ Serilog).
2. Store in DB.
3. Build aggregation (group by date, etc.).
4. API trả data cho dashboard.

**Tiêu chí đánh giá**:
- Data collection: 40% (logs stored).
- Analysis: 30% (queries correct).
- API: 30% (data accessible).

## Cách Tiếp Cận Chung
- **Phân Tích Vấn Đề**: Hiểu requirements, constraints.
- **Thiết Kế**: Vẽ diagrams, chọn tech stack.
- **Implement**: Code theo best practices.
- **Test và Deploy**: Đảm bảo quality, monitor.
- **Review**: Tự đánh giá, cải thiện.

Những bài này giúp phát triển kỹ năng tư duy, chuẩn bị cho công việc thực tế. Tham khảo tài liệu trong repo để hỗ trợ.