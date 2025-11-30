# Các Loại Truy Vấn Trong SQL

## Giới thiệu
SQL (Structured Query Language) là ngôn ngữ chuẩn để quản lý và thao tác cơ sở dữ liệu quan hệ. Các truy vấn SQL được phân loại theo chức năng thành 5 nhóm chính: DQL, DML, DDL, DCL, TCL

### SQL trong Backend Development
- **Kết nối DB**: Sử dụng libraries như `pg` (PostgreSQL) hoặc Sequelize ORM trong Node.js.
- **Parameterized Queries**: Tránh SQL injection bằng placeholders ($1, $2).
- **Connection Pooling**: Quản lý multiple connections hiệu quả.
- **Migrations**: Sử dụng tools như Knex.js để version schema changes.
- **Error Handling**: Catch DB errors và trả về proper HTTP status codes.
- **Caching**: Cache query results với Redis để improve performance.

### Ưu điểm của PostgreSQL
PostgreSQL là RDBMS mã nguồn mở mạnh mẽ, phù hợp cho backend development với nhiều tính năng advanced:

#### JSONB - JSON Binary
- **Lưu trữ JSON**: Column type JSONB lưu flexible data structures.
- **Query nhanh**: Index GIN cho JSONB queries, operators @>, ?, etc.
- **Ví dụ**: `SELECT * FROM users WHERE metadata @> '{"role": "admin"}'`
- **Ứng dụng**: Metadata, configurations, nested data mà không cần schema changes.

#### Rich Data Types
- **UUID**: `gen_random_uuid()` cho distributed systems.
- **ARRAY**: `TEXT[]`, `INTEGER[]` cho multiple values.
- **ENUM**: Custom enumerated types.
- **RANGE**: Date ranges, numeric ranges.
- **INET/CIDR**: IP addresses.
- **Ví dụ**: `CREATE TYPE user_status AS ENUM ('active', 'inactive', 'banned');`

#### Advanced Features
- **Full-text Search**: TSVECTOR, TSQUERY cho search engines.
- **GIS (PostGIS)**: Geographic data, spatial queries.
- **Triggers & Functions**: PL/pgSQL stored procedures.
- **Partitioning**: Table partitioning cho large datasets.
- **Replication**: Streaming replication, logical replication.
- **Extensibility**: Custom types, operators, functions.

#### Performance & Reliability
- **ACID Compliance**: Strong consistency.
- **MVCC**: Multi-version concurrency control.
- **Indexes**: B-tree, Hash, GIN, GiST, SP-GiST.
- **Query Planner**: Sophisticated optimizer.
- **Monitoring**: pg_stat_statements, pg_buffercache.

#### Best Practices với PostgreSQL
- Sử dụng JSONB cho flexible schemas.
- Leverage arrays cho simple lists.
- Use UUID cho primary keys trong microservices.
- Implement full-text search cho content.
- Monitor query performance với EXPLAIN ANALYZE.

#### Best Practices cho Backend
- **Validate Input**: Sử dụng Joi hoặc express-validator trước khi query.
- **Pagination**: Luôn dùng LIMIT/OFFSET hoặc cursor-based cho large datasets.
- **Indexing**: Tạo indexes trên columns thường query (e.g., user_id, email).
- **Transactions**: Wrap related operations (e.g., create user + create profile).
- **Logging**: Log slow queries và errors.
- **Security**: Sử dụng prepared statements, limit query complexity.

## Phần 1: Thiết kế và Thao tác Database

### 1. Data Definition Language (DDL) - Thiết kế Database
DDL dùng để định nghĩa và thay đổi cấu trúc database. Đây là bước đầu tiên khi tạo ứng dụng backend - thiết kế schema.

#### Lý thuyết về Database Design
- **Tables**: Đại diện cho entities (users, posts, orders). Mỗi table có columns và rows.
- **Columns**: Thuộc tính của entity. Chọn data types phù hợp (VARCHAR, INT, UUID, TIMESTAMP).
- **Primary Key**: Định danh duy nhất cho mỗi row (thường là ID).
- **Foreign Key**: Liên kết giữa tables (user_id trong posts table).
- **Constraints**: Đảm bảo data integrity (NOT NULL, UNIQUE, CHECK).
- **Indexes**: Tăng tốc queries nhưng chậm writes.
- **Views**: Virtual tables cho complex queries.
- **UUID vs SERIAL**: UUID cho distributed systems, SERIAL cho simple apps.

