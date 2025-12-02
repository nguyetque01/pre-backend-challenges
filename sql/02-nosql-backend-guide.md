# Hướng Dẫn MongoDB Cho Người Mới: NoSQL Thú Vị Và Linh Hoạt

## Giới Thiệu: MongoDB Là Gì?
MongoDB là một loại database NoSQL, nghĩa là "không phải SQL". Thay vì dùng bảng như Excel, MongoDB dùng "documents" như những tờ giấy ghi chú linh hoạt. Mỗi document là một object JSON (như JavaScript object), có thể chứa text, số, mảng, thậm chí object con.

### Tại Sao MongoDB Thú Vị?
- **Linh hoạt như tủ đồ**: Bạn có thể bỏ gì cũng được, thêm ngăn mới bất kỳ lúc nào. Không cần thiết kế sẵn như tủ gỗ cứng.
- **Nhanh cho dữ liệu lớn**: Dễ mở rộng, phù hợp app có hàng triệu users như Facebook.
- **Dễ dùng với code**: JSON giống JavaScript, nên dev backend thích.
- **Ví dụ vui**: Tưởng tượng user profile: Bạn có thể thêm "sở thích: ['coding', 'gaming']" mà không cần xin phép database!

### Khi Nào Dùng MongoDB?
- App cần thay đổi dữ liệu thường xuyên (social media, e-commerce).
- Dữ liệu không đồng nhất (mỗi user có thông tin khác nhau).
- Cần tốc độ cao cho đọc/ghi.

