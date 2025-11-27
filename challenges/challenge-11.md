# Challenge 11: GraphQL API

## Mục tiêu
Học cách xây dựng API sử dụng GraphQL thay vì REST.

## Yêu cầu
1. Cài đặt Apollo Server: `npm install apollo-server graphql`.
2. Định nghĩa GraphQL schema cho users (type User, Query, Mutation).
3. Implement resolvers để query và mutate data (sử dụng data in-memory hoặc database).
4. Tạo server và test queries trong GraphQL Playground.

## Gợi ý
- Schema:
  ```
  type User { id: ID!, name: String, email: String }
  type Query { users: [User] }
  type Mutation { createUser(name: String, email: String): User }
  ```
- Resolver: `users: () => usersData`

## Kiểm tra
- Truy cập /graphql và chạy queries như { users { name email } }

## Tài liệu tham khảo
- [GraphQL Documentation](https://graphql.org/learn/)
- [Apollo Server](https://www.apollographql.com/docs/apollo-server/)