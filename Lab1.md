# 1. Phân tích kiến trúc
Kiến trúc của hệ thống Payroll gồm các thành phần chính sau:

1. **Giao diện người dùng (UI)**
   - Đây là nơi nhân viên và quản trị viên tương tác với hệ thống. Giao diện dựa trên Windows, cung cấp các chức năng như đăng nhập, nhập thông tin thẻ chấm công, đơn hàng, và thay đổi phương thức thanh toán.
   - **Lý do**: Việc sử dụng giao diện dựa trên Windows giúp hệ thống dễ sử dụng và tương thích tốt với các máy tính cá nhân của nhân viên.

2. **Lớp logic nghiệp vụ (Business Logic Layer)**
   - Xử lý các logic quan trọng liên quan đến việc tính lương, hoa hồng, quản lý thẻ chấm công và đơn hàng. Các yêu cầu như trả lương cho nhân viên đúng số tiền, đúng thời gian và phương thức được chọn đều được thực hiện tại lớp này.
   - **Lý do**: Việc tách biệt logic nghiệp vụ giúp hệ thống dễ bảo trì và mở rộng khi cần thêm chức năng.

3. **Cơ sở dữ liệu quản lý dự án (Legacy Database)**
   - Hệ thống Payroll tương tác với cơ sở dữ liệu DB2 hiện có, chứa các thông tin về dự án và mã phí. Tuy nhiên, hệ thống Payroll chỉ truy cập chứ không cập nhật cơ sở dữ liệu này.
   - **Lý do**: Tiết kiệm chi phí do tận dụng cơ sở dữ liệu hiện có mà không cần phải xây dựng lại từ đầu.

4. **Cơ sở dữ liệu trả lương (Payroll Database)**
   - Hệ thống lưu trữ toàn bộ thông tin về nhân viên, thẻ chấm công, đơn hàng và dữ liệu tính toán lương trong cơ sở dữ liệu quan hệ RDBMS. Các truy vấn SQL sẽ được sử dụng để lấy và cập nhật dữ liệu.
   - **Lý do**: Sử dụng RDBMS đảm bảo hiệu quả lưu trữ và truy xuất dữ liệu nhanh chóng, đồng thời dễ dàng quản lý và bảo trì.

5. **Tích hợp ngân hàng (Bank System Interface)**
   - Hệ thống kết nối với hệ thống ngân hàng để thực hiện các giao dịch nộp tiền trực tiếp vào tài khoản ngân hàng của nhân viên khi chọn phương thức thanh toán qua ngân hàng.
   - **Lý do**: Đảm bảo tính an toàn và bảo mật trong việc chuyển tiền trực tiếp cho nhân viên, cũng như tuân thủ các quy định pháp lý về giao dịch tài chính.

6. **Bảo mật (Security)**
   - Hệ thống đảm bảo rằng chỉ có các nhân viên mới có thể chỉnh sửa thông tin của chính họ và chỉ quản trị viên mới được thay đổi thông tin nhân viên hoặc thiết lập hệ thống.
   - **Lý do**: Tăng cường bảo mật và ngăn ngừa truy cập trái phép vào thông tin nhạy cảm, đặc biệt là liên quan đến lương và thẻ chấm công.
# 2. Cơ chế phân tích
Dưới đây là các **cơ chế phân tích** được đề xuất cho hệ thống **Payroll** và lý do lựa chọn từng cơ chế:

### 1. **Persistency (Tính bền vững dữ liệu)**
   - **Mô tả**: Hệ thống cần lưu trữ và quản lý dữ liệu liên quan đến nhân viên, thẻ chấm công, đơn hàng và các giao dịch thanh toán. Cơ chế này đảm bảo dữ liệu vẫn tồn tại sau khi ứng dụng kết thúc.
   - **Cơ chế đề xuất**: Sử dụng cơ sở dữ liệu quan hệ (RDBMS) như MySQL hoặc PostgreSQL để lưu trữ thông tin nhân viên, bảng chấm công và giao dịch thanh toán.
   - **Lý do**: Cơ sở dữ liệu quan hệ cung cấp khả năng quản lý dữ liệu hiệu quả, dễ truy vấn và bảo mật dữ liệu lâu dài.

