# HƯỚNG DẪN CÀI ĐẶT VÀ KHỞI CHẠY ỨNG DỤNG

Tài liệu này hướng dẫn chi tiết từ việc thiết lập Cơ sở dữ liệu bằng Script SQL đến cách khởi chạy ứng dụng **Quản lý chi tiêu cá nhân** từ thư mục `src`.

## 1. Công cụ & Phần mềm yêu cầu

Trước khi bắt đầu, hãy đảm bảo máy tính của bạn đã cài đặt các phần mềm sau:

* **.NET SDK 8.0** (Bộ công cụ để chạy ứng dụng ASP.NET Core).
* **Microsoft SQL Server (phiên bản 2022 trở lên):** Khuyến nghị bản **Express**.
* **SQL Server Management Studio (SSMS):** Công cụ để quản lý và chạy script cơ sở dữ liệu.
* **Visual Studio 2022**.

---

## 2. Các bước cài đặt chi tiết

### Bước 1: Khởi tạo Cơ sở dữ liệu (Dùng Script SQL)

Thay vì sử dụng lệnh Migration, dự án đã chuẩn bị sẵn file script SQL chứa toàn bộ cấu trúc bảng (`tblTaiKhoan`, `tblVi`, `tblGiaoDich`, `tblNganSach`) và dữ liệu thử nghiệm.

1. Khởi động **SQL Server Management Studio (SSMS)** và kết nối vào SQL Server của bạn.
2. Chọn **File** > **Open** > **File...** và mở file chứa nội dung script SQL của bạn (hoặc tạo một `New Query` rồi dán toàn bộ đoạn mã SQL vào).
3. Nhấn **Execute (F5)** để khởi tạo database `chitieucanhanDB` cùng dữ liệu mẫu.

> ⚠️ **Lưu ý quan trọng:** Script mặc định lưu file dữ liệu tại đường dẫn `C:\Program Files\Microsoft SQL Server\MSSQL16.SQLEXPRESS\...`. Nếu phân hệ SQL Server trên máy bạn cài ở ổ đĩa khác hoặc dùng phiên bản khác (như MSSQL15), hãy sửa lại hai đường dẫn tệp `.mdf` và `.ldf` ở đầu đoạn code SQL trước khi nhấn lệnh chạy.

### Bước 2: Cấu hình Chuỗi kết nối ứng dụng

Ứng dụng cần được kết nối tới SQL Server bạn vừa tạo.

1. Di chuyển vào thư mục `src/` của dự án và mở file `appsettings.json`.
2. Tìm và chỉnh sửa mục `ConnectionStrings` như sau (thay đổi `Server` phù hợp với tên máy của bạn):

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=.\\SQLEXPRESS;Database=chitieucanhanDB;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true"
}

```

### Bước 3: Khôi phục gói thư viện (Restore Packages)

Mở giao diện dòng lệnh (Terminal / PowerShell / CMD) tại thư mục `src/` và chạy lệnh sau để tải các gói thư viện cần thiết:

```bash
dotnet restore

```

---

## 3. Khởi chạy dự án


### Sử dụng Visual Studio 2022

1. Mở Visual Studio và chọn **Open a project or solution**.
2. Tìm đến thư mục `src/` và mở file `Web.csproj` (hoặc tệp `.sln` ngoài thư mục gốc nếu có).
3. Nhấn nút **Play** (hình tam giác xanh lá) hoặc nhấn tổ hợp phím `Ctrl + F5` để khởi chạy ứng dụng tự động mở trên trình duyệt.

---

## 4. Thông tin tài khoản đăng nhập thử nghiệm

Sau khi chạy ứng dụng thành công, bạn có thể sử dụng trực tiếp các tài khoản có sẵn trong database để kiểm tra các tính năng (Quản lý ví, Giao dịch thu chi, Ngân sách):

| Email đăng nhập | Mật khẩu mẫu | Tên người dùng |
| --- | --- | --- |
| `170124186@rdi.edu.vn` | *Pa123456@#Pa* | Truong Lu Quoc |
| `170124188@rdi.edu.vn` | *Pa123456@#Pa* | Lê Tuấn Anh |
| `170124190@rdi.edu.vn` | *Pa123456@#Pa* | Hồ Trung Hiếu |

---