# 1. Subsystem context diagrams

### 1. BankSystem (Hệ Thống Ngân Hàng)

**Mô Tả:**  
BankSystem chịu trách nhiệm quản lý các giao dịch ngân hàng liên quan đến trả lương, đảm bảo rằng các khoản thanh toán được nạp chính xác vào tài khoản ngân hàng của nhân viên. Hệ thống con này cung cấp dịch vụ nạp tiền trực tiếp qua giao diện ngân hàng.

**Sơ Đồ:**  
![Sơ Đồ BankSystem](https://www.planttext.com/api/plantuml/png/h5D1JiCm4Bpx5QjUA19fuLf5LTKAeKWSAdf071TdcrXnxCXsW0Xu6GUUn1U8awPDQ14NBfRjdPsP7ITV7vyBwz2uCfVCPa8LQ307GzoXIYJ1AmDO8iyIeqiLhxJK9Wnj-MWhwoY7mkYNQZw71v9IFv_2HigHsIAd6dKhajJT6AnE0KavuJpNVIeSiNV6pc2bbJDQmagYjOpx5TPOrLToLv9a80nvUwYRlL-0wHHCgQ1eeUFpbcrlPSSdzkTeYIhRj2CDBRTyCHNQ2ZV6MfodnBCPTBiBg6cqxv-1NoErrIP79xJQoMxsQQrzMeDX1hh7iVw3-dKJQojAlGoRTZZ4tZFK8-a3Qh8xaisrJKLXsV5BZ2udawiH1C6ys_QJdK4i_9VL3MIXCM7XII0RFC5R4FIY6TGyTsV_gF33FVkjxuysjY0L-p_Y6m00__y30000)

**Các Thành Phần:**  
- **PayrollController**: Lớp điều khiển khởi tạo quy trình trả lương.
- **IBankSystem (Interface)**: Giao diện cung cấp phương thức nạp lương.
- **BankSystem (Subsystem Proxy)**: Đóng vai trò proxy cho hệ thống ngân hàng thực tế để thực hiện các giao dịch nạp tiền.
- **Paycheck**: Lớp thực thể đại diện cho bảng lương của nhân viên.
- **BankInformation**: Lớp thực thể chứa thông tin tài khoản ngân hàng để xử lý giao dịch.

**Giao Diện (`IBankSystem`)**  
- `deposit(aPaycheck: Paycheck, intoBank: BankInformation)`: Phương thức nạp lương vào tài khoản ngân hàng chỉ định.

---

### 2. PrintService (Dịch Vụ In)

**Mô Tả:**  
Dịch Vụ In được sử dụng để tạo và in các báo cáo lương và các tài liệu liên quan khác. Nó cho phép người dùng có thẩm quyền yêu cầu in bản sao các báo cáo như một phần của quy trình quản lý lương và nhân sự.

**Sơ Đồ:**  
![Sơ Đồ PrintService](https://www.planttext.com/api/plantuml/png/Z5BBJiCm4BpxArQz08UqSAsYg292g1A7gZqWZYRT9bPTErfl2n7mPHpu97w1EEw3b1Jrv7WoExCxw-_Fhv5ZIRnUQU6MofIIv0e8CvOcrmXl0k1MPikSxDhCKwijnR5RFxlACQwW9FjQ9GayeTRsfOixDeoqa1dMh0UL5tnFikeYec75NkknK8pYGuWBc90o33EaZShG0warJ5P3ggLpiB0KA3j6ri0Dj6Lg98ZZB5ngSJyFm61GT-wb2KjBV7aLxFQzdj9NUyBuDmxjCOD7Op0D-ZASGmZdrcwsZt7YOpnZg8FVtnMSwthNvFo_MIY0mr9yuHIrP6MDArJPKNcSUk-wtx_fGHGbkyzsPaF8qI19HhTTWuEDak8esVSeQlkq_tlvqAquXOiHchb_tpy0003__mC0)

**Các Thành Phần:**  
- **PrintController**: Lớp điều khiển xử lý các yêu cầu tạo và in báo cáo.
- **IPrintService (Interface)**: Giao diện định nghĩa chức năng in báo cáo.
- **PrintService (Subsystem Proxy)**: Đóng vai trò proxy cho dịch vụ in thực tế để quản lý các yêu cầu in báo cáo.
- **Report**: Lớp thực thể đại diện cho tài liệu báo cáo.

**Giao Diện (`IPrintService`)**  
- `printReport(aReport: Report)`: Phương thức gửi báo cáo đến dịch vụ in.

---

### 3. ProjectManagementDatabase (Cơ Sở Dữ Liệu Quản Lý Dự Án)

**Mô Tả:**  
Hệ thống Cơ Sở Dữ Liệu Quản Lý Dự Án xử lý dữ liệu liên quan đến quản lý dự án, như cập nhật trạng thái dự án và truy xuất thông tin dự án. Nó tạo điều kiện cho việc giao tiếp với cơ sở dữ liệu nơi lưu trữ dữ liệu liên quan đến dự án.

**Sơ Đồ:**  
![Sơ Đồ ProjectManagementDatabase](https://www.planttext.com/api/plantuml/png/b9F1JW8n48RlVOe95_6me5Uo8GGqXaGJeWVZSLY6fT9jD-siIjGdy-0Z-GfkeRk4W2lSsiu_Cz_Cd_vyVGySe-KYKy8jfSxHOWQM4aQTAe9t0J34P9bQK-ZPo2XZuzWLKxToJ1darhoj-dru8gNCwo7jM3FPEIPKgcvbkk0RYwj3Gj8isTTwN4WcyId46KoiUIvHu0urffIL4hX2nYawyk6HqMoDWf52vs1kR9MmrOja7Gll8K6HXJXEDfUoenyIeDk5R9tdf_Bgzlc6eXwXgL7D9Mlr-4yHxEvbqx_8PyWKSjeO3hsgLO1vg7S_yRi_2cbd1mTfzXqzXUbwRTtfAB1rtPUv9uKiZNOBcVzNPz_GraMdSzc2AEf3TMume1T6SvNPKDuGNYIA9ji-egW1gY7JOuMeE4ub1gHd_bl-0W00__y30000)

**Các Thành Phần:**  
- **ProjectController**: Lớp điều khiển chịu trách nhiệm quản lý cập nhật dữ liệu dự án.
- **IProjectManagementDatabase (Interface)**: Giao diện định nghĩa chức năng tương tác với dữ liệu dự án.
- **ProjectManagementDatabase (Subsystem Proxy)**: Đóng vai trò proxy để truy cập và cập nhật cơ sở dữ liệu quản lý dự án.
- **Project**: Lớp thực thể đại diện cho một dự án.

**Giao Diện (`IProjectManagementDatabase`)**  
- `updateProject(aProject: Project)`: Phương thức cập nhật thông tin cho một dự án cụ thể trong cơ sở dữ liệu.

# 2. Analysis class to design element map

| Lớp Phân Tích              | Phần Tử Thiết Kế                                          |
|----------------------------|-----------------------------------------------------------|
| LoginForm                  | LoginForm                                                 |
| MaintainTimecardForm       | MainEmployeeForm, TimecardForm, MainApplicationForm       |
| TimecardController         | TimecardController                                        |
| SystemClockInterface       | SystemClockInterface                                      |
| PayrollController          | PayrollController                                         |
| Paycheck                   | Paycheck                                                  |
| Employee                   | Employee, EmployeeForm, EmployeeController                |
| PurchaseOrder              | PurchaseOrder, PurchaseOrderForm, PurchaseOrderController |
| BankSystemInterface        | BankSystemInterface, BankSystemProxy                      |
| PrintService               | PrintService, PrintController                             |
| ProjectManagementDatabase  | ProjectManagementDatabase, DatabaseController             |
| PaycheckCalculator         | PaycheckCalculator, SalaryCalculator                      |
| CommissionedEmployee       | CommissionedEmployeeForm, CommissionedEmployeeController  |
| EmployeeDatabase           | EmployeeDatabase, DatabaseService                         |
| PayrollDatabase            | PayrollDatabase, DatabaseController                       |
| PaymentMethod              | PaymentMethod, DirectDeposit, CheckPayment                |
| Timecard                   | Timecard, TimecardEntryForm                               |
| BankInformation            | BankInformation, BankService                              |

# 3. Design element to owning package map

| Design Element            | Owning Package                          |
|---------------------------|-----------------------------------------|
| LoginForm                 | Middleware::Security:GUI Framework      |
| MainEmployeeForm          | Applications::Employee Activities       |
| TimecardForm              | Applications::Employee Activities       |
| MainApplicationForm       | Middleware::Security:GUI Framework      |
| TimecardController        | Applications::Employee Activities       |
| SystemClockInterface      | Applications::Payroll                   |
| PayrollController         | Applications::Payroll                   |
| Paycheck                  | Business Services::Payroll Artifacts    |
| Employee                  | Applications::Employee Activities       |
| PurchaseOrder             | Business Services::Purchase Management  |
| BankSystemInterface       | Business Services::Bank Integration     |
| PrintService              | Business Services::Printing             |
| ProjectManagementDatabase | Infrastructure::Database Management     |
| PaycheckCalculator        | Business Services::Payroll Artifacts    |
| CommissionedEmployee      | Applications::Employee Activities       |
| EmployeeDatabase          | Infrastructure::Database Management     |
| PayrollDatabase           | Infrastructure::Database Management     |
| PaymentMethod             | Business Services::Payment Integration  |
| Timecard                  | Applications::Employee Activities       |
| BankInformation           | Business Services::Bank Integration     |