### 2. **Security (Bảo mật)**
   - **Mô tả**: Cơ chế bảo mật ngăn chặn truy cập trái phép vào hệ thống, đặc biệt với các thông tin nhạy cảm như lương và thông tin tài khoản ngân hàng.
   - **Cơ chế đề xuất**:
     - **Xác thực** (Authentication): Xác thực người dùng qua tên đăng nhập và mật khẩu.
     - **Phân quyền** (Authorization): Chỉ cho phép nhân viên truy cập và thay đổi thông tin của chính mình, và chỉ quản trị viên được thay đổi thông tin của nhân viên khác.
   - **Lý do**: Đảm bảo an toàn cho dữ liệu nhạy cảm và duy trì tính toàn vẹn của hệ thống khi nhiều người dùng tương tác.

### 3. **Concurrency (Xử lý đồng thời)**
   - **Mô tả**: Nhiều người dùng có thể truy cập và thực hiện các thao tác cùng một lúc, chẳng hạn như nhập thông tin thẻ chấm công hoặc thực hiện thanh toán.
   - **Cơ chế đề xuất**: Sử dụng cơ chế khóa trong cơ sở dữ liệu để tránh xung đột khi nhiều người dùng thao tác cùng một lúc (ví dụ: cơ chế "optimistic locking" hoặc "pessimistic locking").
   - **Lý do**: Đảm bảo tính nhất quán của dữ liệu và tránh tình trạng nhiều người dùng chỉnh sửa đồng thời dẫn đến lỗi xung đột dữ liệu.

### 4. **Transaction Management (Quản lý giao dịch)**
   - **Mô tả**: Các thao tác thanh toán hoặc cập nhật thông tin quan trọng phải được thực hiện như một giao dịch toàn vẹn, nghĩa là tất cả các bước trong quá trình phải hoàn thành hoặc không có bước nào được thực hiện.
   - **Cơ chế đề xuất**: Sử dụng cơ chế quản lý giao dịch ACID (Atomicity, Consistency, Isolation, Durability) của cơ sở dữ liệu.
   - **Lý do**: Đảm bảo các thay đổi quan trọng như cập nhật lương hoặc thanh toán được thực hiện chính xác và không gây ra lỗi dữ liệu.

### 5. **Error Handling (Xử lý lỗi)**
   - **Mô tả**: Trong trường hợp xảy ra lỗi (ví dụ: lỗi kết nối ngân hàng hoặc lỗi cơ sở dữ liệu), hệ thống cần có cơ chế xử lý phù hợp để không ảnh hưởng đến toàn bộ hệ thống.
   - **Cơ chế đề xuất**: Sử dụng cơ chế xử lý ngoại lệ (exception handling) và ghi log chi tiết.
   - **Lý do**: Giúp phát hiện và xử lý lỗi một cách kịp thời, đảm bảo hệ thống hoạt động ổn định.

### 6. **Logging and Auditing (Ghi log và kiểm tra)**
   - **Mô tả**: Ghi lại các hành động quan trọng trong hệ thống như thanh toán, chỉnh sửa thông tin nhân viên, để có thể kiểm tra khi cần.
   - **Cơ chế đề xuất**: Sử dụng hệ thống ghi log để lưu trữ lịch sử các thao tác quan trọng và các sự kiện trong hệ thống.
   - **Lý do**: Cần có hệ thống ghi log để kiểm tra khi xảy ra sự cố và đảm bảo tính minh bạch trong quản lý hệ thống.

### 7. **Scalability (Khả năng mở rộng)**
   - **Mô tả**: Hệ thống cần có khả năng mở rộng khi số lượng nhân viên hoặc khối lượng giao dịch tăng lên.
   - **Cơ chế đề xuất**: Sử dụng kiến trúc mô-đun, chia hệ thống thành các thành phần nhỏ có thể dễ dàng mở rộng, và có thể triển khai kiến trúc phân tán nếu cần thiết.
   - **Lý do**: Đảm bảo hệ thống có thể mở rộng khi quy mô công ty hoặc nhu cầu tính lương tăng lên mà không làm giảm hiệu suất.

