# Challenge 4: Kết nối Database với Node.js

## Mục tiêu
Kết hợp Node.js với cơ sở dữ liệu PostgreSQL chuyên sâu.

## Quy tắc chung cho bảng
- Mỗi bảng sử dụng UUID làm primary key.
- Mỗi bảng cần có các trường: created_at (TIMESTAMP), updated_at (TIMESTAMP), created_by (UUID), updated_by (UUID).

## Yêu cầu
1. Cài đặt pg: `npm install pg`.
2. Tạo file `db.js`.
3. Kết nối đến PostgreSQL database (giả sử local với user postgres, password '', database 'testdb').
4. Viết hàm async để lấy tất cả user từ bảng `users`, bao gồm error handling.
5. Thêm hàm để insert user mới (cung cấp created_by).
6. Gọi các hàm và in kết quả ra console.

## Bài tập bổ sung
1. **Hàm getUserById**: Nhận id và trả về user object.
2. **Hàm updateUser**: Nhận id, data, updated_by và update user.
3. **Hàm deleteUser**: Nhận id và xóa user.
4. **Hàm getUsersWithPosts**: JOIN users và posts, trả về users với số posts.
5. **Connection pool**: Sử dụng Pool thay vì Client cho multiple queries.
6. **Environment variables**: Load DB config từ .env.

## Gợi ý
- Import: `const { Client } = require('pg');`
- Tạo client: `const client = new Client({ user: 'postgres', host: 'localhost', database: 'testdb', password: '', port: 5432 });`
- Kết nối: `await client.connect();`
- Query: `const res = await client.query('SELECT * FROM users');`
- Insert: `await client.query('INSERT INTO users (name, email, age, created_by) VALUES ($1, $2, $3, $4)', [name, email, age, createdByUuid]);`
- Đừng quên `await client.end();`
- getUserById: `const res = await client.query('SELECT * FROM users WHERE id = $1', [id]); return res.rows[0];`
- updateUser: `await client.query('UPDATE users SET name = $1, updated_at = NOW(), updated_by = $2 WHERE id = $3', [name, updatedBy, id]);`
- deleteUser: `await client.query('DELETE FROM users WHERE id = $1', [id]);`
- JOIN: `SELECT u.*, COUNT(p.id) as post_count FROM users u LEFT JOIN posts p ON u.id = p.user_id GROUP BY u.id;`
- Pool: `const { Pool } = require('pg'); const pool = new Pool({...});`
- .env: `require('dotenv').config(); const client = new Client({ connectionString: process.env.DATABASE_URL });`

## Kiểm tra
- Chạy script và xem output danh sách user, sau đó kiểm tra database.

## Tài liệu tham khảo
- [pg Documentation](https://node-postgres.com/)