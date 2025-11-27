# Challenge 3: Cơ bản PostgreSQL Queries

## Mục tiêu
Làm quen với cú pháp PostgreSQL cơ bản và nâng cao để truy vấn dữ liệu.

## Quy tắc chung cho bảng
- Mỗi bảng sử dụng UUID làm primary key.
- Mỗi bảng cần có các trường: created_at (TIMESTAMP), updated_at (TIMESTAMP), created_by (UUID), updated_by (UUID).

## Yêu cầu
1. Cài đặt PostgreSQL và tạo database 'testdb'.
2. Tạo bảng `users` với cột: id (UUID PRIMARY KEY DEFAULT gen_random_uuid()), name (VARCHAR(100)), email (VARCHAR(100) UNIQUE), age (INT), created_at (TIMESTAMP DEFAULT NOW()), updated_at (TIMESTAMP DEFAULT NOW()), created_by (UUID), updated_by (UUID).
3. Viết các câu lệnh SQL sau:
   - Lấy tất cả user.
   - Lấy user có id = 'some-uuid'.
   - Lấy user có age > 18, sắp xếp theo name.
   - Thêm một user mới (cung cấp created_by nếu có).
   - Cập nhật email của user có id = 'some-uuid' (cập nhật updated_at và updated_by).
   - Xóa user có id = 'some-uuid'.
   - Tạo index trên cột email.
   - Sử dụng JOIN nếu có bảng liên quan (tùy chọn nâng cao).

## Bài tập bổ sung
1. **Tạo bảng posts**: Tạo bảng `posts` với id (UUID), title (VARCHAR), content (TEXT), user_id (UUID FK), created_at, updated_at, created_by, updated_by.
2. **INSERT dữ liệu mẫu**: Thêm vài posts liên kết với users.
3. **JOIN query**: Lấy posts với user name.
4. **Subquery**: Lấy users có ít nhất 1 post.
5. **Aggregate**: Đếm số posts per user.
6. **Transaction**: Thêm user và post trong 1 transaction.

## Gợi ý
- Kích hoạt extension: `CREATE EXTENSION IF NOT EXISTS "uuid-ossp";`
- Tạo bảng: `CREATE TABLE users (id UUID PRIMARY KEY DEFAULT gen_random_uuid(), name VARCHAR(100), email VARCHAR(100) UNIQUE, age INT, created_at TIMESTAMP DEFAULT NOW(), updated_at TIMESTAMP DEFAULT NOW(), created_by UUID, updated_by UUID);`
- SELECT: `SELECT * FROM users;`
- WHERE: `SELECT * FROM users WHERE id = '550e8400-e29b-41d4-a716-446655440000';`
- INSERT: `INSERT INTO users (name, email, age, created_by) VALUES ('John', 'john@example.com', 25, '550e8400-e29b-41d4-a716-446655440000');`
- UPDATE: `UPDATE users SET email = 'new@example.com', updated_at = NOW(), updated_by = '550e8400-e29b-41d4-a716-446655440000' WHERE id = '550e8400-e29b-41d4-a716-446655440000';`
- DELETE: `DELETE FROM users WHERE id = '550e8400-e29b-41d4-a716-446655440000';`
- Index: `CREATE INDEX idx_email ON users (email);`
- Posts table: `CREATE TABLE posts (id UUID PRIMARY KEY DEFAULT gen_random_uuid(), title VARCHAR(200), content TEXT, user_id UUID REFERENCES users(id), created_at TIMESTAMP DEFAULT NOW(), updated_at TIMESTAMP DEFAULT NOW(), created_by UUID, updated_by UUID);`
- JOIN: `SELECT p.title, u.name FROM posts p JOIN users u ON p.user_id = u.id;`
- Subquery: `SELECT * FROM users WHERE id IN (SELECT DISTINCT user_id FROM posts);`
- Aggregate: `SELECT u.name, COUNT(p.id) FROM users u LEFT JOIN posts p ON u.id = p.user_id GROUP BY u.id, u.name;`
- Transaction: `BEGIN; INSERT INTO users ...; INSERT INTO posts ...; COMMIT;`

## Kiểm tra
- Sử dụng psql hoặc pgAdmin để chạy các query và kiểm tra kết quả.

## Tài liệu tham khảo
- [PostgreSQL Tutorial](https://www.postgresql.org/docs/current/tutorial.html)