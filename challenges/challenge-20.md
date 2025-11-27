# Challenge 20: WebSockets với Socket.io

## Mục tiêu
Học cách implement real-time communication với WebSockets.

## Yêu cầu
1. Cài đặt Socket.io: `npm install socket.io`.
2. Tạo server Socket.io và integrate với Express.
3. Implement chat room hoặc real-time notifications.
4. Handle connections, disconnections, và emit events.

## Gợi ý
- Server: `const io = require('socket.io')(server);`
- Client events: `io.on('connection', (socket) => { socket.on('message', (msg) => { io.emit('message', msg); }); });`

## Kiểm tra
- Mở multiple browser tabs và test chat.

## Tài liệu tham khảo
- [Socket.io](https://socket.io/)