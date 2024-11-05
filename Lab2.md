# 1. Ca sử dụng Login

## Các lớp phân tích:
- **Controll:** LoginControll
- **Boundary:** LoginForm
- **Entities:** Account

## Biểu đồ Squence

![Diagram](https://www.planttext.com/api/plantuml/png/Z9112W9H28RtdaBQTu4MqQ8MGOieQY_lIJnmd46jcBErw4XTeLSDLBJ9XUZlfwAtotNcGHR7He1Ij8OxPuEkIYMLZZHmjARUMX7SzXxSZ91y204UC8wdGuuJN6XKvLXbfOQHD6D7xkVMCWpG9xudAPc2CHbdrYWa3a0IhygNZDNU8vwR9xXg3rWKM9nngQV_ckR5Ew4UsQmUtB0x7VY9_jopuR0UAvL84mkmPe1PzO-7tG400F__0m00)

## Nhiệm vụ và quan hệ của các lớp phân tích

### 1. **Lớp LoginControll**
- Nhiệm vụ: Điều khiển đăng nhập
- Một số phương thức:
1. `validate()`: Xác thực tên đăng nhập và mật khẩu,
2. `login()`: Thực hiện đăng nhập,
3. `checkLogin()`: Kiểm tra đăng nhập,
4. `displayError()`: Hiển thị lỗi,
5. `cancelLogin()`: Hủy đăng nhập

### 2. **Lớp LoginForm**
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

### 3. **Lớp Account**
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

## Quan hệ giữa các lớp phân tích
### 1. **LoginControll**
- **Liên kết với LoginForm**: 
  - **Quan hệ**: `LoginControll` sẽ tạo và điều khiển một phiên bản của `LoginForm`. Nó sử dụng `LoginForm` để thu thập thông tin đăng nhập từ người dùng.
  - **Phương thức sử dụng**: `LoginForm.getName()`, `LoginForm.getPassword()`, `LoginForm.showError()`, `LoginForm.resetFields()`, `LoginForm.onCancel()`.
  
- **Liên kết với Account**: 
  - **Quan hệ**: `LoginControll` sẽ tương tác với lớp `Account` để thực hiện việc xác thực tên đăng nhập và mật khẩu.
  - **Phương thức sử dụng**: `Account.validateCredentials()`, `Account.lockAccount()` (nếu cần).

### 2. **LoginForm**
- **Liên kết với LoginControll**: 
  - **Quan hệ**: `LoginForm` nhận thông tin từ người dùng và gửi thông tin đó đến `LoginControll` khi người dùng thực hiện hành động đăng nhập.
  - **Phương thức sử dụng**: `onLoginButtonClick()` (gọi `LoginControll.login()`).
  
- **Liên kết với người dùng (User)**: 
  - **Quan hệ**: `LoginForm` trực tiếp tương tác với người dùng để nhận đầu vào và hiển thị thông báo.

### 3. **Account**
- **Liên kết với LoginControll**: 
  - **Quan hệ**: `Account` đại diện cho dữ liệu tài khoản người dùng và cung cấp các phương thức xác thực cho `LoginControll`.
  - **Phương thức sử dụng**: `validateCredentials()`, `lockAccount()`.

## Tổng kết các quan hệ:
- **LoginControll** là bộ điều khiển chính, kết nối `LoginForm` và `Account`.
- **LoginForm** là giao diện người dùng, cung cấp thông tin đăng nhập và nhận phản hồi từ `LoginControll`.
- **Account** là mô hình dữ liệu, chứa thông tin và logic xác thực liên quan đến tài khoản.

## Biểu đồ lớp phân tích

![Diagram](https://www.planttext.com/api/plantuml/png/V9B1QiCm38RlUGeV4rXU88VI4jPJ6OKzWMUBn5IHYkKqZB4dss6Fj5TOtCGZ3M6-MVhrIv_idw_llGJjGzzXPb2Bg1CtZcgcu1bHVMGgdfj6PtM0l9Zk64NfObembzCoOfrSKRy_Uyy-xq14Dr2fr-0TDQb8am5CLP_PilkHVJTtBabtS7I0DjLFuUie7jZRZPIJ-kvTgJTc14rJmmR2o-YL5m_g63xFNkkKj3pyX-118Dm7a0JEDFLU8XsCuPv20ke5V8JQvbcZ74nmDrYXfDUeFLYWu3HAlhHyKckxOkM0R2xpN6dqdZQ2fjNKmD-228RpsZc2FlwPijmjth5IdQPnUQ9s6xgqd4gDUucIFP2Dd_4N003__mC0)

# Ca sử dụng Maintain Employee Information

# Code Java mô phỏng ca sử dụng Maintain Timecard

```python
import java.util.*;

class ChargeNumber {
    private String code;
    private String projectName;

    public ChargeNumber(String code, String projectName) {
        this.code = code;
        this.projectName = projectName;
    }

    public String getCode() {
        return code;
    }

    public String getProjectName() {
        return projectName;
    }

    @Override
    public String toString() {
        return code + " - " + projectName;
    }
}

class Timecard {
    private Employee employee;
    private Date startDate;
    private Date endDate;
    private Map<ChargeNumber, Integer> hoursWorked;
    private boolean isSubmitted;
    private Date submittedDate;

    public Timecard(Employee employee, Date startDate, Date endDate) {
        this.employee = employee;
        this.startDate = startDate;
        this.endDate = endDate;
        this.hoursWorked = new HashMap<>();
        this.isSubmitted = false;
    }

    public boolean isSubmitted() {
        return isSubmitted;
    }

    public void submitTimecard() {
        if (isSubmitted) {
            System.out.println("Error: Timecard already submitted.");
            return;
        }
        this.submittedDate = new Date();
        this.isSubmitted = true;
        System.out.println("Timecard submitted on " + submittedDate);
    }

    public void enterHours(ChargeNumber chargeNumber, int hours) {
        if (hours > 24 || hours < 0) {
            System.out.println("Error: Invalid number of hours. Must be between 0 and 24.");
            return;
        }

        if (hours + getTotalHours() > employee.getMaxHours()) {
            System.out.println("Error: Exceeds maximum allowable hours for employee.");
            return;
        }

        hoursWorked.put(chargeNumber, hours);
        System.out.println("Entered " + hours + " hours for project " + chargeNumber.getProjectName());
    }

    public int getTotalHours() {
        return hoursWorked.values().stream().mapToInt(Integer::intValue).sum();
    }

    public void printTimecard() {
        System.out.println("Timecard for " + employee.getName() + " (" + startDate + " to " + endDate + ")");
        if (hoursWorked.isEmpty()) {
            System.out.println("No hours recorded.");
        } else {
            for (Map.Entry<ChargeNumber, Integer> entry : hoursWorked.entrySet()) {
                System.out.println("Project: " + entry.getKey().getProjectName() + " - Hours: " + entry.getValue());
            }
        }
    }
}

class Employee {
    private String name;
    private String id;
    private int maxHours;

    public Employee(String name, String id, int maxHours) {
        this.name = name;
        this.id = id;
        this.maxHours = maxHours;
    }

    public String getName() {
        return name;
    }

    public String getId() {
        return id;
    }

    public int getMaxHours() {
        return maxHours;
    }
}

class TimecardSystem {
    private Map<String, Timecard> timecards;
    private List<ChargeNumber> chargeNumbers;

    public TimecardSystem() {
        this.timecards = new HashMap<>();
        this.chargeNumbers = new ArrayList<>();
        loadChargeNumbers();
    }

    private void loadChargeNumbers() {
        chargeNumbers.add(new ChargeNumber("CN001", "Project Alpha"));
        chargeNumbers.add(new ChargeNumber("CN002", "Project Beta"));
        chargeNumbers.add(new ChargeNumber("CN003", "Project Gamma"));
    }

    public Timecard getTimecardForEmployee(Employee employee, Date startDate, Date endDate) {
        String key = employee.getId() + "-" + startDate.toString() + "-" + endDate.toString();
        return timecards.get(key);
    }

    public void createOrUpdateTimecard(Employee employee, Date startDate, Date endDate) {
        Timecard timecard = getTimecardForEmployee(employee, startDate, endDate);
        if (timecard == null) {
            timecard = new Timecard(employee, startDate, endDate);
            timecards.put(employee.getId() + "-" + startDate.toString() + "-" + endDate.toString(), timecard);
            System.out.println("New timecard created for employee: " + employee.getName());
        }
        timecard.printTimecard();
    }

    public void submitTimecard(Employee employee, Date startDate, Date endDate) {
        Timecard timecard = getTimecardForEmployee(employee, startDate, endDate);
        if (timecard != null) {
            timecard.submitTimecard();
        } else {
            System.out.println("Error: Timecard not found.");
        }
    }

    public List<ChargeNumber> getChargeNumbers() {
        return chargeNumbers;
    }
}

public class MaintainTimecardApp {
    public static void main(String[] args) {
        Employee employee = new Employee("John Doe", "E123", 40); // Max 40 hours/week
        TimecardSystem system = new TimecardSystem();
        Date startDate = new GregorianCalendar(2024, Calendar.OCTOBER, 1).getTime();
        Date endDate = new GregorianCalendar(2024, Calendar.OCTOBER, 7).getTime();

        // Step 1: Create a timecard
        system.createOrUpdateTimecard(employee, startDate, endDate);

        // Step 2: Enter hours worked
        Timecard timecard = system.getTimecardForEmployee(employee, startDate, endDate);
        timecard.enterHours(system.getChargeNumbers().get(0), 8);  // 8 hours for Project Alpha
        timecard.enterHours(system.getChargeNumbers().get(1), 6);  // 6 hours for Project Beta

        // Step 3: Submit the timecard
        system.submitTimecard(employee, startDate, endDate);

        // Step 4: Attempt to modify after submission
        timecard.enterHours(system.getChargeNumbers().get(2), 10);  // This should show error
    }
}
```
