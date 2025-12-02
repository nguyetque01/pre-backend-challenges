# Hướng Dẫn Các Loại Truy Vấn SQL Cho Người Mới: Ngôn Ngữ Nói Chuyện Với Database

## Giới Thiệu: SQL Là Gì Và Tại Sao Thú Vị?
SQL là ngôn ngữ để "nói chuyện" với cơ sở dữ liệu, như một người phiên dịch giữa bạn và kho dữ liệu khổng lồ. Thay vì lục tung tủ đồ hỗn độn, SQL giúp bạn tìm kiếm nhanh như tra cứu sách trong thư viện thông minh. Mỗi truy vấn SQL như một câu hỏi hoặc lệnh: "Cho tôi xem posts của user này", hoặc "Thêm user mới vào".

### Tại Sao Học Các Loại Truy Vấn SQL?
- **Như quản lý thư viện số**: Tạo kệ sách (DDL), thêm/sửa sách (DML), tìm sách (DQL), khóa tủ (DCL), và đảm bảo mọi thứ ổn (TCL).
- **Mạnh mẽ cho app**: Từ blog đơn giản đến mạng xã hội lớn, SQL xử lý dữ liệu hiệu quả.
- **Dễ bắt đầu**: Bắt đầu với SELECT, rồi học thêm dần.
- **Ví dụ vui**: Tưởng tượng app blog CMS: Users đăng posts, posts thuộc categories. SQL giúp bạn quản lý như một thư viện viên siêu tốc!

### Khi Nào Dùng SQL Queries?
- App cần dữ liệu có cấu trúc rõ ràng (e-commerce, CMS).
- Quan trọng tính nhất quán và truy vấn phức tạp.
- Dự án cần mở rộng và bảo mật cao.

