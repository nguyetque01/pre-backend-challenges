# Các Loại Truy Vấn Trong SQL

## Giới thiệu
SQL (Structured Query Language) là ngôn ngữ chuẩn để quản lý và thao tác cơ sở dữ liệu quan hệ. Các truy vấn SQL được phân loại theo chức năng thành 5 nhóm chính: DQL, DML, DDL, DCL, TCL. Bài viết này cung cấp Lý thuyết, ví dụ chi tiết và 30 bài tập thực hành, tập trung vào ứng dụng trong backend development với Node.js.

### Tại sao phân loại truy vấn?
- Giúp tổ chức và hiểu rõ mục đích của từng lệnh.
- Trong backend development, DML và DQL được sử dụng hàng ngày để thao tác dữ liệu trong APIs.
- DDL quan trọng cho thiết kế schema và migrations.
- DCL và TCL đảm bảo bảo mật và tính toàn vẹn dữ liệu trong multi-user apps.

### SQL trong Backend Development
- **Kết nối DB**: Sử dụng libraries như `pg` (PostgreSQL) hoặc Sequelize ORM trong Node.js.
- **Parameterized Queries**: Tránh SQL injection bằng placeholders ($1, $2).
- **Connection Pooling**: Quản lý multiple connections hiệu quả.
- **Migrations**: Sử dụng tools như Knex.js để version schema changes.
- **Error Handling**: Catch DB errors và trả về proper HTTP status codes.
- **Caching**: Cache query results với Redis để improve performance.

#### Ví dụ tích hợp với Node.js (sử dụng pg)
```javascript
const { Pool } = require('pg');
const pool = new Pool({ connectionString: process.env.DATABASE_URL });

// DQL: Get users
app.get('/users', async (req, res) => {
  try {
    const result = await pool.query('SELECT * FROM users WHERE age > $1', [18]);
    res.json(result.rows);
  } catch (err) {
    res.status(500).json({ error: 'DB error' });
  }
});

// DML: Create user
app.post('/users', async (req, res) => {
  const { name, email, age } = req.body;
  try {
    const result = await pool.query(
      'INSERT INTO users (name, email, age) VALUES ($1, $2, $3) RETURNING id',
      [name, email, age]
    );
    res.status(201).json({ id: result.rows[0].id });
  } catch (err) {
    res.status(400).json({ error: 'Insert failed' });
  }
});
```

#### Best Practices cho Backend
- **Validate Input**: Sử dụng Joi hoặc express-validator trước khi query.
- **Pagination**: Luôn dùng LIMIT/OFFSET hoặc cursor-based cho large datasets.
- **Indexing**: Tạo indexes trên columns thường query (e.g., user_id, email).
- **Transactions**: Wrap related operations (e.g., create user + create profile).
- **Logging**: Log slow queries và errors.
- **Security**: Sử dụng prepared statements, limit query complexity.

## 1. Data Query Language (DQL) - Ngôn ngữ truy vấn dữ liệu

## 1. Data Query Language (DQL) - Ngôn ngữ truy vấn dữ liệu
DQL chỉ bao gồm lệnh SELECT, dùng để truy vấn và lấy dữ liệu từ database mà không thay đổi nó. Đây là loại truy vấn phổ biến nhất trong ứng dụng backend.

### Lý thuyết
- **Cấu trúc SELECT**: `SELECT columns FROM table WHERE condition ORDER BY column LIMIT n;`
- **Best practices**: Sử dụng WHERE để lọc sớm, tránh SELECT * trên bảng lớn, dùng LIMIT cho pagination.
- **JOINs**: INNER, LEFT, RIGHT, FULL để kết hợp dữ liệu từ nhiều bảng.
- **Aggregate functions**: COUNT, SUM, AVG, MIN, MAX với GROUP BY.
- **Subqueries**: Query lồng nhau, có thể chậm nếu không tối ưu.
- **Window functions**: ROW_NUMBER, RANK cho phân tích dữ liệu (PostgreSQL, SQL Server).

### Ví dụ chi tiết
```sql
-- Basic SELECT
SELECT id, name FROM users WHERE age BETWEEN 18 AND 65 ORDER BY name DESC;

-- JOIN
SELECT u.name, p.title FROM users u INNER JOIN posts p ON u.id = p.user_id;

-- Aggregate
SELECT user_id, COUNT(*) as post_count FROM posts GROUP BY user_id HAVING COUNT(*) > 5;

-- Window function
SELECT name, age, ROW_NUMBER() OVER (ORDER BY age DESC) as rank FROM users;
```