### 8. **Integration with Legacy Systems (Tích hợp với hệ thống cũ)**
   - **Mô tả**: Hệ thống mới cần phải tích hợp với cơ sở dữ liệu quản lý dự án cũ (DB2) để truy xuất thông tin dự án.
   - **Cơ chế đề xuất**: Sử dụng API hoặc JDBC để kết nối và truy xuất dữ liệu từ hệ thống DB2 hiện có.
   - **Lý do**: Đảm bảo tích hợp dữ liệu từ hệ thống cũ mà không cần phải xây dựng lại toàn bộ từ đầu, tiết kiệm chi phí.
# 3. Phân tích ca sử dụng Payment
### **Xác định các lớp phân tích:**

Dựa trên ca sử dụng Payment, các lớp phân tích sau đây được xác định:

1. **Employee (Nhân viên)**
   - **Nhiệm vụ**: Lớp này đại diện cho một nhân viên, có thể chọn và thay đổi phương thức thanh toán của họ.
   - **Thuộc tính**:
     - `employeeID: int`
     - `name: String`
     - `paymentMethod: PaymentMethod`
   - **Quan hệ**: Có quan hệ với lớp `PaymentMethod`.

2. **PaymentMethod (Phương thức thanh toán)**
   - **Nhiệm vụ**: Đại diện cho phương thức thanh toán được chọn, có thể là nhận tiền trực tiếp, qua thư hoặc chuyển khoản ngân hàng.
   - **Thuộc tính**:
     - `methodType: String` (Pick-up, Mail, Direct Deposit)
     - `address: String` (nếu phương thức là Mail)
     - `bankAccount: String` (nếu phương thức là Direct Deposit)
   - **Quan hệ**: Được sử dụng bởi lớp `Employee` và tương tác với lớp `BankSystem` nếu là phương thức chuyển khoản ngân hàng.

3. **PaymentController (Bộ điều khiển thanh toán)**
   - **Nhiệm vụ**: Điều khiển toàn bộ quy trình chọn, xác thực và cập nhật phương thức thanh toán cho nhân viên.
   - **Phương thức**:
     - `selectPaymentMethod()`
     - `validatePaymentDetails()`
     - `confirmAndSavePayment()`
   - **Quan hệ**: Tương tác với `PaymentUI`, `Employee`, và `PaymentMethod`.

4. **PaymentUI (Giao diện thanh toán)**
   - **Nhiệm vụ**: Hiển thị giao diện cho nhân viên để chọn và nhập thông tin thanh toán.
   - **Phương thức**:
     - `displayPaymentOptions()`
     - `getSelectedPaymentMethod()`
     - `showConfirmation()`
   - **Quan hệ**: Tương tác với `Employee` và `PaymentController`.

5. **BankSystem (Hệ thống ngân hàng)**
   - **Nhiệm vụ**: Xử lý giao dịch khi phương thức thanh toán là chuyển khoản ngân hàng.
   - **Phương thức**:
     - `sendPayment(employee, amount, bankAccount)`
   - **Quan hệ**: Tương tác với `PaymentController` và `PaymentMethod`.

---

### **Mô tả hành vi thông qua biểu đồ Sequence:**

Dưới đây là biểu đồ **Sequence** mô tả quá trình chọn phương thức thanh toán:

