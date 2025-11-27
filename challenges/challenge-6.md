# Challenge 6: API với MongoDB

## Mục tiêu
Xây dựng RESTful API sử dụng Express và Mongoose.

## Yêu cầu
1. Cài đặt mongoose: `npm install mongoose`.
2. Tạo model User với schema: name (String), email (String), age (Number).
3. Tạo routes:
   - GET /users: Lấy tất cả users.
   - POST /users: Thêm user mới.
   - PUT /users/:id: Cập nhật user.
   - DELETE /users/:id: Xóa user.
4. Kết nối MongoDB và chạy server.

## Bài tập bổ sung
1. **Validation**: Thêm validation cho email (unique, format) và age (min 0).
2. **Middleware**: Thêm pre-save middleware để log khi save user.
3. **Error handling**: Wrap routes trong try-catch, trả về proper error responses.
4. **Pagination**: Thêm query params page và limit cho GET /users.
5. **Search**: Thêm query param search để tìm users theo name.
6. **Populate**: Tạo model Post liên kết với User, và populate trong GET.

## Gợi ý
- Model: `const User = mongoose.model('User', userSchema);`
- Routes: Sử dụng app.post, app.get, etc.
- Kết nối: `mongoose.connect('mongodb://localhost/testdb');`
- Validation: `email: {type: String, required: true, unique: true, match: /.+\@.+\..+/}`
- Middleware: `userSchema.pre('save', function(next) { console.log('Saving user'); next(); });`
- Error: `try { ... } catch (err) { res.status(500).json({error: err.message}); }`
- Pagination: `const page = parseInt(req.query.page) || 1; const limit = parseInt(req.query.limit) || 10; const users = await User.find().skip((page-1)*limit).limit(limit);`
- Search: `const users = await User.find({name: new RegExp(req.query.search, 'i')});`
- Populate: Tạo Post model với user: {type: mongoose.Schema.Types.ObjectId, ref: 'User'}, sau đó `await Post.find().populate('user');`

## Kiểm tra
- Test API với Postman hoặc curl.

## Tài liệu tham khảo
- [Mongoose Guide](https://mongoosejs.com/docs/guide.html)