### Bài tập DQL (1-10) - Tập trung Backend
1. **API GET /users**: Viết query SELECT lấy users với pagination (LIMIT/OFFSET), trả về JSON cho API.
2. **JOIN cho API**: Query lấy posts với user info, sử dụng trong endpoint GET /posts.
3. **Aggregate cho Dashboard**: Query tính stats (total users, avg age) cho admin dashboard.
4. **Search API**: Query tìm users theo name/email với LIKE, case-insensitive.
5. **Filter & Sort**: Query users với filters (age range, name) và sorting, cho advanced search API.
6. **Subquery trong API**: Query lấy users có orders > 100, sử dụng cho user segmentation.
7. **Pagination với Window**: Sử dụng ROW_NUMBER để implement cursor-based pagination.
8. **Caching Query**: Query phức tạp cho cache (e.g., top posts), tránh recompute.
9. **Real-time Data**: Query lấy recent posts (last 24h) cho notifications.
10. **Analytics**: Query group users by age range, count per group cho reports.

## 2. Data Manipulation Language (DML) - Ngôn ngữ thao tác dữ liệu
DML bao gồm INSERT, UPDATE, DELETE, dùng để thay đổi dữ liệu. Các lệnh này ảnh hưởng trực tiếp đến dữ liệu và thường được sử dụng trong transactions.

### Lý thuyết
- **INSERT**: Có thể insert một hoặc nhiều rows. Sử dụng RETURNING để lấy ID vừa insert.
- **UPDATE**: Luôn có WHERE để tránh update toàn bộ bảng. Có thể update dựa trên subquery.
- **DELETE**: Tương tự UPDATE, cần WHERE. Sử dụng CASCADE nếu có FK.
- **Best practices**: Sử dụng transactions cho multiple operations, validate data trước khi insert/update, log changes cho audit.
- **Bulk operations**: INSERT với VALUES list hoặc SELECT từ bảng khác.
- **UPSERT**: INSERT ... ON CONFLICT UPDATE (PostgreSQL).

### Ví dụ chi tiết
```sql
-- INSERT multiple
INSERT INTO users (name, email) VALUES ('John', 'john@example.com'), ('Jane', 'jane@example.com');

-- UPDATE with subquery
UPDATE users SET age = (SELECT AVG(age) FROM users) WHERE age IS NULL;

-- DELETE with JOIN (MySQL/PostgreSQL)
DELETE u FROM users u LEFT JOIN posts p ON u.id = p.user_id WHERE p.id IS NULL;

-- UPSERT
INSERT INTO users (id, name) VALUES (1, 'John') ON CONFLICT (id) DO UPDATE SET name = EXCLUDED.name;
```

### Bài tập DML (11-20) - Tập trung Backend
11. **API POST /users**: Query INSERT user từ request body, validate và return new ID.
12. **Bulk Insert**: Query INSERT multiple records từ array data (e.g., import CSV).
13. **Update Profile**: Query UPDATE user profile, chỉ allow update own data (check user_id).
14. **Soft Delete**: Query UPDATE set is_deleted=true thay vì DELETE, cho audit trail.
15. **Transaction trong API**: Wrap INSERT user + INSERT profile trong transaction, rollback on error.
16. **Conditional Update**: Update user status chỉ nếu conditions met (e.g., age > 18).
17. **Audit Logging**: Query INSERT vào audit_log table mỗi khi UPDATE/DELETE.
18. **Batch Update**: Update multiple users based on criteria (e.g., bulk email change).
19. **Upsert for Sync**: Use UPSERT để sync data từ external API.
20. **Delete Cascade**: Handle DELETE với FK constraints trong API (soft delete related).

## 3. Data Definition Language (DDL) - Ngôn ngữ định nghĩa dữ liệu
DDL dùng để định nghĩa và thay đổi cấu trúc database: tạo bảng, index, constraints, etc.

### Lý thuyết
- **CREATE**: Tạo tables, indexes, views, functions.
- **ALTER**: Thay đổi cấu trúc: add/drop columns, change types, add constraints.
- **DROP**: Xóa objects. Sử dụng CASCADE cẩn thận.
- **Constraints**: PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, NOT NULL.
- **Indexes**: B-tree (default), Hash, GIN (for arrays/JSON). Tối ưu queries nhưng chậm writes.
- **Views**: Virtual tables, có thể update nếu simple.
- **UUID vs SERIAL**: UUID tốt cho distributed systems, tránh conflicts; SERIAL đơn giản hơn nhưng có thể leak info.

