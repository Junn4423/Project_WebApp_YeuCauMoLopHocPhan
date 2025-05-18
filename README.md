# Project WebApp Yêu Cầu Mở Lớp Học Phần

Ứng dụng web hỗ trợ sinh viên và giảng viên thực hiện yêu cầu mở lớp học phần, quản lý thông tin sinh viên, giảng viên, môn học và lịch học.

---

## Mục lục

* [Giới thiệu](#giới-thiệu)
* [Chức năng chính](#chức-năng-chính)
* [Kiến trúc tổng quan](#kiến-trúc-tổng-quan)
* [Công nghệ sử dụng](#công-nghệ-sử-dụng)
* [Yêu cầu môi trường](#yêu-cầu-môi-trường)
* [Cài đặt và chạy ứng dụng](#cài-đặt-và-chạy-ứng-dụng)
* [Cấu hình kết nối cơ sở dữ liệu](#cấu-hình-kết-nối-cơ-sở-dữ-liệu)
* [Seed dữ liệu mẫu](#seed-dữ-liệu-mẫu)
* [API Endpoints](#api-endpoints)
* [Kiểm thử](#kiểm-thử)
* [Đóng góp](#đóng-góp)
* [License](#license)

---

## Giới thiệu

`Project_WebApp_YeuCauMoLopHocPhan` là hệ thống quản lý và xử lý yêu cầu mở lớp học phần dành cho sinh viên và giảng viên. Ứng dụng cho phép:

* Sinh viên tạo và theo dõi trạng thái yêu cầu mở lớp
* Giảng viên phê duyệt hoặc từ chối yêu cầu
* Quản trị viên quản lý thông tin sinh viên, giảng viên, môn học và lịch học

## Chức năng chính

1. **Đăng nhập / Đăng ký**

   * Xác thực người dùng qua JWT
2. **Quản lý sinh viên**

   * Thêm, sửa, xoá thông tin sinh viên
3. **Quản lý giảng viên**

   * Thêm, sửa, xoá thông tin giảng viên
4. **Quản lý môn học / học phần**

   * Danh sách môn học, mã học phần, tín chỉ
5. **Yêu cầu mở lớp**

   * Sinh viên tạo yêu cầu, đính kèm lý do
   * Giảng viên / admin phê duyệt hoặc từ chối
6. **Lịch học**

   * Cấu hình lịch học sau khi lớp được duyệt
7. **Báo cáo và thống kê**

   * Xuất báo cáo yêu cầu theo trạng thái

## Kiến trúc tổng quan

```
Client (React)  <--->  Web API (.NET Core)  <--->  Database (SQL Server)
```

* **Presentation Layer**: React + Bootstrap / Material UI
* **Business Layer**: ASP.NET Core Web API, Clean Architecture
* **Data Layer**: Entity Framework Core, SQL Server

## Công nghệ sử dụng

* **Backend**: .NET 6+ / .NET Core
* **ORM**: Entity Framework Core
* **Database**: SQL Server / PostgreSQL (tuỳ cấu hình)
* **Frontend**: React, TypeScript, Axios
* **Xác thực**: JWT (JSON Web Token)
* **Build & CI/CD**: GitHub Actions / Azure DevOps

## Yêu cầu môi trường

* .NET SDK 6.0 hoặc cao hơn
* Node.js 14+ và npm/yarn
* SQL Server (hoặc PostgreSQL)
* Git

## Cài đặt và chạy ứng dụng

1. **Clone repo**

   ```bash
   git clone https://github.com/Junn4423/Project_WebApp_YeuCauMoLopHocPhan.git
   cd Project_WebApp_YeuCauMoLopHocPhan
   ```

2. **Thiết lập backend**

   ```bash
   cd Server         # hoặc thư mục chứa project .NET
   dotnet restore
   dotnet ef database update    # migrates và tạo schema
   dotnet run --urls "https://localhost:5001"
   ```

3. **Thiết lập frontend**

   ```bash
   cd ../ClientApp   # hoặc thư mục React/Angular
   npm install
   npm start        # chạy dev server trên port 3000
   ```

4. Mở trình duyệt vào `https://localhost:5001` (API) và `http://localhost:3000` (UI)

## Cấu hình kết nối cơ sở dữ liệu

Trong file `appsettings.json` (hoặc biến môi trường) đặt chuỗi kết nối:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=.;Database=StudentRegistration;User Id=sa;Password=Your_password123;"
}
```

## Seed dữ liệu mẫu

* Tập tin `DataSeeder.cs` trong project backend chứa logic tạo sẵn:

  * 50 sinh viên mẫu
  * 20 giảng viên mẫu
  * 30 môn học
  * Một số yêu cầu mở lớp demo

Chạy kèm lệnh migrate sẽ tự động seed:

```bash
dotnet run
```

## API Endpoints

| Method | Endpoint                     | Mô tả                    |
| ------ | ---------------------------- | ------------------------ |
| POST   | `/api/auth/register`         | Đăng ký tài khoản        |
| POST   | `/api/auth/login`            | Đăng nhập, trả về JWT    |
| GET    | `/api/students`              | Lấy danh sách sinh viên  |
| POST   | `/api/students`              | Thêm sinh viên           |
| GET    | `/api/lecturers`             | Lấy danh sách giảng viên |
| POST   | `/api/requests`              | Tạo yêu cầu mở lớp       |
| PUT    | `/api/requests/{id}/approve` | Phê duyệt yêu cầu        |
| PUT    | `/api/requests/{id}/reject`  | Từ chối yêu cầu          |

## Kiểm thử

* **Unit Test**: xUnit / NUnit cho backend
* **Integration Test**: sử dụng InMemory DB

Chạy test:

```bash
cd Server
dotnet test
```

## Đóng góp

Mọi đóng góp (issues/pull requests) rất hoan nghênh. Vui lòng tuân thủ quy tắc:

* Tạo branch riêng cho feature/fix
* Follow code style (nếu có)
* Viết test cho thay đổi

## License

---
DOCS: [![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/Junn4423/Project_WebApp_YeuCauMoLopHocPhan)
*Updated: May 18, 2025*
