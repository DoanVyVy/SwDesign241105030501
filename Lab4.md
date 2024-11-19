# Phân tích và thiết kế ca sử dụng
### 1. Login:
Mô tả: 
  - Đăng nhập là bước khởi đầu để người dùng truy cập vào hệ thống và sử dụng các chức năng khác.

Actor: 
  - Nhân viên, Quản lý, Bộ phận nhân sự.

Luồng chính:
  - Người dùng mở giao diện đăng nhập.
  - Nhập tên đăng nhập và mật khẩu.
  - Hệ thống xác thực thông tin.
  - Nếu hợp lệ, chuyển người dùng đến giao diện chính.

Luồng phụ:
  - Nếu sai tên đăng nhập hoặc mật khẩu, hiển thị thông báo lỗi và yêu cầu nhập lại.
  - Nếu tài khoản bị khóa, hiển thị thông báo liên hệ quản trị viên.

Lý do thiết kế:
  - Bảo vệ dữ liệu nhạy cảm (lương, thông tin nhân viên).
  - Xác định quyền hạn của người dùng dựa trên vai trò (nhân viên, quản lý, nhân sự).

### 2. Ca sử dụng: Nhập giờ làm việc
Mô tả:
  - Nhân viên nhập số giờ làm việc để hệ thống làm cơ sở tính lương.

Actor: Nhân viên.
Luồng chính:
  - Nhân viên đăng nhập vào hệ thống.
  - Chọn tính năng "Nhập giờ làm việc".
  - Nhập số giờ làm việc vào biểu mẫu.
  - Gửi yêu cầu đến hệ thống.
  - Hệ thống kiểm tra dữ liệu (vd: giờ không được âm, số giờ không vượt quá giới hạn).
  - Lưu thông tin vào cơ sở dữ liệu.

Luồng phụ:
  - Nếu nhập dữ liệu không hợp lệ, hiển thị thông báo lỗi và yêu cầu nhập lại.

Lý do thiết kế:
  - Dữ liệu giờ làm việc là yếu tố cốt lõi để tính toán lương.
  - Đơn giản hóa quy trình nhập dữ liệu cho nhân viên.

### 3. Ca sử dụng: Tính lương
Mô tả:
  - Quản lý yêu cầu hệ thống tính toán lương cho tất cả nhân viên dựa trên giờ làm việc và các quy định.

Actor: Quản lý.

Luồng chính:
  - Quản lý đăng nhập vào hệ thống.
  - Chọn chức năng "Tính lương".
  - Hệ thống truy xuất dữ liệu giờ làm việc và thông tin nhân viên từ cơ sở dữ liệu.
  - Áp dụng công thức tính lương (Lương cơ bản + Phụ cấp - Các khoản trừ).
  - Lưu kết quả lương vào cơ sở dữ liệu.
  - Hiển thị thông báo hoàn tất.

Luồng phụ:
  - Nếu thiếu dữ liệu giờ làm việc hoặc thông tin lương cơ bản, hiển thị lỗi yêu cầu bổ sung.

Lý do thiết kế:
  - Tự động hóa việc tính lương, giảm thiểu sai sót và tiết kiệm thời gian.

### 4. Ca sử dụng: Tạo phiếu lương
Mô tả:
  - Hệ thống tạo phiếu lương cá nhân cho từng nhân viên, phục vụ việc tra cứu hoặc gửi qua email.

Actor: Bộ phận nhân sự.

Luồng chính:
  - Bộ phận nhân sự đăng nhập vào hệ thống.
  - Chọn tính năng "Tạo phiếu lương"./-strong/-heart:>:o:-((:-h - Hệ thống lấy dữ liệu lương từ cơ sở dữ liệu.
  - Tạo phiếu lương theo định dạng PDF hoặc Excel.
  - Gửi phiếu lương qua email hoặc lưu trữ để tải xuống.

Lý do thiết kế:
  - Đáp ứng nhu cầu thông báo lương cho nhân viên một cách chính xác và minh bạch.

5. Ca sử dụng: Tạo báo cáo lương
Mô tả:
  - Quản lý tạo báo cáo tổng hợp về tình hình lương của công ty trong một khoảng thời gian.

Actor: Quản lý.

Luồng chính:
  - Quản lý đăng nhập vào hệ thống.
  - Chọn tính năng "Tạo báo cáo lương".
  - Nhập các tiêu chí báo cáo (tháng/năm, phòng ban, nhân viên cụ thể).
  - Hệ thống tổng hợp dữ liệu lương theo yêu cầu.
  - Xuất báo cáo dưới dạng PDF/Excel.

Luồng phụ:
  - Nếu không có dữ liệu cho tiêu chí báo cáo, hiển thị thông báo "Không có dữ liệu".

Lý do thiết kế:
  - Cung cấp công cụ hỗ trợ quản lý trong việc theo dõi và phân tích chi phí lương.

# Lý do thiết kế các ca sử dụng
Phù hợp với nghiệp vụ thực tiễn:
  - Các ca sử dụng đáp ứng đúng yêu cầu quản lý lương và xử lý thanh toán trong các doanh nghiệp.
  - Đảm bảo sự phân quyền rõ ràng giữa nhân viên, quản lý và nhân sự.

Tăng hiệu quả và tự động hóa:
  - Các chức năng tính lương, tạo phiếu lương, và báo cáo đều tự động, giảm công việc thủ công.
  - Quy trình rõ ràng giúp người dùng dễ sử dụng.

Tính bảo mật:
  - Yêu cầu đăng nhập giúp hạn chế truy cập trái phép.
  - Dữ liệu nhạy cảm như lương và thông tin cá nhân được bảo vệ trong toàn bộ hệ thống.

Khả năng mở rộng:
  - Các ca sử dụng được thiết kế để dễ dàng bổ sung chức năng mới (ví dụ: quản lý thưởng, quản lý nghỉ phép).

# Biểu đồ tuần tự minh họa
Biểu đồ tuần tự: Đăng nhập

Actors: Nhân viên, Quản lý.

Objects: LoginForm, Database.

Tương tác:
  - Actor gửi yêu cầu đăng nhập với tên và mật khẩu.
  - LoginForm xác thực thông tin với Database.
  - Nếu hợp lệ, cấp quyền truy cập và trả về giao diện chính.
  - Biểu đồ tuần tự: Tính lương

Actors: Quản lý.

Objects: PayrollForm, Database.

Tương tác:
  - Quản lý gửi yêu cầu tính lương.
  - PayrollForm truy xuất dữ liệu từ Database.
  - Áp dụng công thức tính lương.
  - Lưu kết quả và thông báo hoàn tất.