### Ví dụ chi tiết
```sql
-- Enable UUID extension
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- CREATE with constraints
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 0),
    created_at TIMESTAMP DEFAULT NOW()
);

-- ALTER
ALTER TABLE users ADD COLUMN updated_at TIMESTAMP;
ALTER TABLE users DROP COLUMN age;

-- Index
CREATE INDEX idx_users_email ON users (email);
CREATE UNIQUE INDEX idx_users_name_email ON users (name, email);

-- View
CREATE VIEW active_users AS SELECT * FROM users WHERE age >= 18;
```

### Bài tập DDL (21-25) - Tập trung Backend
21. **Schema Design cho API**: CREATE TABLE users với UUID PRIMARY KEY DEFAULT gen_random_uuid(), timestamps, constraints (NOT NULL, UNIQUE).
22. **Migration Script**: ALTER TABLE thêm cột avatar_url VARCHAR(255) cho user profiles.
23. **Index cho Performance**: CREATE INDEX trên email và user_id để optimize API queries.
24. **View cho Reporting**: CREATE VIEW user_activity với joins cho dashboard API.
25. **Constraints cho Validation**: ADD CHECK (age >= 0 AND age <= 150), UNIQUE (email).

## 4. Data Control Language (DCL) - Ngôn ngữ kiểm soát dữ liệu
DCL quản lý quyền truy cập và bảo mật.

### Lý thuyết
- **GRANT**: Cấp quyền SELECT, INSERT, UPDATE, DELETE, etc. trên tables/views.
- **REVOKE**: Thu hồi quyền.
- **Roles**: Nhóm quyền, dễ quản lý.
- **Best practices**: Principle of least privilege, audit permissions.

### Ví dụ chi tiết
```sql
-- Grant specific
GRANT SELECT, INSERT ON users TO app_user;

-- Grant all
GRANT ALL PRIVILEGES ON DATABASE mydb TO admin;

-- Revoke
REVOKE INSERT ON users FROM app_user;

-- Role
CREATE ROLE readonly;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly;
```

### Bài tập DCL (26-27) - Tập trung Backend
26. **API Permissions**: GRANT SELECT, INSERT trên users cho app_user role.
27. **Security Audit**: REVOKE DELETE permissions từ regular users, chỉ admin có.

## 5. Transaction Control Language (TCL) - Ngôn ngữ kiểm soát giao dịch
TCL quản lý transactions để đảm bảo ACID properties.

### Lý thuyết
- **ACID**: Atomicity, Consistency, Isolation, Durability.
- **Isolation levels**: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE.
- **SAVEPOINT**: Điểm lưu trong transaction.
- **Best practices**: Sử dụng transactions cho related operations, handle deadlocks.

### Ví dụ chi tiết
```sql
-- Transaction
BEGIN;
INSERT INTO users (name) VALUES ('Alice');
SAVEPOINT sp1;
UPDATE users SET age = 25 WHERE name = 'Alice';
ROLLBACK TO sp1; -- Hoàn tác update
COMMIT; -- Commit insert

-- Isolation
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

### Bài tập TCL (28-30) - Tập trung Backend
28. **API Transaction**: BEGIN/COMMIT cho create user + create wallet in one API call.
29. **Partial Rollback**: SAVEPOINT trong order processing, rollback payment if inventory fails.
30. **Concurrency Control**: Use SERIALIZABLE for critical operations like stock updates.

## Lưu ý chung
- Luôn test queries trên data sample trước khi production.
- Sử dụng EXPLAIN để analyze performance.
- Backup database trước khi chạy DDL.
- Trong Node.js, sử dụng parameterized queries để tránh SQL injection.

### Ví dụ Backend Scenarios
- **User Registration API**: DML INSERT + validation, return JWT.
- **Product Search**: DQL với LIKE, pagination, sorting.
- **Order Processing**: TCL transaction for deduct inventory + create order.
- **Admin Dashboard**: DQL aggregates cho stats, caching results.
- **Data Migration**: DDL ALTER tables, bulk DML updates.

## Tài liệu tham khảo
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQL Tutorial](https://www.w3schools.com/sql/)
- [SQL Best Practices](https://www.sqlstyle.guide/)