# 🎓 CLB Vui Học Thông Minh - Backend System

![NestJS](https://img.shields.io/badge/nestjs-%23E0234E.svg?style=for-the-badge&logo=nestjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

> **Lưu ý:** Dự án này được thiết kế theo tiêu chuẩn **Production-ready** nhằm mục đích học tập và nghiên cứu chuyên sâu về kiến trúc Backend hiện đại (2025).

## 📖 Giới thiệu (Introduction)

Đây là hệ thống Backend (API) cho nền tảng E-learning **CLB Vui Học Thông Minh**. Dự án được xây dựng với kiến trúc **Modular Monolith** sử dụng **NestJS**, hướng tới khả năng mở rộng (scalability), dễ bảo trì (maintainability) và hiệu năng cao (performance).

Hệ thống cung cấp đầy đủ các tính năng cho một nền tảng giáo dục trực tuyến: quản lý khóa học, bài tập, chấm điểm, bảng xếp hạng và phân quyền người dùng chi tiết.

🔗 **Frontend Repository:** [clbvuihocthongminh-frontend](https://github.com/nghiacd06/clbvuihocthongminh)
🔗 **Live API:** `https://api.clbvuihocthongminh.com` (Coming soon)

---

## 🛠 Công nghệ sử dụng (Tech Stack)

Dự án áp dụng các công nghệ và thư viện chuẩn mực của ngành (Industry Standard) trong năm 2025:

| Hạng mục             | Công nghệ             | Lý do lựa chọn (Design Decision)                                                     |
| :------------------- | :-------------------- | :----------------------------------------------------------------------------------- |
| **Core Framework**   | **NestJS 10+**        | Framework số 1 cho Node.js Enterprise. Cấu trúc rõ ràng, hỗ trợ TypeScript tốt nhất. |
| **Language**         | **TypeScript 5.x**    | Type-safety, giảm thiểu lỗi runtime, DX (Developer Experience) tuyệt vời.            |
| **Database**         | **PostgreSQL 16**     | RDBMS mạnh mẽ, ổn định, hỗ trợ JSONB và các tính năng nâng cao.                      |
| **ORM**              | **Prisma**            | Type-safe ORM, migration dễ dàng, DX tốt hơn TypeORM.                                |
| **Authentication**   | **JWT + Argon2**      | Stateless auth, Argon2 an toàn hơn Bcrypt.                                           |
| **Caching**          | **Redis** (Planned)   | Caching response, session management, queues.                                        |
| **Documentation**    | **Swagger (OpenAPI)** | Tự động sinh tài liệu API, test API trực tiếp.                                       |
| **Containerization** | **Docker**            | Đảm bảo môi trường đồng nhất (Dev = Prod).                                           |
| **CI/CD**            | **GitHub Actions**    | Tự động hóa quy trình test và deploy.                                                |

---

## 📂 Kiến trúc hệ thống (Architecture)

Dự án tuân theo kiến trúc **Modular Monolith**, giúp code được tổ chức gọn gàng theo từng domain (Auth, User, Course...) nhưng vẫn chạy trên một process duy nhất để tối ưu chi phí hạ tầng ban đầu. Dễ dàng tách thành Microservices khi cần thiết.

### Cấu trúc thư mục (Folder Structure)

```
src/
├── common/          # Các thành phần dùng chung (Decorators, Guards, Filters...)
├── config/          # Cấu hình hệ thống (Environment variables)
├── modules/         # Các module nghiệp vụ (Domain logic)
│   ├── auth/        # Xác thực & Phân quyền
│   ├── users/       # Quản lý người dùng
│   ├── courses/     # Quản lý khóa học
│   └── ...
├── prisma/          # Database Schema & Seeds
└── main.ts          # Entry point
```

---

## 🚀 Tính năng chính (Key Features)

1.  **Authentication & Authorization**:

    - Đăng ký/Đăng nhập (Email/Password).
    - Refresh Token rotation.
    - Phân quyền dựa trên Role (RBAC): `ADMIN`, `TEACHER`, `STUDENT`, `PARENT`.

2.  **Quản lý Khóa học (LMS)**:

    - Tạo, sửa, xóa khóa học (Teacher/Admin).
    - Đăng ký tham gia khóa học (Student).

3.  **Bài tập & Chấm điểm**:

    - Giao bài tập, nộp bài (File upload).
    - Chấm điểm tự động hoặc thủ công.

4.  **Gamification**:
    - Bảng xếp hạng (Leaderboard) dựa trên điểm số.
    - Hệ thống danh hiệu (Badges) - _Planned_.

---

## 🚦 Hướng dẫn cài đặt (Getting Started)

### Yêu cầu (Prerequisites)

- Node.js >= 20
- pnpm >= 9
- Docker & Docker Compose

### Cài đặt & Chạy Local

1.  **Clone dự án:**

    ```bash
    git clone https://github.com/nghiacd06/clbvuihocthongminh-backend.git
    cd clbvuihocthongminh-backend
    ```

2.  **Cài đặt dependencies:**

    ```bash
    pnpm install
    ```

3.  **Cấu hình môi trường:**

    ```bash
    cp .env.example .env
    # Cập nhật các biến môi trường trong file .env nếu cần
    ```

4.  **Khởi chạy Database (Docker):**

    ```bash
    docker-compose up -d
    ```

5.  **Chạy Migration & Seed data:**

    ```bash
    npx prisma migrate dev
    npx prisma db seed
    ```

6.  **Khởi chạy Server:**
    ```bash
    pnpm run start:dev
    ```

👉 **API Server:** `http://localhost:3000`
👉 **Swagger Docs:** `http://localhost:3000/api-docs`

---

## 🗺 Lộ trình phát triển (Roadmap)

- [x] **Phase 1:** Khởi tạo dự án, thiết lập Docker, Prisma, Auth cơ bản.
- [ ] **Phase 2:** Module Users, Profile, Role Management.
- [ ] **Phase 3:** Module Courses, Lessons, Assignments.
- [ ] **Phase 4:** Tính năng nộp bài, chấm điểm, File Upload (S3/Cloudinary).
- [ ] **Phase 5:** Bảng xếp hạng, Thống kê.
- [ ] **Phase 6:** Testing (Unit/E2E), CI/CD, Deployment.

---

## 🤝 Đóng góp (Contributing)

Mọi đóng góp đều được hoan nghênh! Vui lòng tạo Pull Request hoặc mở Issue để thảo luận.

## 📄 License

Dự án này được cấp phép dưới [MIT License](LICENSE).
