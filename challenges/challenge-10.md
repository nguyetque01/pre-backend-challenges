# Challenge 10: Caching với Redis

## Mục tiêu
Học cách sử dụng Redis để cache dữ liệu và cải thiện performance.

## Yêu cầu
1. Cài đặt Redis server locally hoặc sử dụng Docker.
2. Cài đặt package: `npm install redis`.
3. Tạo middleware caching cho API endpoints (ví dụ: cache kết quả GET users).
4. Implement cache invalidation khi dữ liệu thay đổi.

## Gợi ý
- Kết nối Redis: `const redis = require('redis'); const client = redis.createClient();`
- Set cache: `client.setex(key, 3600, JSON.stringify(data));`
- Get cache: `client.get(key, (err, data) => { if (data) return JSON.parse(data); });`

## Kiểm tra
- Gọi API nhiều lần và kiểm tra thời gian response (có cache vs không cache).

## Tài liệu tham khảo
- [Redis Documentation](https://redis.io/documentation)
- [Node Redis](https://www.npmjs.com/package/redis)