# Cookie Session Auth Example

## Mô tả
Đây là dự án Node.js sử dụng Express, MongoDB, session và cookie để xác thực người dùng.

## Cài đặt
1. Clone hoặc tải về dự án.
2. Chạy lệnh cài đặt các package:
   ```powershell
   npm install
   ```
3. Đảm bảo MongoDB đang chạy ở địa chỉ `mongodb://127.0.0.1:27017/sessionAuth`.
4. Khởi động server:
   ```powershell
   node app.js
   ```

## API và chức năng

### 1. Đăng ký tài khoản
- **URL:** `POST /auth/register`
- **Body:**
  ```json
  { "username": "admin", "password": "12345" }
  ```
- **Kết quả thành công:**
![User registered successfully!](img/image1.png)
![MongoDB users](img/image7.png)
![MongoDB session](img/image9.png)
  ```json
  { "message": "User registered successfully!" }
  
  ```
- **Lỗi:**
  - Username đã tồn tại hoặc thiếu trường dữ liệu
  ![User registration failed](img/image2.png)
  - Trả về:
    ```json
    { "error": "User registration failed", "details": "E11000 duplicate key error collection: sessionAuth.users index: username_1 dup key: { username: \"admin\" }" }
    ```

### 2. Đăng nhập
- **URL:** `POST /auth/login`
- **Body:**
  ```json
  { "username": "admin", "password": "12345" }
  ```
- **Kết quả thành công:**
![Login successful!](img/image3.png)
  ```json
  { "message": "Login successful!" }
  ```
  - Cookie `connect.sid` được trả về để xác thực phiên đăng nhập.
![connect.sid](img/image4.png)
![MongoDB](img/image5.png)

- **Lỗi:**
  - Sai username hoặc password
![Invalid username or password](img/image6.png)
  - Trả về:
  "Invalid username or password" 
  - Không ghi nhận được dữ liệu hệ thống báo lỗi
![Login failed](img/image13.png)
  - Trả về: 
  "Login failed" 
### 3. Xem thông tin cá nhân (Profile)
- **URL:** `GET /auth/profile`
- **Yêu cầu:** Đã đăng nhập (gửi kèm cookie `connect.sid`)
- **Kết quả thành công:**
  - Trả về thông tin user (không có password)
![No password](img/image10.png)
![Cookie](img/image11.png)
- **Lỗi:**
  - Chưa đăng nhập hoặc session hết hạn
![Unauthorized](img/image12.png)
  - Trả về: 
  "Unauthorized" 
### 4. Đăng xuất
- **URL:** `GET /auth/logout`
- **Yêu cầu:** Đã đăng nhập (gửi kèm cookie `connect.sid`)
- **Kết quả thành công:**
![Logout successful!](img/image14.png)
![not cookie](img/image15.png)
![not cookie MonggoDB](img/image16.png)
 "Logout successful!" 
- **Lỗi:**
  - Nếu session không tồn tại hoặc có lỗi khi xóa session
  - Trả về:
    ```json
    { "error": "Logout failed" }
    ```

## Các trường hợp lỗi cần kiểm thử
- Đăng ký với username đã tồn tại
- Đăng nhập với sai mật khẩu
- Truy cập profile khi chưa đăng nhập
- Đăng xuất khi chưa đăng nhập

## Liên hệ
Nếu có thắc mắc, vui lòng liên hệ qua email hoặc github của tác giả.