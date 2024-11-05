# 1. Ca sử dụng Login

## Các lớp phân tích:
- **Controll:** LoginControll
- **Boundary:** LoginForm
- **Entities:** Account

## Biểu đồ Squence

![Diagram](https://www.planttext.com/api/plantuml/png/Z9112W9H28RtdaBQTu4MqQ8MGOieQY_lIJnmd46jcBErw4XTeLSDLBJ9XUZlfwAtotNcGHR7He1Ij8OxPuEkIYMLZZHmjARUMX7SzXxSZ91y204UC8wdGuuJN6XKvLXbfOQHD6D7xkVMCWpG9xudAPc2CHbdrYWa3a0IhygNZDNU8vwR9xXg3rWKM9nngQV_ckR5Ew4UsQmUtB0x7VY9_jopuR0UAvL84mkmPe1PzO-7tG400F__0m00)

## Nhiệm vụ và quan hệ của các lớp phân tích

**1. Lớp LoginControll**
- Nhiệm vụ: Điều khiển đăng nhập
- Một số phương thức:
1. `validate()`: Xác thực tên đăng nhập và mật khẩu,
2. `login()`: Thực hiện đăng nhập,
3. `checkLogin()`: Kiểm tra đăng nhập,
4. `displayError()`: Hiển thị lỗi,
5. `cancelLogin()`: Hủy đăng nhập
**2. Lớp LoginForm**
- Nhiệm vụ: Hiển thì form login
- Thuộc tính:
1. `nameField: String`: Lấy giá trị name từ input
2. `passwordField: String`: Lấy giá trị password từ input
3. `errorMessage: String`: Hiển thị lỗi
4. `isCancel: boolean`: Kiểm tra xem có hủy đăng nhập hay không
- Phương thức:
1. `getName()`: Trả về giá trị từ trường nhập tên.
2. `getPassword()`: Trả về giá trị từ trường nhập mật khẩu.
3. `showError(message: String)`: Hiển thị thông báo lỗi khi đăng nhập không thành công.
4. `resetFields()`: Đặt lại các trường nhập để người dùng có thể nhập lại.
5. `onCancel()`: Xử lý sự kiện khi người dùng hủy đăng nhập, cập nhật `isCancel`.
**3. Lớp Account**
- Nhiệm vụ: Đại diện cho tài khoản người dùng, chứa thông tin như tên đăng nhập và mật khẩu, cũng như trạng thái của tài khoản.
- Thuộc tính:
1. `username: String`: Tên đăng nhập của người dùng.
2. `password: String`: Mật khẩu của người dùng (nên được mã hóa để bảo mật).
3. `isActive: boolean`: Trạng thái hoạt động của tài khoản (có thể là kích hoạt hay bị khóa).
- Phương thức:
1. `validateCredentials(name: String, password: String): boolean`: Xác thực tên đăng nhập và mật khẩu so với thông tin trong tài khoản.
2. `lockAccount()`: Khóa tài khoản khi nhập sai mật khẩu quá số lần cho phép.
3. `unlockAccount()`: Mở khóa tài khoản.
4. `changePassword(newPassword: String)`: Thay đổi mật khẩu của tài khoản.