## Mục Lục
- [Phần 1: Cơ Bản - CRUD Operations (Tạo, Đọc, Sửa, Xóa)](#phần-1-cơ-bản---crud-operations-tạo-đọc-sửa-xóa)
- [Phần 2: Tìm Kiếm Dữ Liệu - Querying Documents](#phần-2-tìm-kiếm-dữ-liệu---querying-documents)
- [Phần 3: Xử Lý Dữ Liệu Nâng Cao - Aggregation Framework](#phần-3-xử-lý-dữ-liệu-nâng-cao---aggregation-framework)
- [Phần 4: Tăng Tốc - Indexing](#phần-4-tăng-tốc---indexing)
- [Phần 5: Thiết Kế Dữ Liệu - Data Modeling](#phần-5-thiết-kế-dữ-liệu---data-modeling)
- [Lưu Ý Cho Người Mới Học MongoDB](#lưu-ý-cho-người-mới-học-mongodb)

## Phần 1: Cơ Bản - CRUD Operations (Tạo, Đọc, Sửa, Xóa)

### CRUD Là Gì?
CRUD là viết tắt của Create (tạo), Read (đọc), Update (sửa), Delete (xóa). Đây là 4 thao tác cơ bản với dữ liệu.

#### Ví Dụ Thú Vị: Quản Lý Users Trong App Blog
Giả sử bạn làm app blog CMS. Users có thể đăng ký với name, email, và sở thích linh hoạt.

- **Create**: Thêm user mới.
  ```
  db.users.insertOne({
    name: "Alice",
    email: "alice@example.com",
    hobbies: ["reading", "coding"],
    joinedAt: new Date()
  })
  ```

- **Read**: Tìm user theo email.
  ```
  db.users.findOne({email: "alice@example.com"})
  ```

- **Update**: Thêm sở thích mới.
  ```
  db.users.updateOne(
    {email: "alice@example.com"},
    {$push: {hobbies: "traveling"}}
  )
  ```

- **Delete**: Xóa user (soft delete bằng cách thêm flag).
  ```
  db.users.updateOne(
    {email: "alice@example.com"},
    {$set: {isDeleted: true}}
  )
  ```

#### Bài Tập Thực Hành Cho Người Mới
1. **Tạo collection users**: Trong MongoDB shell hoặc Compass, tạo collection `users`.
2. **Thêm user đầu tiên**: Insert document với name, email, và một hobby bất kỳ. Xem kết quả.
3. **Tìm user**: Find user vừa tạo bằng email.
4. **Cập nhật user**: Thêm một hobby mới vào mảng hobbies.
5. **Xóa user**: Update để set isDeleted: true (soft delete).
6. **Thử bulk insert**: Thêm 3 users cùng lúc với insertMany.
7. **Tìm với điều kiện**: Find users có hobby "coding".
8. **Update nhiều**: Thêm field "level": "beginner" cho tất cả users.
9. **Delete thật**: Xóa hẳn một user (dùng deleteOne).
10. **Kiểm tra dữ liệu**: Dùng find() để xem tất cả users còn lại.

## Phần 2: Tìm Kiếm Dữ Liệu - Querying Documents

### Tìm Kiếm Linh Hoạt
MongoDB có nhiều "operators" (toán tử) để tìm kiếm thông minh, như tìm số lớn hơn, text chứa từ, hoặc trong mảng.

#### Ví Dụ Thú Vị: Tìm Posts Trong Blog
Posts có tags (như ['tech', 'javascript']), published date, và author.

- Tìm posts có tag "tech":
  ```
  db.posts.find({tags: "tech"})
  ```

- Tìm posts published sau 2023:
  ```
  db.posts.find({publishedAt: {$gte: new Date("2023-01-01")}})
  ```

- Tìm posts có cả "tech" và "javascript":
  ```
  db.posts.find({tags: {$all: ["tech", "javascript"]}})
  ```

- Tìm posts không có author:
  ```
  db.posts.find({author: {$exists: false}})
  ```

#### Bài Tập Thực Hành
1. **Tạo posts**: Insert 5 posts với title, content, tags (mảng), publishedAt.
2. **Tìm theo tag**: Find posts có tag "news".
3. **Tìm theo ngày**: Find posts published trong tháng này.
4. **Tìm với AND**: Posts có tag "tech" và author là "Alice".
5. **Tìm với OR**: Posts có tag "news" hoặc "sports".
6. **Tìm trong mảng**: Posts có ít nhất một tag trong ["tech", "coding"].
7. **Tìm text**: Nếu có text index, tìm posts chứa "tutorial".
8. **Tìm với regex**: Posts title bắt đầu bằng "How to".
9. **Tìm nested**: Posts có metadata.featured = true.
10. **Pagination**: Dùng limit(5).skip(0) để lấy 5 posts đầu.

## Phần 3: Xử Lý Dữ Liệu Nâng Cao - Aggregation Framework

### Aggregation Là Gì?
Aggregation như một "dây chuyền sản xuất" để xử lý dữ liệu: lọc, nhóm, tính toán, sắp xếp. Dùng cho báo cáo, thống kê.

#### Ví Dụ Thú Vị: Thống Kê Blog
Tính số posts per user, top tags, etc.

- Đếm posts per user:
  ```
  db.posts.aggregate([
    {$group: {_id: "$author", count: {$sum: 1}}},
    {$sort: {count: -1}}
  ])
  ```

- Top 5 tags phổ biến:
  ```
  db.posts.aggregate([
    {$unwind: "$tags"},
    {$group: {_id: "$tags", count: {$sum: 1}}},
    {$sort: {count: -1}},
    {$limit: 5}
  ])
  ```

- Thống kê monthly posts:
  ```
  db.posts.aggregate([
    {$group: {
      _id: {$month: "$publishedAt"},
      count: {$sum: 1}
    }}
  ])
  ```

#### Bài Tập Thực Hành
1. **Group cơ bản**: Aggregate để đếm số posts per author.
2. **Unwind mảng**: Tách tags và đếm mỗi tag xuất hiện bao lần.
3. **Filter trước**: Match posts published, rồi group.
4. **Tính trung bình**: Avg likes per post.
5. **Join với lookup**: Lookup author info từ users collection.
6. **Sort và limit**: Top 10 authors theo số posts.
7. **Date operations**: Group theo năm/tháng.
8. **Conditional**: Đếm posts có > 10 likes.
9. **Multiple stages**: Match -> group -> project (chọn fields).
10. **Complex pipeline**: Tạo báo cáo dashboard với nhiều metrics.

## Phần 4: Tăng Tốc - Indexing

### Indexing Như Gì?
Index như mục lục sách: Giúp tìm nhanh mà không đọc toàn bộ. Không index thì query chậm như tìm kim trong bể cỏ.

#### Ví Dụ Thú Vị: Tìm User Nhanh
- Index trên email: Tìm user theo email siêu nhanh.
- Compound index: Trên email + name cho queries phức tạp.
- Text index: Tìm kiếm full-text trong content.

#### Bài Tập Thực Hành
1. **Tạo index đơn**: Index trên email trong users.
2. **Xem indexes**: Dùng getIndexes() để kiểm tra.
3. **Compound index**: Index trên author + publishedAt.
4. **Unique index**: Index unique trên email.
5. **Text index**: Index text trên post content, rồi tìm "tutorial".
6. **TTL index**: Index trên session expiry để tự xóa.
7. **Partial index**: Index chỉ cho posts published.
8. **Geospatial index**: Nếu có location, index 2dsphere.
9. **Analyze**: Dùng explain() để xem query dùng index không.
10. **Drop index**: Xóa index không dùng để tiết kiệm dung lượng.

## Phần 5: Thiết Kế Dữ Liệu - Data Modeling

### Modeling Như Thiết Kế Nhà
Quyết định embed (gộp vào) hay reference (liên kết) data. Như thiết kế nhà: Phòng nào gộp, phòng nào riêng.

#### Ví Dụ Thú Vị: Blog CMS
- **Embed**: Comments trong post (vì đọc cùng lúc).
- **Reference**: Author reference đến users (vì author info thay đổi).

#### Bài Tập Thực Hành
1. **Embed đơn giản**: Post với embedded author info.
2. **Reference cơ bản**: Post reference author _id.
3. **One-to-many**: User với embedded posts (nếu ít posts).
4. **Many-to-many**: Posts với tags array.
5. **Hybrid**: Embed comments, reference author.
6. **Denormalize**: Lưu author name trong post để query nhanh.
7. **Schema validation**: Thêm JSON schema cho users.
8. **Migration**: Chuyển từ embed sang reference.
9. **Backup**: Dump database với mongodump.
10. **Restore**: Restore từ backup.

## Tổng Kết

Trong hướng dẫn này, chúng ta đã khám phá MongoDB, một cơ sở dữ liệu NoSQL linh hoạt và mạnh mẽ cho backend development.

**Điểm Chính:**
- **CRUD Operations**: Cơ bản tạo, đọc, sửa, xóa documents.
- **Querying**: Tìm kiếm linh hoạt với operators và conditions.
- **Aggregation**: Xử lý dữ liệu nâng cao cho báo cáo và thống kê.
- **Indexing**: Tăng tốc queries với indexes.
- **Data Modeling**: Thiết kế embed vs reference cho hiệu quả.

**Lời Khuyên:** Bắt đầu với CRUD và querying, rồi học aggregation và indexing. Thử nghiệm với MongoDB Compass và xây dựng projects nhỏ để thực hành. MongoDB phù hợp cho apps cần linh hoạt và mở rộng.

## Lưu Ý Cho Người Mới Học MongoDB
- **Bắt đầu với CRUD**: Học insert, find, update, delete trước.
- **Thử với MongoDB Compass**: GUI dễ dùng hơn shell.
- **Practive với data thực**: Tạo app blog nhỏ để thực hành.
- **Đọc docs vui**: [MongoDB University](https://university.mongodb.com/) có khóa miễn phí.
- **Lỗi thường gặp**: Nhớ _id là ObjectId, dùng new Date() cho dates.

MongoDB thú vị vì linh hoạt! Khi quen, bạn có thể xây app động như mạng xã hội. Chúc học vui!