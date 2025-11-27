# Challenge 5: Giới thiệu MongoDB

## Mục tiêu
Làm quen với NoSQL database MongoDB.

## Yêu cầu
1. Cài đặt MongoDB và MongoDB Compass.
2. Tạo database 'testdb' và collection 'users'.
3. Thực hiện CRUD operations:
   - Insert: Thêm một document {name: 'Alice', age: 30}.
   - Find: Lấy tất cả documents.
   - Update: Cập nhật age của Alice thành 31.
   - Delete: Xóa document của Alice.

## Bài tập bổ sung
1. **Insert nhiều documents**: Thêm vài users với fields khác nhau.
2. **Query với filter**: Tìm users có age > 25.
3. **Projection**: Lấy chỉ name và age của users.
4. **Update nhiều**: Tăng age của tất cả users lên 1.
5. **Indexing**: Tạo index trên field name và query performance.
6. **Aggregation**: Tính average age của users.

## Gợi ý
- Sử dụng MongoDB Compass GUI hoặc mongo shell.
- Commands: `db.users.insertOne({...})`, `db.users.find()`, `db.users.updateOne({...})`, `db.users.deleteOne({...})`.
- Insert nhiều: `db.users.insertMany([{...}, {...}]);`
- Filter: `db.users.find({age: {$gt: 25}});`
- Projection: `db.users.find({}, {name: 1, age: 1, _id: 0});`
- Update nhiều: `db.users.updateMany({}, {$inc: {age: 1}});`
- Index: `db.users.createIndex({name: 1});`
- Aggregation: `db.users.aggregate([{$group: {_id: null, avgAge: {$avg: '$age'}}}]);`

## Kiểm tra
- Kiểm tra collection sau mỗi operation.

## Tài liệu tham khảo
- [MongoDB CRUD](https://docs.mongodb.com/manual/crud/)