# Hướng Dẫn Chi Tiết Express.js Với TypeScript Từ Cơ Bản Đến Nâng Cao

## 1. Giới Thiệu

### 1.1 Express.js là gì?

- **Express.js** là một framework web cho Node.js, cung cấp một tập hợp các tính năng mạnh mẽ để xây dựng các ứng dụng web và API.
- Được sử dụng rộng rãi để xây dựng các ứng dụng web do tính đơn giản và linh hoạt của nó.

### 1.2 Tại sao nên sử dụng TypeScript với Express.js?

- **TypeScript** cung cấp khả năng kiểm tra kiểu tĩnh, giúp giảm thiểu lỗi trong quá trình phát triển.
- Hỗ trợ các tính năng nâng cao như IntelliSense, giúp lập trình viên viết mã chính xác và nhanh hơn.
- Dễ dàng phát triển và bảo trì các dự án lớn.

### 1.3 Thiết lập dự án Express.js với TypeScript

- Cài đặt Node.js và npm.
- Khởi tạo dự án Node.js mới với TypeScript: `npm init -y` và `npm install typescript --save-dev`.
- Cấu hình TypeScript bằng cách tạo tệp `tsconfig.json` với cấu hình cơ bản.
- Cài đặt Express và các gói cần thiết: `npm install express @types/express`.

## 2. Tạo Ứng Dụng Express.js Cơ Bản

### 2.1 Tạo Server Đầu Tiên

- Tạo tệp `src/index.ts` và viết mã để khởi tạo một server Express.js cơ bản.
- Sử dụng phương thức `app.get()` để xử lý yêu cầu GET tại route `/`.
- Khởi động server bằng cách sử dụng `app.listen()`.

```typescript
import express, { Request, Response } from "express";

const app = express();
const port = 3000;

app.get("/", (req: Request, res: Response) => {
  res.send("Hello, Express with TypeScript!");
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

### 2.2 Sử Dụng Middleware

- Middleware là các hàm được thực thi trong chuỗi xử lý yêu cầu.
- Tạo một middleware đơn giản để log thông tin của mỗi yêu cầu.

```typescript
app.use((req: Request, res: Response, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

## 3. Quản Lý Route

### 3.1 Route Cơ Bản

- Tạo các route để xử lý các yêu cầu HTTP khác nhau như `GET`, `POST`, `PUT`, `DELETE`.
- Tách route thành các module riêng biệt để dễ quản lý.

```typescript
// Tệp src/routes/users.ts
import { Router, Request, Response } from "express";

const router = Router();

router.get("/users", (req: Request, res: Response) => {
  res.send("List of users");
});

router.post("/users", (req: Request, res: Response) => {
  res.send("Create a new user");
});

export default router;
```

### 3.2 Route Với Tham Số Động

- Sử dụng route động để xử lý các URL có tham số.

```typescript
router.get("/users/:id", (req: Request, res: Response) => {
  const userId = req.params.id;
  res.send(`User ID: ${userId}`);
});
```

### 3.3 Sử Dụng express.Router()

- Sử dụng `express.Router()` để tách các route theo module và tổ chức code gọn gàng hơn.
- Kết nối các module route với ứng dụng chính.

```typescript
import userRoutes from "./routes/users";

app.use("/api", userRoutes);
```

## 4. Làm Việc Với Dữ Liệu

### 4.1 Nhận Dữ Liệu Từ Request

- Sử dụng `req.body` để lấy dữ liệu từ yêu cầu POST (cần sử dụng middleware `express.json()`).
- Sử dụng `req.query` và `req.params` để lấy dữ liệu từ query string và tham số động.

### 4.2 Gửi Phản Hồi

- Sử dụng `res.send()` để gửi dữ liệu dạng văn bản hoặc JSON.
- Sử dụng `res.status()` để thiết lập mã trạng thái HTTP.

```typescript
app.post("/users", (req: Request, res: Response) => {
  const userData = req.body;
  res.status(201).json(userData);
});
```

## 5. Xử Lý Lỗi

### 5.1 Middleware Xử Lý Lỗi

- Tạo middleware để xử lý các lỗi phát sinh trong quá trình xử lý yêu cầu.
- Sử dụng `next(error)` để chuyển lỗi tới middleware xử lý lỗi.

```typescript
app.use((err: Error, req: Request, res: Response, next) => {
  console.error(err.message);
  res.status(500).send("Internal Server Error");
});
```

### 5.2 Xử Lý Lỗi 404

- Tạo middleware để xử lý các yêu cầu không tìm thấy (404 Not Found).

```typescript
app.use((req: Request, res: Response) => {
  res.status(404).send("Page Not Found");
});
```

## 6. Bảo Mật Ứng Dụng

### 6.1 Sử Dụng Helmet

- Sử dụng middleware `helmet` để bảo vệ ứng dụng khỏi các lỗ hổng bảo mật phổ biến.

```typescript
import helmet from "helmet";
app.use(helmet());
```

### 6.2 CORS

- Cấu hình CORS (Cross-Origin Resource Sharing) để kiểm soát truy cập từ các domain khác.

```typescript
import cors from "cors";
app.use(cors());
```

## 7. Testing Với Express.js

### 7.1 Viết Test Cho Các Route

- Sử dụng `supertest` và `jest` để viết và chạy các test cho các route trong ứng dụng.

```typescript
import request from "supertest";
import app from "./app";

describe("GET /", () => {
  it("should return a 200 status and a message", async () => {
    const response = await request(app).get("/");
    expect(response.status).toBe(200);
    expect(response.text).toBe("Hello, Express with TypeScript!");
  });
});
```

## 8. Tối Ưu Hóa và Deploy

### 8.1 Tối Ưu Hóa Hiệu Suất

- Sử dụng các kỹ thuật tối ưu hóa như nén phản hồi bằng `compression` và caching.
- Tối ưu hóa truy vấn cơ sở dữ liệu và giảm thiểu số lượng yêu cầu không cần thiết.

### 8.2 Deploy Ứng Dụng

- Hướng dẫn deploy ứng dụng Express.js lên các dịch vụ cloud như Heroku hoặc Vercel.
- Cấu hình các biến môi trường và thiết lập cơ sở dữ liệu trong môi trường sản xuất.
