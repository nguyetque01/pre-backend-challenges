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

#### Best Practices cho Backend
- **Validate Input**: Sử dụng Joi hoặc express-validator trước khi query.
- **Pagination**: Luôn dùng LIMIT/OFFSET hoặc cursor-based cho large datasets.
- **Indexing**: Tạo indexes trên columns thường query (e.g., user_id, email).
- **Transactions**: Wrap related operations (e.g., create user + create profile).
- **Logging**: Log slow queries và errors.
- **Security**: Sử dụng prepared statements, limit query complexity.

## Phần 1: Thực hiện trong DB (Queries & Operations)

### 1. Data Query Language (DQL) - Ngôn ngữ truy vấn dữ liệu
DQL chỉ bao gồm lệnh SELECT, dùng để truy vấn và lấy dữ liệu từ database mà không thay đổi nó. Đây là loại truy vấn phổ biến nhất trong ứng dụng backend.

#### Lý thuyết
- **Cấu trúc SELECT**: `SELECT columns FROM table WHERE condition ORDER BY column LIMIT n;`
- **Best practices**: Sử dụng WHERE để lọc sớm, tránh SELECT * trên bảng lớn, dùng LIMIT cho pagination.
- **JOINs**: INNER, LEFT, RIGHT, FULL để kết hợp dữ liệu từ nhiều bảng.
- **Aggregate functions**: COUNT, SUM, AVG, MIN, MAX với GROUP BY.
- **Subqueries**: Query lồng nhau, có thể chậm nếu không tối ưu.
- **Window functions**: ROW_NUMBER, RANK cho phân tích dữ liệu (PostgreSQL, SQL Server).

#### Bài tập (1-5)
1. Viết query SELECT lấy users với pagination (LIMIT/OFFSET).
2. Viết query lấy posts với user info sử dụng JOIN.
3. Viết query tính stats (total users, avg age) cho dashboard.
4. Viết query tìm users theo name/email với LIKE, case-insensitive.
5. Viết query users với filters (age range, name) và sorting.

### 2. Data Manipulation Language (DML) - Ngôn ngữ thao tác dữ liệu
DML bao gồm INSERT, UPDATE, DELETE, dùng để thay đổi dữ liệu. Các lệnh này ảnh hưởng trực tiếp đến dữ liệu và thường được sử dụng trong transactions.

#### Lý thuyết
- **INSERT**: Có thể insert một hoặc nhiều rows. Sử dụng RETURNING để lấy ID vừa insert.
- **UPDATE**: Luôn có WHERE để tránh update toàn bộ bảng. Có thể update dựa trên subquery.
- **DELETE**: Tương tự UPDATE, cần WHERE. Sử dụng CASCADE nếu có FK.
- **Best practices**: Sử dụng transactions cho multiple operations, validate data trước khi insert/update, log changes cho audit.
- **Bulk operations**: INSERT với VALUES list hoặc SELECT từ bảng khác.
- **UPSERT**: INSERT ... ON CONFLICT UPDATE (PostgreSQL).

#### Bài tập (11-15)
11. Viết query INSERT user với RETURNING id.
12. Viết query INSERT multiple records từ array.
13. Viết query UPDATE user profile với WHERE.
14. Viết query UPDATE set is_deleted=true cho soft delete.
15. Viết transaction BEGIN/COMMIT cho insert user + profile.

### 3. Data Definition Language (DDL) - Ngôn ngữ định nghĩa dữ liệu
DDL dùng để định nghĩa và thay đổi cấu trúc database: tạo bảng, index, constraints, etc.

#### Lý thuyết
- **CREATE**: Tạo tables, indexes, views, functions.
- **ALTER**: Thay đổi cấu trúc: add/drop columns, change types, add constraints.
- **DROP**: Xóa objects. Sử dụng CASCADE cẩn thận.
- **Constraints**: PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, NOT NULL.
- **Indexes**: B-tree (default), Hash, GIN (for arrays/JSON). Tối ưu queries nhưng chậm writes.
- **Views**: Virtual tables, có thể update nếu simple.
- **UUID vs SERIAL**: UUID tốt cho distributed systems, tránh conflicts; SERIAL đơn giản hơn nhưng có thể leak info.

#### Bài tập (21-25)
21. Viết CREATE TABLE users với UUID, constraints.
22. Viết ALTER TABLE thêm cột avatar_url.
23. Viết CREATE INDEX trên email và user_id.
24. Viết CREATE VIEW user_activity với joins.
25. Viết ALTER TABLE ADD CHECK cho age.

### 4. Data Control Language (DCL) - Ngôn ngữ kiểm soát dữ liệu
DCL quản lý quyền truy cập và bảo mật.

