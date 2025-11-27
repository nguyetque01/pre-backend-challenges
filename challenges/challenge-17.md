# Challenge 17: File Upload với Multer

## Mục tiêu
Học cách handle file uploads trong Express app.

## Yêu cầu
1. Cài đặt Multer: `npm install multer`.
2. Tạo route POST /upload để upload files.
3. Configure storage (disk hoặc memory).
4. Validate file types và sizes.
5. Lưu file info vào database.

## Gợi ý
- Multer: `const upload = multer({ dest: 'uploads/' });`
- Route: `app.post('/upload', upload.single('file'), (req, res) => { ... });`

## Kiểm tra
- Upload file qua Postman và kiểm tra folder uploads.

## Tài liệu tham khảo
- [Multer](https://www.npmjs.com/package/multer)