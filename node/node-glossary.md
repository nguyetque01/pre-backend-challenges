# Node.js Series Glossary: Khái Niệm, Thuật Ngữ, Công Cụ

Đây là danh sách các khái niệm, thuật ngữ, công cụ quan trọng trong series Node.js. Mỗi mục có mô tả ngắn gọn và link đến vị trí mô tả chi tiết trong các file. Danh sách sắp xếp theo alphabet để dễ tra cứu.

## A
- **API (Application Programming Interface)**: Giao diện cho phép ứng dụng giao tiếp, thường qua HTTP requests/responses. Ví dụ: RESTful API với endpoints như /users. [03-express-guide.md#phần-4-crud-operations---tạo-đọc-sửa-xóa](03-express-guide.md#phần-4-crud-operations---tạo-đọc-sửa-xóa)
- **Async/Await**: Cú pháp để xử lý promises dễ dàng. [02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait](02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait)
- **Authentication**: Xác thực người dùng. [03-express-guide.md#phần-6-nâng-cao---authentication-sessions-templates](03-express-guide.md#phần-6-nâng-cao---authentication-sessions-templates), [06-advanced-node-guide.md#chương-5-authentication--authorization](06-advanced-node-guide.md#chương-5-authentication--authorization)

## B
- **Backend**: Phần xử lý phía server. [00-how-websites-work.md#chương-2-các-nhiệm-vụ-cơ-bản-của-backend](00-how-websites-work.md#chương-2-các-nhiệm-vụ-cơ-bản-của-backend)
- **Buffers**: Xử lý dữ liệu nhị phân. [02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes](02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes)

## C
- **Callbacks**: Hàm được gọi sau khi task hoàn thành. [02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait](02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait)
- **Child Processes**: Chạy commands hoặc scripts con. [02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes](02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes), [05-node-operations-types.md](05-node-operations-types.md)
- **Client-Server Flow**: Mô hình giao tiếp client-server. [00-how-websites-work.md#chương-1-cơ-bản-về-website---mô-hình-client-server](00-how-websites-work.md#chương-1-cơ-bản-về-website---mô-hình-client-server)
- **Clusters**: Sử dụng nhiều CPU cores. [06-advanced-node-guide.md#chương-2-clusters---multi-core-processing](06-advanced-node-guide.md#chương-2-clusters---multi-core-processing)
- **CRUD Operations**: Create, Read, Update, Delete. [03-express-guide.md#phần-4-crud-operations---tạo-đọc-sửa-xóa](03-express-guide.md#phần-4-crud-operations---tạo-đọc-sửa-xóa)

## D
- **Database**: Lưu trữ dữ liệu. [04-node-databases-guide.md](04-node-databases-guide.md)
- **Deployment**: Triển khai app lên production. [06-advanced-node-guide.md#chương-7-deployment---chạy-production](06-advanced-node-guide.md#chương-7-deployment---chạy-production)

## E
- **Endpoints**: Điểm cuối của API. [03-express-guide.md#phần-3-routing---quản-lý-đường-dẫn](03-express-guide.md#phần-3-routing---quản-lý-đường-dẫn)
- **Error Handling**: Xử lý lỗi. [03-express-guide.md#phần-5-error-handling---xử-lý-lỗi](03-express-guide.md#phần-5-error-handling---xử-lý-lỗi)
- **Event Loop**: Vòng lặp xử lý events trong Node.js. [00-how-websites-work.md#chương-7-tại-sao-và-làm-thế-nào-chúng-làm-được](00-how-websites-work.md#chương-7-tại-sao-và-làm-thế-nào-chúng-làm-được), [02-node-basics-guide.md#phần-7-events---event-driven-programming](02-node-basics-guide.md#phần-7-events---event-driven-programming)
- **Events**: Sự kiện trong Node.js. [02-node-basics-guide.md#phần-7-events---event-driven-programming](02-node-basics-guide.md#phần-7-events---event-driven-programming), [05-node-operations-types.md](05-node-operations-types.md)
- **Express.js**: Framework cho Node.js. [00-how-websites-work.md#chương-5-expressjs-–-framework-xây-web-apps](00-how-websites-work.md#chương-5-expressjs-–-framework-xây-web-apps), [03-express-guide.md](03-express-guide.md)

## F
- **File System**: Xử lý files. [02-node-basics-guide.md#phần-4-file-system---đọcghi-files](02-node-basics-guide.md#phần-4-file-system---đọcghi-files), [05-node-operations-types.md](05-node-operations-types.md)

## G
- **Git**: Version control. [02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code](02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code)

## H
- **HTTP**: Giao thức truyền tải. [00-how-websites-work.md#chương-3-http-và-client-server-flow](00-how-websites-work.md#chương-3-http-và-client-server-flow), [02-node-basics-guide.md#phần-5-http-server---xây-dựng-web-server](02-node-basics-guide.md#phần-5-http-server---xây-dựng-web-server), [05-node-operations-types.md](05-node-operations-types.md)

## J
- **JSON**: Định dạng dữ liệu nhẹ, dễ đọc, dùng trao đổi giữa client-server. Ví dụ: {"name": "Alice", "age": 25}. [00-how-websites-work.md#chương-6-api-và-json-–-cơ-sở-giao-tiếp](00-how-websites-work.md#chương-6-api-và-json-–-cơ-sở-giao-tiếp)

## M
- **Middleware**: Hàm xử lý requests trong Express. [03-express-guide.md#phần-2-middleware---xử-lý-requests](03-express-guide.md#phần-2-middleware---xử-lý-requests)
- **Modules**: Chia code thành file. [02-node-basics-guide.md#phần-3-cơ-bản---modules-file-system-http](02-node-basics-guide.md#phần-3-cơ-bản---modules-file-system-http)
- **MongoDB**: NoSQL database. [04-node-databases-guide.md#phần-2-crud-với-mongodb---nosql](04-node-databases-guide.md#phần-2-crud-với-mongodb---nosql)

## N
- **Node.js**: Runtime JavaScript. [00-how-websites-work.md#chương-4-nodejs-–-mang-js-lên-server](00-how-websites-work.md#chương-4-nodejs-–-mang-js-lên-server), [01-node-vs-other-backends.md](01-node-vs-other-backends.md), [02-node-basics-guide.md](02-node-basics-guide.md)
- **Nodemon**: Auto-restart server. [02-node-basics-guide.md#nodemon-auto-restart-server](02-node-basics-guide.md#nodemon-auto-restart-server)

## O
- **ORMs**: Object-Relational Mappers. [04-node-databases-guide.md#phần-4-orms---sequelize-và-mongoose](04-node-databases-guide.md#phần-4-orms---sequelize-và-mongoose)

## P
- **Performance Tuning**: Tối ưu hiệu suất. [06-advanced-node-guide.md#chương-3-performance-tuning---tối-ưu-hiệu-suất](06-advanced-node-guide.md#chương-3-performance-tuning---tối-ưu-hiệu-suất)
- **Postman**: Tool test APIs. [02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code](02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code)
- **PostgreSQL**: SQL database. [04-node-databases-guide.md#phần-3-crud-với-postgresql---sql](04-node-databases-guide.md#phần-3-crud-với-postgresql---sql)
- **Promises**: Đối tượng xử lý async. [02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait](02-node-basics-guide.md#phần-6-asynchronous-programming---callbacks-promises-asyncawait)

## R
- **RESTful API**: API theo REST. [03-express-guide.md](03-express-guide.md)
- **Routing**: Định tuyến requests. [03-express-guide.md#phần-3-routing---quản-lý-đường-dẫn](03-express-guide.md#phần-3-routing---quản-lý-đường-dẫn)

## S
- **Security**: Bảo mật apps. [06-advanced-node-guide.md#chương-4-security---bảo-mật-apps](06-advanced-node-guide.md#chương-4-security---bảo-mật-apps)
- **Streams**: Xử lý dữ liệu lớn. [02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes](02-node-basics-guide.md#phần-8-nâng-cao---buffers-streams-child-processes), [06-advanced-node-guide.md#chương-1-streams---xử-lý-dữ-liệu-lớn](06-advanced-node-guide.md#chương-1-streams---xử-lý-dữ-liệu-lớn)
- **Swagger/OpenAPI**: Tài liệu API. [03-express-guide.md#phần-7-api-documentation-với-swaggeropenapi](03-express-guide.md#phần-7-api-documentation-với-swaggeropenapi)

## T
- **Testing**: Kiểm tra code. [06-advanced-node-guide.md#chương-6-testing---đảm-bảo-chất-lượng](06-advanced-node-guide.md#chương-6-testing---đảm-bảo-chất-lượng)

## V
- **VS Code**: Editor phổ biến. [02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code](02-node-basics-guide.md#tools-hỗ-trợ-git-postman-vs-code)

## W
- **WebSockets**: Real-time communication. [06-advanced-node-guide.md#chương-10-real-time-apps---websockets](06-advanced-node-guide.md#chương-10-real-time-apps---websockets)

*Ghi chú: Links có thể cần điều chỉnh nếu cấu trúc file thay đổi. Sử dụng Ctrl+Click trong VS Code để nhảy đến phần.*