#### Lý thuyết DDL Commands
- **CREATE**: Tạo tables, indexes, views, functions.
- **ALTER**: Thay đổi cấu trúc: add/drop columns, change types, add constraints.
- **DROP**: Xóa objects. Sử dụng CASCADE cẩn thận.

#### Bài tập Thiết kế DB (1-15)
1. Thiết kế table users với columns: id (UUID), name, email, age, created_at.
2. Thêm constraints: PRIMARY KEY, UNIQUE email, CHECK age >= 0.
3. Tạo table posts với FK user_id, title, content, published_at.
4. Thiết kế table categories và many-to-many relationship với posts.
5. Tạo indexes trên email và user_id cho performance.
6. Viết CREATE VIEW cho active users (age >= 18).
7. ALTER TABLE thêm column avatar_url VARCHAR(255).
8. Tạo compound index trên (user_id, created_at).
9. Viết CREATE TABLE orders với FKs và constraints.
10. Thiết kế schema cho e-commerce app (users, products, orders, reviews).
11. Tạo table products với JSONB metadata cho flexible attributes.
12. Tạo ENUM type user_status ('active', 'inactive', 'banned').
13. Tạo table tags với ARRAY column tag_names TEXT[].
14. Tạo table events với RANGE column event_period TSRANGE.
15. Tạo table logs với JSONB data cho arbitrary log entries.

### 2. Data Manipulation Language (DML) - Thao tác Dữ liệu
Sau khi thiết kế DB, chúng ta thêm dữ liệu vào tables.

#### Lý thuyết DML
- **INSERT**: Thêm dữ liệu mới. Sử dụng RETURNING để lấy ID.
- **UPDATE**: Sửa dữ liệu existing. Luôn có WHERE.
- **DELETE**: Xóa dữ liệu. Cẩn thận với CASCADE.
- **Transactions**: Wrap multiple operations để đảm bảo consistency.

#### Bài tập Thao tác Dữ liệu (1-15)
1. INSERT user với RETURNING id.
2. INSERT multiple users từ array data.
3. UPDATE user profile với WHERE id = ?.
4. UPDATE set is_deleted=true cho soft delete.
5. DELETE user và CASCADE delete posts.
6. Transaction: INSERT user + INSERT profile.
7. Bulk INSERT từ CSV-like data.
8. UPSERT user data (INSERT OR UPDATE).
9. UPDATE multiple rows với subquery.
10. Transaction rollback on error.
11. INSERT product với JSONB metadata {'brand': 'Apple', 'specs': {...}}.
12. UPDATE user status sử dụng ENUM value.
13. INSERT tags với ARRAY ['javascript', 'nodejs'].
14. UPDATE event với RANGE period.
15. INSERT log entry với JSONB data.

### 3. Data Query Language (DQL) - Truy vấn Dữ liệu
Sau khi có dữ liệu, chúng ta query để lấy thông tin.

#### Lý thuyết DQL
- **SELECT**: Cấu trúc cơ bản với WHERE, ORDER BY, LIMIT.
- **JOINs**: Kết hợp dữ liệu từ multiple tables.
- **Aggregates**: COUNT, SUM, AVG với GROUP BY.
- **Subqueries**: Nested queries.
- **Window functions**: Advanced analytics.

