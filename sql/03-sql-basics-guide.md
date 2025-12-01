# Hướng Dẫn SQL Cơ Bản Cho Người Mới: Cơ Sở Dữ Liệu Quan Hệ Thú Vị

## Giới Thiệu: SQL Là Gì?
SQL là ngôn ngữ để "nói chuyện" với cơ sở dữ liệu quan hệ. Nghĩ như một bảng tính Excel khổng lồ, nhưng thông minh hơn: Có thể tìm kiếm nhanh, liên kết dữ liệu, và đảm bảo an toàn. Mỗi "bảng" (table) như một tờ giấy với hàng (rows) và cột (columns).

### Tại Sao SQL Thú Vị?
- **Như tủ sách có thứ tự**: Mọi thứ có chỗ, dễ tìm. Thêm sách mới, sắp xếp lại, hoặc tìm sách theo tác giả.
- **Mạnh mẽ cho dữ liệu phức tạp**: Liên kết users với posts, categories với posts. Không bị lẫn lộn như tủ đồ hỗn độn.
- **An toàn và nhanh**: Dữ liệu nhất quán, truy vấn siêu tốc với hàng triệu bản ghi.
- **Ví dụ vui**: Tưởng tượng app blog: Users đăng posts, posts thuộc categories. SQL giúp bạn quản lý như thư viện số!

### Khi Nào Dùng SQL?
- App cần dữ liệu có cấu trúc rõ ràng (e-commerce, banking).
- Quan trọng tính nhất quán (không được mất tiền hay dữ liệu sai).
- Cần truy vấn phức tạp (tìm posts theo category và author).

## Phần 1: Cơ Bản - Thiết Kế Database (DDL)

### DDL Là Gì?
DDL là Data Definition Language. Dùng để "xây nhà": Tạo bảng, thêm cột, như thiết kế blueprint cho database.

#### Ví Dụ Thú Vị: Xây Dựng App Blog CMS
Tạo bảng users, posts, categories.

- **Tạo bảng users**:
  ```
  CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

- **Tạo bảng posts**:
  ```
  CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    content TEXT,
    user_id INTEGER REFERENCES users(id),
    category_id INTEGER REFERENCES categories(id),
    published_at TIMESTAMP
  );
  ```

- **Thay đổi bảng**: Thêm cột tags.
  ```
  ALTER TABLE posts ADD COLUMN tags TEXT[];
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Tạo database**: Trong PostgreSQL hoặc MySQL, tạo database tên "cms_blog".
2. **Tạo bảng users**: Với id (auto tăng), name, email, created_at.
3. **Tạo bảng categories**: id, name, description.
4. **Tạo bảng posts**: Liên kết với users và categories.
5. **Thêm cột**: ALTER để thêm published BOOLEAN cho posts.
6. **Tạo index**: CREATE INDEX trên email của users.
7. **Xem schema**: Dùng \d trong psql để xem cấu trúc bảng.
8. **Thêm constraint**: UNIQUE trên email, NOT NULL trên title.
9. **Xóa bảng**: DROP TABLE nếu sai, nhưng cẩn thận!
10. **Backup schema**: Dùng pg_dump để lưu cấu trúc.

## Phần 2: Thao Tác Dữ Liệu - CRUD Operations (DML)

### DML Là Gì?
DML là Data Manipulation Language. Dùng để thêm, sửa, xóa dữ liệu, như quản lý sách trong tủ.

#### Ví Dụ Thú Vị: Quản Lý Users Và Posts
- **Thêm user mới**:
  ```
  INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
  ```

- **Sửa thông tin user**:
  ```
  UPDATE users SET name = 'Alice Wonderland' WHERE id = 1;
  ```

- **Xóa post cũ**:
  ```
  DELETE FROM posts WHERE published_at < '2023-01-01';
  ```

- **Thêm nhiều dữ liệu**:
  ```
  INSERT INTO categories (name) VALUES ('Tech'), ('Lifestyle');
  ```

#### Bài Tập Thực Hành
1. **Insert user**: Thêm 3 users với name và email.
2. **Insert posts**: Tạo posts cho mỗi user, liên kết category.
3. **Update post**: Thay đổi title của một post.
4. **Update nhiều**: Set published = true cho posts cũ.
5. **Delete comment**: Giả sử có bảng comments, xóa comment spam.
6. **Bulk insert**: Thêm 5 categories cùng lúc.
7. **Upsert**: Dùng ON CONFLICT để insert hoặc update nếu trùng.
8. **Copy data**: Sao chép dữ liệu từ file CSV.
9. **Truncate**: Xóa tất cả dữ liệu trong bảng test.
10. **Kiểm tra**: SELECT COUNT(*) để xem số bản ghi.

## Phần 3: Truy Vấn Dữ Liệu - Querying (DQL)

### DQL Là Gì?
DQL là Data Query Language. Dùng để tìm kiếm, như tra cứu sách trong thư viện.

#### Ví Dụ Thú Vị: Tìm Posts Trong Blog
- **Tìm tất cả posts**:
  ```
  SELECT * FROM posts;
  ```

- **Tìm posts của user cụ thể**:
  ```
  SELECT * FROM posts WHERE user_id = 1;
  ```

- **JOIN để lấy author info**:
  ```
  SELECT p.title, u.name FROM posts p JOIN users u ON p.user_id = u.id;
  ```