![Diagram](https://www.planttext.com/api/plantuml/png/Z5HBJiCm4Dtx52DMhGGNg0G2IXPPK28g3k34KseHsy6U5ELiB3WILy2EdQGfL2ARnFDvdz4utvzVjuwufLRLZ5TaB6IggKs72Dn1nahJQi5j1mNl56fwoKFy9MULqMHDFSJNyLYZ3VbYpNnCKZUYPV4OC8z0xxb-stQEKEMQqEvurTE6C6CPNDrufXKyutkBZg29LA2GzaQ0QKWQxPYNv0kBzGg4T4tDkoJfAUONIrQiGqMMhU0LAMKVUn2Vp3nFwhT8hTLGjTO6dZbVZv8KkRtv6DE3Zadm5ckiVlLFEbrRAdaYnFKzAE9noHYl2ORWO5awk7ZaihvWu9zeAn3QEA6GkXF2eWkkGyaegR7c80KUL_3uZeMduiuMJhDi6y49aujSxymYghoE4YzXx4Cjpljva3OCwm4RuoITSHOsegVuszQOBlt7XYlqv5NbjumshIhH_ktnVrt_CNpYuHBA17qC4UWyjHz6WbXWkXnJlLUWWe3O5ph6vVGNRYUj6dhJL2TrZXzcscQRFQoYz9c-ShRES-ZnPjnwXl1V-0400F__0m00)

### **Xác định nhiệm vụ của từng lớp phân tích:**

1. **Employee**
   - Quản lý thông tin cá nhân của nhân viên và phương thức thanh toán của họ.
   - Xác định các thông tin cần thiết khi chọn phương thức thanh toán (địa chỉ hoặc thông tin ngân hàng).

2. **PaymentMethod**
   - Lưu trữ thông tin chi tiết của phương thức thanh toán (Pick-up, Mail, Direct Deposit).
   - Xác định và cung cấp các chi tiết thanh toán tùy thuộc vào phương thức.

3. **PaymentController**
   - Xử lý quy trình chọn phương thức thanh toán.
   - Xác thực các chi tiết thanh toán do nhân viên cung cấp.
   - Lưu thông tin thanh toán vào hệ thống.
   - Tương tác với hệ thống ngân hàng nếu cần thiết.

4. **PaymentUI**
   - Hiển thị giao diện để nhân viên chọn phương thức thanh toán.
   - Thu thập thông tin từ nhân viên như địa chỉ hoặc thông tin ngân hàng.

5. **BankSystem**
   - Xử lý giao dịch thanh toán qua chuyển khoản ngân hàng khi phương thức thanh toán là Direct Deposit.

---

### **Biểu đồ lớp phân tích và giải thích:**

![Diagram](https://www.planttext.com/api/plantuml/png/V5DBJiD03Dtt51QhLg8BjbcWbi-Y2mHIu01kngKZvXF6Jb64E1aBZiGLIC8afDEMRA9vzhFVF7k-FxyMB1YaicPI66I6MriQNnF1-mIQRmuKWTLD1jf9H1rQoY2NeDrpX4giBJcv8zbwbS73-DYb03397ZpzZpEBfEUKD4kBVqoY-3ruk87jZezrcIf6fG8n9-WQtSkoA7pbP2y2i4EZ5Ggr2jRU6q9teF661BNXDYLoKtNNtadmnb282bjV31N9BNynKlzwqojAcyTmuTr61xjqAiTTdzH4KqbFgq6AqbmQh6FWlXJjtL_1vfvvr9NC92O4Ugs8vQhnSEKsFbKIINcrjfgvAJqMqvBoceNioWc53HOqSiZr7QVzHcR3ifuV6zeveFqzAr-j3NMTXlK-kpY3-Voo---lJGPRvCdXiDhiWTwz1GfO2CERbks9_BHoFoy6T0gu6ShGgPd1Y36gam6tTiafJSTiEv2tQFnh7_aF0000__y30000)

### **Giải thích biểu đồ lớp phân tích:**

- **Employee**: Đại diện cho nhân viên và chứa thông tin về phương thức thanh toán của họ.
- **PaymentMethod**: Quản lý các loại phương thức thanh toán (như Pick-up, Mail, Direct Deposit) và các chi tiết liên quan (địa chỉ, thông tin ngân hàng).
- **PaymentController**: Điều khiển toàn bộ quy trình xử lý chọn, xác thực, và lưu phương thức thanh toán.
- **PaymentUI**: Giao diện cho nhân viên để chọn phương thức thanh toán.
- **BankSystem**: Xử lý giao dịch chuyển khoản ngân hàng khi nhân viên chọn Direct Deposit.

Quan hệ giữa các lớp:
- Lớp `PaymentController` điều khiển và tương tác với các lớp `Employee`, `PaymentMethod`, và `BankSystem`.
- Lớp `PaymentUI` tương tác trực tiếp với nhân viên và chuyển tiếp các lựa chọn lên lớp điều khiển `PaymentController`.

