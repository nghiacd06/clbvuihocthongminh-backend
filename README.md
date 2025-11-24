# CLB Vui Học Thông Minh – Backend

**Production-ready NestJS Monolith 2025**

Live API (sau khi hoàn thành): `https://api.clbvuihocthongminh.com`  
Frontend repo: https://github.com/nghiacd06/clbvuihocthongminh

## 1. Mục tiêu dự án

Xây dựng một backend hoàn chỉnh, có thể đưa vào production ngay cho nền tảng e-learning với các tính năng chính:

- Đăng ký / Đăng nhập / Refresh token với 4 vai trò (ADMIN – TEACHER – STUDENT – PARENT)
- Quản lý người dùng, khóa học, bài tập, nộp bài, chấm điểm tự động/ thủ công
- Bảng xếp hạng học viên
- Upload tài liệu / bài nộp
- Swagger documentation, Dockerized, CI/CD, deploy AWS Free Tier

## 2. Tech Stack (2025 production standard)

| Layer             | Technology                              | Lý do chọn                                    |
| ----------------- | --------------------------------------- | --------------------------------------------- |
| Framework         | NestJS 13+ (TypeScript)                 | Opinionated, dễ scale → microservices sau này |
| HTTP Adapter      | @nestjs/platform-fastify (optional)     | Performance cao hơn Express ~20-30%           |
| Database          | PostgreSQL 16 + Prisma ORM              | Type-safe, migration mạnh, phổ biến nhất VN   |
| Authentication    | JWT + Refresh Token + HttpOnly cookie   | Stateless, an toàn, chuẩn ngành               |
| Password hashing  | argon2                                  | Bảo mật cao hơn bcrypt                        |
| Validation        | class-validator + class-transformer     | Type-safe validation                          |
| API Documentation | @nestjs/swagger                         | Tự động sinh Swagger UI đẹp                   |
| Logging           | Winston + daily-rotate-file             | Log có cấu trúc, dễ debug production          |
| Testing           | Jest (unit + e2e) – coverage > 85%      | Built-in, mạnh mẽ                             |
| Containerization  | Docker + docker-compose (multi-stage)   | Local = Production                            |
| Package manager   | pnpm 9                                  | Nhanh nhất, disk-efficient                    |
| Deployment        | AWS EC2 t3.micro + RDS + GitHub Actions | Free Tier 12 tháng, chuẩn doanh nghiệp        |
| File upload       | Cloudinary (hoặc AWS S3 sau này)        | Miễn phí, CDN toàn cầu                        |

## 3. Cấu trúc thư mục (chuẩn doanh nghiệp Việt Nam 2025)

src/
├── app.module.ts
├── main.ts
├── common/
│ ├── decorators/ # @Roles(), @Public(), @CurrentUser()
│ ├── filters/ # AllExceptionsFilter
│ ├── guards/ # JwtAuthGuard, RolesGuard
│ ├── interceptors/ # ResponseInterceptor, LoggingInterceptor
│ ├── pipes/ # Global ValidationPipe
│ └── dto/ # BaseResponseDto, PaginationDto
├── config/
│ └── configuration.ts # @nestjs/config
├── modules/
│ ├── auth/
│ │ ├── dto/
│ │ ├── auth.controller.ts
│ │ ├── auth.service.ts
│ │ └── auth.module.ts
│ ├── users/
│ ├── courses/
│ ├── assignments/
│ ├── scores/
│ ├── rankings/
│ └── upload/
├── prisma/
│ ├── schema.prisma
│ └── seed.ts
└── shared/
└── utils/
text## 4. Các module chính & API endpoints (đã thiết kế)

| Module      | Endpoint mẫu                 | Role cho phép          |
| ----------- | ---------------------------- | ---------------------- |
| Auth        | POST /auth/register          | Public                 |
|             | POST /auth/login             | Public                 |
|             | POST /auth/refresh           | Public (refresh token) |
| Users       | GET /users/me                | All authenticated      |
|             | PATCH /users/me              | Owner                  |
| Courses     | POST /courses                | TEACHER, ADMIN         |
|             | POST /courses/:id/enroll     | STUDENT                |
| Assignments | POST /assignments            | TEACHER                |
|             | POST /assignments/:id/submit | STUDENT                |
| Scores      | GET /scores/my-history       | STUDENT                |
| Rankings    | GET /rankings/top-10         | All authenticated      |
| Upload      | POST /upload                 | Authenticated          |

## 5. Quá trình triển khai (Implementation Roadmap)

| Tuần | Nội dung chính                                | Kết quả đạt được                         |
| ---- | --------------------------------------------- | ---------------------------------------- |
| 1    | Project init, Docker, Prisma, Auth hoàn chỉnh | Register/Login 4 role + protected routes |
| 2    | Users module, Swagger, Logging, Tests         | CRUD user + API docs đẹp                 |
| 3    | Courses + Assignments + File upload           | Teacher tạo khóa học, student nộp bài    |
| 4    | Scores, Rankings, Rate limiting, Security     | Leaderboard + production hardening       |
| 5    | Seed data, Health check, Deploy Railway       | Backend live tạm thời (miễn phí)         |
| 6    | AWS EC2 + RDS + GitHub Actions + SSL          | Backend live thật với domain + HTTPS     |

## 6. Local Development

```bash
# 1. Clone & install
git clone https://github.com/nghiacd06/clbvuihocthongminh-backend.git
cd clbvuihocthongminh-backend
cp .env.example .env
pnpm install

# 2. Chạy DB + pgAdmin
docker-compose up -d

# 3. Migrate & seed
npx prisma migrate dev
npx prisma db seed   # tạo admin default

# 4. Run app
pnpm run start:dev

```

Truy cập:

API: http://localhost:3000
Swagger: http://localhost:3000/api-docs
pgAdmin: http://localhost:8080

## 7. Production Deployment (AWS Free Tier)

Tạo EC2 (Amazon Linux 2023) + RDS PostgreSQL
Security Group: mở port 22 (SSH), 80, 443, 3000
Cấu hình GitHub Actions (file .github/workflows/deploy.yml đã có sẵn)
Push code → tự động build & deploy
Cài Nginx + Certbot (Let’s Encrypt) → HTTPS miễn phí

## 8. Tiêu chí hoàn thành dự án

- [ ] Swagger UI hoạt động đầy đủ và đẹp
- [ ] Docker compose chạy chỉ 1 lệnh
- [ ] Test coverage > 85%
- [ ] Backend live trên AWS với HTTPS
- [ ] Frontend Next.js kết nối thành công 100% API
- [ ] README có badge CI/CD + AWS + NestJS