- **Tìm với LIKE**:
  ```
  SELECT * FROM posts WHERE title LIKE '%tutorial%';
  ```

- **Group và count**:
  ```
  SELECT category_id, COUNT(*) FROM posts GROUP BY category_id;
  ```

#### Bài Tập Thực Hành
1. **SELECT cơ bản**: Lấy tất cả users.
2. **WHERE đơn giản**: Posts với published = true.
3. **JOIN hai bảng**: Posts với users để lấy author name.
4. **JOIN ba bảng**: Posts, users, categories.
5. **ORDER BY**: Sắp xếp posts theo published_at DESC.
6. **LIMIT và OFFSET**: Phân trang, lấy 10 posts đầu.
7. **Aggregate**: Đếm số posts per user.
8. **HAVING**: Users có > 5 posts.
9. **Subquery**: Posts của users có email chứa 'gmail'.
10. **Complex query**: Top categories theo số posts.

## Phần 4: Bảo Mật Database - Permissions (DCL)

### DCL Là Gì?
DCL là Data Control Language. Dùng để cho phép hoặc cấm truy cập, như khóa tủ sách.

#### Ví Dụ Thú Vị: Phân Quyền Cho App
- **Cho phép đọc**:
  ```
  GRANT SELECT ON users TO reader_role;
  ```

- **Cho phép viết**:
  ```
  GRANT INSERT, UPDATE ON posts TO writer_role;
  ```

- **Thu hồi quyền**:
  ```
  REVOKE DELETE ON posts FROM writer_role;
  ```

#### Bài Tập Thực Hành
1. **Tạo role**: CREATE ROLE editor;
2. **Grant select**: Cho editor đọc tất cả bảng.
3. **Grant insert**: Cho editor thêm posts.
4. **Revoke**: Thu hồi quyền xóa từ editor.
5. **Check permissions**: Dùng \dp để xem quyền.
6. **Role hierarchy**: Tạo role admin kế thừa editor.
7. **Grant on schema**: Quyền trên toàn bộ schema.
8. **Revoke all**: Thu hồi tất cả quyền từ user.
9. **Backup roles**: pg_dump roles.
10. **Test access**: Đăng nhập với role khác để thử.

## Phần 5: Quản Lý Transactions - Safety (TCL)

### TCL Là Gì?
TCL là Transaction Control Language. Dùng để nhóm thao tác, như một "gói" an toàn: Hoặc thành công hết, hoặc hủy hết.

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
  ROLLBACK; -- Nếu sai
  ```

#### Bài Tập Thực Hành
1. **Begin commit**: Thêm user và post trong transaction.
2. **Rollback**: Thử rollback sau insert.
3. **Savepoint**: Tạo savepoint giữa các thao tác.
4. **Nested transaction**: Transaction trong transaction.
5. **Isolation levels**: Set isolation level.
6. **Locking**: SELECT FOR UPDATE để khóa row.
7. **Deadlock**: Tạo deadlock và xử lý.
8. **Autocommit**: Tắt autocommit để manual commit.
9. **Error handling**: Catch lỗi trong transaction.
10. **Performance**: Đo thời gian transaction lớn.

## Phần 6: Nâng Cao - Indexing, Views, Triggers

### Indexing: Tăng Tốc Truy Vấn
Index như mục lục: Giúp tìm nhanh.

- **Tạo index**:
  ```
  CREATE INDEX idx_posts_user ON posts(user_id);
  ```

- **Index composite**:
  ```
  CREATE INDEX idx_posts_user_cat ON posts(user_id, category_id);
  ```

#### Views: Bảng Ảo
- **Tạo view**:
  ```
  CREATE VIEW recent_posts AS SELECT * FROM posts WHERE published_at > NOW() - INTERVAL '7 days';
  ```

#### Triggers: Tự Động Hành Động
- **Trigger update count**:
  ```
  CREATE TRIGGER update_post_count AFTER INSERT ON posts FOR EACH ROW EXECUTE FUNCTION increment_count();
  ```

#### Bài Tập Thực Hành
1. **Tạo index**: Index trên email users.
2. **Explain query**: Dùng EXPLAIN để xem index dùng không.
3. **Index partial**: Index chỉ cho posts published.
4. **Drop index**: Xóa index không dùng.
5. **Tạo view**: View posts với author name.
6. **View updatable**: View có thể update.
7. **Trigger insert**: Trigger log khi insert user.
8. **Trigger update**: Auto update timestamp.
9. **Function**: Viết function cho trigger.
10. **Advanced**: Partitioning bảng lớn.

## Lưu Ý Cho Người Mới Học SQL
- **Bắt đầu với SELECT**: Học tìm kiếm trước, rồi thêm/sửa.
- **Thử với tool**: Dùng pgAdmin hoặc DBeaver để GUI.
- **Practive với data thực**: Tạo database cho app cá nhân.
- **Đọc docs vui**: [PostgreSQL Tutorial](https://www.postgresqltutorial.com/) miễn phí.
- **Lỗi thường gặp**: Nhớ semicolon ;, dùng quotes cho string, JOIN đúng.

SQL như xây dựng thư viện số! Khi quen, bạn có thể quản lý dữ liệu phức tạp như ngân hàng. Chúc học vui!