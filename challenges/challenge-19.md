# Challenge 19: Scheduling Tasks với Node-Cron

## Mục tiêu
Học cách schedule recurring tasks trong Node.js.

## Yêu cầu
1. Cài đặt node-cron: `npm install node-cron`.
2. Tạo cron job để chạy task định kỳ (e.g., cleanup database, send reports).
3. Schedule job chạy mỗi phút, giờ, ngày.
4. Log execution và handle errors.

## Gợi ý
- Cron: `cron.schedule('0 0 * * *', () => { console.log('Daily task'); });`

## Kiểm tra
- Chạy app và chờ job execute, kiểm tra logs.

## Tài liệu tham khảo
- [node-cron](https://www.npmjs.com/package/node-cron)