#### Lý thuyết
- **GRANT**: Cấp quyền SELECT, INSERT, UPDATE, DELETE, etc. trên tables/views.
- **REVOKE**: Thu hồi quyền.
- **Roles**: Nhóm quyền, dễ quản lý.
- **Best practices**: Principle of least privilege, audit permissions.

#### Bài tập (26-27)
26. Viết GRANT SELECT, INSERT trên users cho app_user role.
27. Viết REVOKE DELETE permissions từ regular users, chỉ admin có.

### 5. Transaction Control Language (TCL) - Ngôn ngữ kiểm soát giao dịch
TCL quản lý transactions để đảm bảo ACID properties.

#### Lý thuyết
- **ACID**: Atomicity, Consistency, Isolation, Durability.
- **Isolation levels**: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE.
- **SAVEPOINT**: Điểm lưu trong transaction.
- **Best practices**: Sử dụng transactions cho related operations, handle deadlocks.

#### Bài tập (28-30)
28. Viết BEGIN/COMMIT cho create user + create wallet in one transaction.
29. Viết SAVEPOINT trong order processing, rollback payment if inventory fails.
30. Viết SET TRANSACTION ISOLATION LEVEL SERIALIZABLE for critical operations.

### 6. NoSQL (MongoDB) trong Backend Development
MongoDB là document-based NoSQL database phổ biến, phù hợp cho flexible schemas, high scalability, và real-time applications. Khác với SQL relational, MongoDB lưu data dưới dạng BSON documents trong collections, hỗ trợ nested structures và dynamic schemas.

#### Lý thuyết
- **Documents & Collections**: Documents là JSON objects, collections tương đương tables nhưng schemaless. Mỗi document có _id (ObjectId).
- **CRUD Operations**: 
  - Create: insertOne/insertMany
  - Read: find/findOne với query filters
  - Update: updateOne/updateMany với $set, $inc, etc.
  - Delete: deleteOne/deleteMany
- **Indexing**: Cải thiện performance queries. Types: single, compound, multikey (arrays), text, geospatial.
- **Aggregation Pipeline**: Stages như $match, $group, $sort, $project, $lookup (join). Powerful cho analytics.
- **Replication & Sharding**: Replica sets cho HA, sharding cho horizontal scaling.
- **Schema vs Schemaless**: Mongoose enforces schemas, validation; native driver flexible.
- **Data Modeling**: Embed vs Reference. Embed cho 1-1/many, reference cho large or frequently updated.
- **Best practices**: 
  - Index on query fields.
  - Avoid unbounded arrays.
  - Use TTL indexes cho auto-delete.
  - Monitor with MongoDB Atlas/Compass.
  - Backup with mongodump.

#### So sánh SQL vs NoSQL
- **SQL**: Structured, ACID, joins, normalized. Tốt cho complex queries, consistency.
- **NoSQL**: Flexible, scalable, fast writes, denormalized. Tốt cho big data, real-time, changing schemas.

#### Bài tập (31-40)
31. Viết insertOne với Mongoose schema validation, handle duplicate email.
32. Viết find với filtering (age range, city), sorting (name, createdAt), pagination.
33. Viết regex cho case-insensitive search, add fuzzy matching với text index.
34. Viết updateOne validate ownership, update only allowed fields.
35. Viết soft delete với isDeleted: true, override find để exclude deleted docs.
36. Viết aggregation pipeline group by month, count users per month.
37. Viết populate refs User -> Posts, Post -> Comments.
38. Viết create compound index (email, age), explain query performance.
39. Viết create text index trên name/description, search với $text.
40. Viết bulkWrite cho insert/update multiple, handle errors.

## Phần 2: Implement API (Backend Implementations)

### DQL APIs (6-10)
6. Implement API GET /users với pagination, trả về JSON.
7. Implement API GET /posts với JOIN, trả về posts với user info.
8. Implement API cho admin dashboard với aggregates.
9. Implement search API với LIKE.
10. Implement advanced filter & sort API.

### DML APIs (16-20)
16. Implement API POST /users với INSERT, validate input.
17. Implement bulk insert API từ CSV data.
18. Implement API PUT /users/:id với UPDATE, check ownership.
19. Implement upsert API cho sync data.
20. Implement API DELETE với soft delete và FK handling.

### NoSQL APIs (41-50)
41. Implement POST /users với insert, validation, error handling.
42. Implement GET /users với filtering, sorting, pagination.
43. Implement GET /users/search với regex và text search.
44. Implement PUT /users/:id với ownership check, update fields.
45. Implement DELETE /users/:id với soft delete.
46. Implement GET /users/stats với aggregation pipeline.
47. Implement GET /users/:id/posts với populate.
48. Implement POST /indexes để create indexes via API.
49. Implement GET /search với $text query.
50. Implement POST /bulk với bulkWrite operations.

## Lưu ý chung
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQL Tutorial](https://www.w3schools.com/sql/)
- [SQL Best Practices](https://www.sqlstyle.guide/)