## Mục Lục
- [Phần 1: DDL - Thiết Kế Database Như Xây Nhà](#phần-1-ddl---thiết-kế-database-như-xây-nhà)
- [Phần 2: DML - Thao Tác Dữ Liệu Như Quản Lý Sách](#phần-2-dml---thao-tác-dữ-liệu-như-quản-lý-sách)
- [Phần 3: DQL - Truy Vấn Dữ Liệu Như Tra Cứu Sách](#phần-3-dql---truy-vấn-dữ-liệu-như-tra-cứu-sách)
- [Phần 4: DCL - Bảo Mật Database Như Khóa Tủ](#phần-4-dcl---bảo-mật-database-như-khóa-tủ)
- [Phần 5: TCL - Quản Lý Transactions Như Gói An Toàn](#phần-5-tcl---quản-lý-transactions-như-gói-an-toàn)
- [Phần 6: Nâng Cao - Tính Năng Chuyên Sâu Cho Pro](#phần-6-nâng-cao---tính-năng-chuyên-sâu-cho-pro)
- [Phần 7: Kết Hợp Với Backend - Thực Hành API](#phần-7-kết-hợp-với-backend---thực-hành-api)
- [Lưu Ý Cho Người Mới Học SQL Queries](#lưu-ý-cho-người-mới-học-sql-queries)

## Phần 1: DDL - Thiết Kế Database Như Xây Nhà

### DDL Là Gì?
DDL là Data Definition Language, như bản thiết kế cho nhà: Tạo phòng (bảng), thêm cửa sổ (cột), và sắp xếp đồ đạc (constraints). Không thêm dữ liệu, chỉ định hình cấu trúc.

#### Ví Dụ Thú Vị: Xây Dựng App Blog CMS
Tạo bảng users, posts, categories như thiết kế phòng cho gia đình số.

- **Tạo bảng users**:
  ```
  CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

- **Thêm cột cho posts**:
  ```
  ALTER TABLE posts ADD COLUMN tags TEXT[];
  ```

- **Tạo index để tìm nhanh**:
  ```
  CREATE INDEX idx_posts_user ON posts(user_id);
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Tạo database**: CREATE DATABASE cms_blog;
2. **Tạo bảng users**: Với id, name, email, created_at.
3. **Tạo bảng categories**: id, name, description.
4. **Tạo bảng posts**: Liên kết với users và categories.
5. **Thêm cột**: ALTER để thêm published BOOLEAN.
6. **Tạo index**: Index trên email users.
7. **Foreign keys**: Đảm bảo posts liên kết đúng với users.
8. **Constraints**: UNIQUE trên email, NOT NULL trên name.
9. **Views**: CREATE VIEW recent_posts AS SELECT * FROM posts WHERE created_at > NOW() - INTERVAL '7 days';
10. **Drop table**: DROP TABLE test_table (cẩn thận!).

## Phần 2: DML - Thao Tác Dữ Liệu Như Quản Lý Sách

### DML Là Gì?
DML là Data Manipulation Language, như thêm, sửa, xóa sách trong tủ: Thêm cuốn mới, sửa tiêu đề, hoặc dọn dẹp sách cũ.

#### Ví Dụ Thú Vị: Quản Lý Users Và Posts Trong Blog
- **Thêm user mới**:
  ```
  INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
  ```

- **Sửa thông tin post**:
  ```
  UPDATE posts SET title = 'New Title' WHERE id = 1;
  ```

- **Xóa comment cũ**:
  ```
  DELETE FROM comments WHERE created_at < '2023-01-01';
  ```

#### Bài Tập Thực Hành
1. **Insert user**: Thêm user với name và email.
2. **Insert posts**: Tạo 3 posts cho user khác nhau.
3. **Update user**: Thay đổi name của user.
4. **Update posts**: Set published = true cho posts cũ.
5. **Delete post**: Xóa post cụ thể.
6. **Bulk insert**: Thêm nhiều categories cùng lúc.
7. **Upsert**: INSERT ON CONFLICT để update nếu email trùng.
8. **Soft delete**: Update is_deleted = true thay vì delete.
9. **Transaction insert**: BEGIN; INSERT user; INSERT profile; COMMIT;
10. **Kiểm tra**: SELECT COUNT(*) sau mỗi thao tác.

## Phần 3: DQL - Truy Vấn Dữ Liệu Như Tra Cứu Sách

### DQL Là Gì?
DQL là Data Query Language, như tìm sách trong thư viện: Tìm theo tác giả, tiêu đề, hoặc kết hợp nhiều điều kiện.

#### Ví Dụ Thú Vị: Tìm Posts Trong Blog
- **Tìm tất cả posts**:
  ```
  SELECT * FROM posts;
  ```

- **Tìm posts của user với JOIN**:
  ```
  SELECT p.title, u.name FROM posts p JOIN users u ON p.user_id = u.id;
  ```

- **Tìm với điều kiện**:
  ```
  SELECT * FROM posts WHERE published = true ORDER BY created_at DESC LIMIT 10;
  ```

- **Đếm và nhóm**:
  ```
  SELECT category_id, COUNT(*) FROM posts GROUP BY category_id;
  ```

#### Bài Tập Thực Hành
1. **SELECT cơ bản**: Lấy tất cả users.
2. **WHERE đơn giản**: Posts với published = true.
3. **JOIN hai bảng**: Posts với users để lấy author.
4. **JOIN ba bảng**: Posts, users, categories.
5. **ORDER BY**: Sắp xếp posts theo created_at.
6. **LIMIT/OFFSET**: Phân trang, lấy 5 posts đầu.
7. **Aggregate**: Đếm posts per user.
8. **HAVING**: Users có > 2 posts.
9. **Subquery**: Posts của users từ subquery.
10. **Complex query**: Top categories theo số posts.

## Phần 4: DCL - Bảo Mật Database Như Khóa Tủ

### DCL Là Gì?
DCL là Data Control Language, như khóa tủ và chia chìa khóa: Cho phép ai đọc, ai viết, ai xóa.

#### Ví Dụ Thú Vị: Phân Quyền Cho Blog
- **Cho phép đọc**:
  ```
  GRANT SELECT ON posts TO reader;
  ```

- **Thu hồi quyền**:
  ```
  REVOKE DELETE ON users FROM editor;
  ```

#### Bài Tập Thực Hành
1. **Tạo role**: CREATE ROLE editor;
2. **Grant select**: Cho editor đọc users và posts.
3. **Grant insert**: Cho editor thêm posts.
4. **Revoke**: Thu hồi quyền xóa từ editor.
5. **Check permissions**: Dùng \dp để xem quyền.
6. **Role hierarchy**: Tạo role admin kế thừa editor.
7. **Grant on schema**: Quyền trên toàn bộ schema.
8. **Revoke all**: Thu hồi tất cả quyền từ user.
9. **Test access**: Đăng nhập với role khác để thử.
10. **Backup roles**: pg_dump roles.

## Phần 5: TCL - Quản Lý Transactions Như Gói An Toàn

### TCL Là Gì?
TCL là Transaction Control Language, như gói quà: Mọi thứ bên trong phải ổn, hoặc hủy hết nếu có lỗi.

#### Ví Dụ Thú Vị: Publish Post Và Cập Nhật Thống Kê
- **Transaction đơn giản**:
  ```
  BEGIN;
  INSERT INTO posts (title, user_id) VALUES ('New Post', 1);
  UPDATE users SET post_count = post_count + 1 WHERE id = 1;
  COMMIT;
  ```

- **Rollback nếu lỗi**:
  ```
  BEGIN;
  -- Thao tác
  ROLLBACK; -- Hủy nếu sai
  ```

#### Bài Tập Thực Hành
1. **Begin commit**: Thêm user và post trong transaction.
2. **Rollback**: Thử rollback sau insert.
3. **Savepoint**: Tạo savepoint giữa thao tác.
4. **Nested transaction**: Transaction trong transaction.
5. **Isolation levels**: Set READ COMMITTED.
6. **Locking**: SELECT FOR UPDATE để khóa row.
7. **Deadlock**: Tạo và xử lý deadlock.
8. **Autocommit**: Tắt autocommit.
9. **Error handling**: Catch lỗi trong transaction.
10. **Performance**: Đo thời gian transaction lớn.

## Phần 6: Nâng Cao - Tính Năng Chuyên Sâu Cho Pro

### Indexing Và Views: Tăng Tốc Và Tiện Lợi
- **Index như mục lục**: CREATE INDEX để query nhanh.
- **Views như bảng ảo**: CREATE VIEW cho queries phức tạp.

#### Triggers Và Functions: Tự Động Hành Động
- **Trigger**: Auto-update khi insert.
  ```
  CREATE TRIGGER update_timestamp BEFORE UPDATE ON posts FOR EACH ROW EXECUTE FUNCTION update_modified_column();
  ```

#### Full-Text Search: Tìm Kiếm Như Google
- **Tìm text**:
  ```
  SELECT * FROM posts WHERE to_tsvector('english', content) @@ to_tsquery('tutorial');
  ```

#### Bài Tập Thực Hành
1. **Tạo index**: Index trên user_id posts.
2. **Explain query**: Dùng EXPLAIN để xem index dùng không.
3. **Index partial**: Index chỉ cho posts published.
4. **Drop index**: Xóa index không dùng.
5. **Tạo view**: View posts với user name.
6. **View updatable**: View có thể update.
7. **Trigger insert**: Trigger log khi insert user.
8. **Trigger update**: Auto update timestamp.
9. **Function**: Viết function cho trigger.
10. **Full-text**: Tìm posts chứa 'backend'.

## Phần 7: Kết Hợp Với Backend - Thực Hành API

### Implement API Với SQL Queries
Như xây app thực tế: Kết nối database với code.

#### Ví Dụ Thú Vị: API Cho Blog CMS
- **GET /posts**: SELECT với JOIN và pagination.
- **POST /users**: INSERT với validation.
- **PUT /posts/:id**: UPDATE với check ownership.

#### Bài Tập Thực Hành
1. **API GET users**: Trả về JSON với pagination.
2. **API POST user**: Insert với error handling.
3. **API PUT user**: Update profile.
4. **API DELETE post**: Soft delete.
5. **API GET search**: Query với LIKE.
6. **API GET stats**: Aggregate cho dashboard.
7. **API POST transaction**: Wrap multiple inserts.
8. **API GET with auth**: Check permissions.
9. **API POST bulk**: Bulk insert từ array.
10. **API GET advanced**: Complex query với filters.

## Tổng Kết

Trong hướng dẫn này, chúng ta đã khám phá các loại truy vấn SQL chính, từ DDL đến DCL, TCL, và các tính năng nâng cao.

**Điểm Chính:**
- **DDL**: Thiết kế database với CREATE, ALTER, indexes.
- **DML**: Thao tác dữ liệu với INSERT, UPDATE, DELETE.
- **DQL**: Truy vấn với SELECT, JOIN, aggregates.
- **DCL**: Bảo mật với GRANT, REVOKE.
- **TCL**: An toàn với transactions BEGIN/COMMIT/ROLLBACK.
- **Nâng Cao**: Indexing, views, triggers, full-text search.
- **Backend Integration**: Kết hợp với API thực tế.

**Lời Khuyên:** Bắt đầu với DQL (SELECT), rồi học DDL và DML. Thử nghiệm với database thực và xây dựng APIs. SQL là kỹ năng cốt lõi cho backend developers.

## Lưu Ý Cho Người Mới Học SQL Queries
- **Bắt đầu với SELECT**: Học tìm kiếm trước, rồi thêm/sửa.
- **Thử với tool**: Dùng DBeaver hoặc pgAdmin để GUI.
- **Practive với data thực**: Tạo database cho app cá nhân.
- **Đọc docs vui**: [SQLZoo](https://sqlzoo.net/) có bài tập interactive.
- **Lỗi thường gặp**: Nhớ semicolon ;, dùng prepared statements.
- **Kết hợp với ORM**: Học Sequelize sau khi quen raw SQL.

SQL như ngôn ngữ bí mật của database! Khi quen, bạn có thể quản lý dữ liệu như một wizard. Chúc học vui!