#### Bài tập Truy vấn Dữ liệu (1-15)
1. SELECT users với pagination (LIMIT/OFFSET).
2. SELECT posts với user info sử dụng JOIN.
3. SELECT stats (total users, avg age) cho dashboard.
4. SELECT users theo name/email với LIKE.
5. SELECT với filters (age range) và sorting.
6. JOIN 3 tables: users -> posts -> categories.
7. Aggregate: posts per user với COUNT.
8. Subquery: users với more than 5 posts.
9. Window function: user ranking by post count.
10. Complex query với multiple JOINs và aggregates.
11. Query products WHERE metadata @> '{"brand": "Apple"}'.
12. SELECT users WHERE status = 'active'::user_status.
13. SELECT tags WHERE 'javascript' = ANY(tag_names).
14. SELECT events WHERE event_period && '[2023-01-01,2023-12-31]'.
15. Query logs WHERE data ->> 'level' = 'error'.

### 4. Data Control Language (DCL) - Bảo mật Database
DCL quản lý quyền truy cập.

#### Lý thuyết DCL
- **GRANT**: Cấp quyền cho users/roles.
- **REVOKE**: Thu hồi quyền.
- **Roles**: Nhóm quyền.

#### Bài tập Bảo mật (1-2)
1. GRANT SELECT, INSERT trên users cho app_user.
2. REVOKE DELETE từ regular users.

### 5. Transaction Control Language (TCL) - Quản lý Transactions
TCL đảm bảo data consistency.

#### Lý thuyết TCL
- **ACID**: Atomicity, Consistency, Isolation, Durability.
- **Isolation levels**: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE.
- **SAVEPOINT**: Partial rollback.

#### Bài tập Transactions (1-3)
1. BEGIN/COMMIT cho create user + wallet.
2. SAVEPOINT trong order processing.
3. SET ISOLATION LEVEL SERIALIZABLE.

### 6. NoSQL (MongoDB) - Alternative Database
MongoDB cho flexible schemas.

#### Lý thuyết NoSQL
- **Documents & Collections**: JSON-like data.
- **CRUD Operations**: insertOne, find, updateOne, deleteOne.
- **Indexing & Aggregation**: Performance optimization.
- **Data Modeling**: Embed vs Reference.

#### Bài tập NoSQL (1-10)
1. insertOne user với validation.
2. find users với filtering, sorting, pagination.
3. updateOne user profile.
4. aggregation pipeline cho stats.
5. populate refs User -> Posts.
6. create compound index.
7. text search với $text.
8. bulkWrite operations.
9. soft delete với isDeleted.
10. transaction cho money transfer.

## Phần 2: Implement API (Backend Implementations)

### DDL APIs (Thiết kế DB qua API)
1. API POST /tables để create table dynamically.
2. API PUT /tables/:name để alter table (add column).
3. API POST /indexes để create index.
4. API GET /schema để inspect current schema.
5. API DELETE /tables/:name để drop table (admin only).

### DML APIs (Thao tác Dữ liệu qua API)
6. API POST /users với INSERT, validate input.
7. API PUT /users/:id với UPDATE, check ownership.
8. API DELETE /users/:id với soft delete.
9. API POST /bulk-insert từ CSV data.
10. API PUT /users/:id/upsert cho sync data.

### DQL APIs (Truy vấn Dữ liệu qua API)
11. API GET /users với pagination, trả về JSON.
12. API GET /posts với JOIN, trả về posts với user info.
13. API GET /dashboard với aggregates (stats).
14. API GET /search với LIKE queries.
15. API GET /users với advanced filters & sorting.

### Bảo mật & Transaction APIs
16. API POST /permissions để grant/revoke permissions.
17. API POST /transactions để wrap multiple operations.
18. API POST /backup để create DB backup.

### NoSQL APIs
19. API POST /users với insert, validation, error handling.
20. API GET /users với filtering, sorting, pagination.
21. API PUT /users/:id với ownership check, update fields.
22. API DELETE /users/:id với soft delete.
23. API GET /users/stats với aggregation pipeline.
24. API GET /users/:id/posts với populate.
25. API POST /indexes để create indexes via API.
26. API GET /search với $text query.
27. API POST /bulk với bulkWrite operations.
28. API POST /transactions cho money transfer.
29. API GET /users/search với regex và text search.
30. API PUT /users/:id/profile với updateOne.

## Lưu ý chung
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQL Tutorial](https://www.w3schools.com/sql/)
- [SQL Best Practices](https://www.sqlstyle.guide/)
