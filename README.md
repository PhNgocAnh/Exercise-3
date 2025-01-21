#### .NET Core Web Service với MongoDB 
#### Dự án này là một ví dụ về cách xây dựng một Web API sử dụng **.NET Core** và kết nối với cơ sở dữ liệu **MongoDB**. Ứng dụng cung cấp các chức năng CRUD (Create, Read, Update, Delete) trong MongoDB.  
## Cấu trúc Dự án

### 1. **Models**
- **Book**: Đại diện cho tài liệu trong MongoDB với các thuộc tính như:
  - `Id`: Mã định danh duy nhất của sách.
  - `Name`: Tên sách.
  - `Price`: Giá sách.
  - `Category`: Danh mục sách.
  - `Author`: Tác giả của sách.
  
- **BookStoreDatabaseSettings**: Lưu trữ thông tin cấu hình kết nối với MongoDB, bao gồm:
  - `ConnectionString`: Chuỗi kết nối đến MongoDB.
  - `DatabaseName`: Tên cơ sở dữ liệu.
  - `BooksCollectionName`: Tên bộ sưu tập (collection).

---

### 2. **Services**
- **BooksService**:
  - Chứa logic xử lý dữ liệu và giao tiếp với MongoDB thông qua MongoDB Driver.
  - Các phương thức chính:
    - `GetAsync`: Lấy danh sách tất cả sách.
    - `GetAsync(string id)`: Lấy chi tiết sách dựa trên `Id`.
    - `CreateAsync(Book newBook)`: Tạo một sách mới.
    - `UpdateAsync(string id, Book updatedBook)`: Cập nhật thông tin sách theo `Id`.
    - `RemoveAsync(string id)`: Xóa sách theo `Id`.

---

### 3. **Controllers**
- **BooksController**:
  - Cung cấp các endpoint API để thao tác với tài liệu MongoDB:
    - `GET /api/books`: Lấy danh sách tất cả sách.
    - `GET /api/books/{id}`: Lấy chi tiết sách theo `Id`.
    - `POST /api/books`: Thêm sách mới vào cơ sở dữ liệu.
    - `PUT /api/books/{id}`: Cập nhật sách theo `Id`.
    - `DELETE /api/books/{id}`: Xóa sách theo `Id`.

---

### 4. **Program.cs**
- Cấu hình và khởi tạo ứng dụng, bao gồm:
  - **Đăng ký dịch vụ**:
    - `BookStoreDatabaseSettings`: Đọc thông tin cấu hình từ tệp `appsettings.json`.
    - `BooksService`: Được đăng ký làm singleton service.
  - **Tích hợp Swagger**:
    - Tự động tạo tài liệu API và cung cấp giao diện Swagger UI.
  - **Cấu hình Middleware**:
    - Bật chuyển hướng HTTPS.
    - Xác thực (Authorization).
    - Ánh xạ các controller để xử lý yêu cầu API.
