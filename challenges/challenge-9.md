# Challenge 9: Deployment với Docker

## Mục tiêu
Học cách containerize ứng dụng Node.js sử dụng Docker và chạy nó.

## Yêu cầu
1. Tạo Dockerfile cho ứng dụng Node.js.
2. Tạo docker-compose.yml để chạy app với database (PostgreSQL hoặc MongoDB).
3. Build và run container: `docker-compose up`.
4. Kiểm tra app chạy trong container.

## Gợi ý
- Dockerfile cơ bản:
  ```
  FROM node:14
  WORKDIR /app
  COPY package*.json ./
  RUN npm install
  COPY . .
  EXPOSE 3000
  CMD ["npm", "start"]
  ```
- docker-compose.yml: Dịch vụ app và db.

## Kiểm tra
- Truy cập app qua localhost và kiểm tra database connection.

## Tài liệu tham khảo
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)