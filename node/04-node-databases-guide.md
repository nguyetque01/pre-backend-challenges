# Hướng Dẫn Node.js Với Databases: Kết Nối Dữ Liệu Cho Apps

## Giới Thiệu: Databases Với Node.js Là Gì?
Node.js kết hợp với databases như "não bộ" cho apps: Lưu trữ, truy vấn dữ liệu. Có thể dùng SQL (PostgreSQL, MySQL) hoặc NoSQL (MongoDB). Node.js mạnh với async I/O, phù hợp queries database.

### Tại Sao Thú Vị?
- **Async queries**: Không block app.
- **ORMs**: Sequelize, Mongoose dễ dùng.
- **Ví dụ vui**: Tưởng tượng Node như đầu bếp, database như tủ lạnh: Lấy nguyên liệu nhanh!

### Khi Nào Dùng?
- Apps cần persist data.
- User accounts, posts, etc.

## Mục Lục
- [Giới Thiệu: Databases Với Node.js Là Gì?](#giới-thiệu-databases-với-nodejs-là-gì)
- [Phần 1: Cơ Bản - Kết Nối Database](#phần-1-cơ-bản---kết-nối-database)
- [Phần 2: CRUD Với MongoDB - NoSQL](#phần-2-crud-với-mongodb---nosql)
- [Phần 3: CRUD Với PostgreSQL - SQL](#phần-3-crud-với-postgresql---sql)
- [Phần 4: ORMs - Sequelize Và Mongoose](#phần-4-orms---sequelize-và-mongoose)
- [Phần 5: Authentication - Bảo Mật Apps](#phần-5-authentication---bảo-mật-apps)
- [Phần 6: Nâng Cao - Caching, Pagination, Testing](#phần-6-nâng-cao---caching-pagination-testing)
- [Lưu Ý Cho Người Mới Học Node + DB](#lưu-ý-cho-người-mới-học-node--db)
- [Tổng Kết](#tổng-kết)

## Phần 1: Cơ Bản - Kết Nối Database

### Kết Nối Là Gì?
Kết nối như "đường ống": Gửi queries từ Node đến DB.

#### Ví Dụ Thú Vị: Connect MongoDB
- **MongoDB**:
  ```javascript
  const mongoose = require('mongoose');
  mongoose.connect('mongodb://localhost:27017/myapp');
  ```

- **PostgreSQL**:
  ```javascript
  const { Client } = require('pg');
  const client = new Client();
  client.connect();
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Install drivers**: npm install mongoose pg.
2. **Connect MongoDB**: Local MongoDB.
3. **Connect PostgreSQL**: Local Postgres.
4. **Connection string**: mongodb://user:pass@host/db.
5. **Environment vars**: process.env.DB_URL.
6. **Connection pool**: pg.Pool.
7. **Error handling**: on('error').
8. **Disconnect**: mongoose.disconnect().
9. **Multiple DBs**: Connect to test/prod.
10. **Docker DB**: Run DB in container.

## Phần 2: CRUD Với MongoDB - NoSQL

### MongoDB Là Gì?
MongoDB như "tủ linh hoạt": Documents JSON.

#### Ví Dụ Thú Vị: User Management
- **Schema**:
  ```javascript
  const userSchema = new mongoose.Schema({
    name: String,
    email: String
  });
  const User = mongoose.model('User', userSchema);
  ```

- **Create**:
  ```javascript
  const user = new User({ name: 'Alice', email: 'alice@example.com' });
  await user.save();
  ```

#### Bài Tập Thực Hành
1. **Define schema**: User with name, email.
2. **Create user**: new User().save().
3. **Read all**: User.find().
4. **Read one**: User.findById(id).
5. **Update**: User.findByIdAndUpdate().
6. **Delete**: User.findByIdAndDelete().
7. **Validation**: required: true.
8. **Middleware**: pre('save').
9. **Populate**: ref to other models.
10. **Indexes**: schema.index({ email: 1 }).

## Phần 3: CRUD Với PostgreSQL - SQL

### PostgreSQL Là Gì?
PostgreSQL như "bảng tính thông minh": Quan hệ, ACID.

#### Ví Dụ Thú Vị: Post Management
- **Query**:
  ```javascript
  const res = await client.query('INSERT INTO users (name, email) VALUES ($1, $2)', ['Alice', 'alice@example.com']);
  ```

#### Bài Tập Thực Hành
1. **Create table**: client.query(CREATE TABLE).
2. **Insert**: INSERT INTO.
3. **Select**: SELECT * FROM.
4. **Update**: UPDATE SET.
5. **Delete**: DELETE FROM.
6. **Prepared statements**: $1, $2.
7. **Transactions**: BEGIN, COMMIT.
8. **Joins**: INNER JOIN.
9. **Pool queries**: pool.query().
10. **Migrations**: node-pg-migrate.

## Phần 4: ORMs - Sequelize Và Mongoose

### ORMs Là Gì?
ORMs như "dịch giả": Code thay vì raw SQL.

#### Sequelize (SQL):
```javascript
const User = sequelize.define('User', { name: DataTypes.STRING });
await User.create({ name: 'Alice' });
```

#### Mongoose (NoSQL):
```javascript
const user = await User.findOne({ name: 'Alice' });
```

#### Bài Tập Thực Hành
1. **Sequelize setup**: npm install sequelize pg.
2. **Define model**: sequelize.define().
3. **Sync DB**: sequelize.sync().
4. **CRUD with Sequelize**: create, findAll.
5. **Associations**: hasMany, belongsTo.
6. **Migrations**: sequelize-cli.
7. **Mongoose setup**: npm install mongoose.
8. **Schema**: new Schema().
9. **Model methods**: static/instance.
10. **Plugins**: mongoose-paginate.

## Phần 5: Authentication - Bảo Mật Apps

### Auth Là Gì?
Auth như "chìa khóa": Đăng nhập, bảo vệ routes.

#### Ví Dụ Thú Vị: JWT Auth
- **Register**:
  ```javascript
  const token = jwt.sign({ id: user.id }, 'secret');
  ```

- **Middleware**:
  ```javascript
  const auth = (req, res, next) => {
    const token = req.header('Authorization');
    req.user = jwt.verify(token, 'secret');
    next();
  };
  ```

#### Bài Tập Thực Hành
1. **Hash password**: bcrypt.
2. **JWT sign**: jsonwebtoken.
3. **Login route**: Check password, return token.
4. **Protect routes**: auth middleware.
5. **Refresh token**: Separate refresh logic.
6. **Sessions**: express-session with DB.
7. **OAuth**: Passport.js.
8. **Roles**: Admin, user permissions.
9. **Password reset**: Email tokens.
10. **Rate limiting**: express-rate-limit.

## Phần 6: Nâng Cao - Caching, Pagination, Testing

### Caching: Tăng Tốc
Caching như "bộ nhớ nhanh": Redis.

#### Pagination: Phân Trang
Pagination như "sách nhiều trang".

#### Testing: Đảm Bảo Chất Lượng
Testing như "kiểm tra": Jest, Supertest.

#### Bài Tập Thực Hành
1. **Redis setup**: npm install redis.
2. **Cache queries**: set/get.
3. **Pagination**: limit, offset.
4. **Cursor pagination**: for large data.
5. **Jest setup**: npm install jest.
6. **Unit tests**: Test functions.
7. **Integration tests**: Supertest for routes.
8. **Mock DB**: mongodb-memory-server.
9. **CI/CD**: GitHub Actions.
10. **Performance**: Benchmark queries.

## Lưu Ý Cho Người Mới Học Node + DB
- **Bắt đầu với basics**: Connect, CRUD.
- **Thử với local DB**: MongoDB Compass, pgAdmin.
- **Practive với projects**: Build user API.
- **Đọc docs vui**: [Mongoose docs](https://mongoosejs.com/), [Sequelize docs](https://sequelize.org/).
- **Lỗi thường gặp**: Forget await, connection errors.

## Tổng Kết
Hướng dẫn này đã hướng dẫn kết nối Node.js với databases: MongoDB, PostgreSQL, ORMs, auth, caching, testing. Bạn giờ có thể xây dựng apps data-driven. Thực hành để củng cố!

Node + DB như sức mạnh backend! Khi master, bạn xây apps data-driven. Chúc học vui!</content>
<parameter name="filePath">d:\WorkSpace\Books\Pre-Backend-Challenges\node\04-node-databases-guide.md