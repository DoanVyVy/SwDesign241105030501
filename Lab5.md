# Thiết Kế Hệ Thống Payroll

## Mô Tả Hệ Thống
Hệ thống Payroll quản lý quá trình tính toán và trả lương cho nhân viên trong công ty. Hệ thống bao gồm các chức năng đăng nhập, nhập thông tin giờ làm việc, tính toán lương, tạo phiếu lương, báo cáo lương và phân quyền bảo mật người dùng.

### 1. Hệ Thống Đăng Nhập
**Mô Tả:** Hệ thống xác thực người dùng trước khi truy cập vào các chức năng của hệ thống.

**Chức Năng:**
- Nhập tên đăng nhập và mật khẩu.
- Kiểm tra tính hợp lệ của thông tin.
- Phân quyền người dùng dựa trên vai trò (nhân viên, quản lý, bộ phận nhân sự).
- Cung cấp thông báo nếu tài khoản không hợp lệ hoặc bị khóa.

**Lý Do Thiết Kế:**
Bảo mật và phân quyền người dùng, ngăn chặn truy cập trái phép vào các chức năng của hệ thống.

---

### 2. Hệ Thống Nhập Thông Tin Giờ Làm Việc
**Mô Tả:** Hệ thống cho phép nhân viên nhập giờ làm việc vào hệ thống để tính toán lương.

**Chức Năng:**
- Nhân viên nhập số giờ làm việc.
- Kiểm tra tính hợp lệ của giờ làm việc (ví dụ, số giờ không được vượt quá quy định).
- Lưu dữ liệu vào cơ sở dữ liệu.

**Lý Do Thiết Kế:**
Đảm bảo tính chính xác và minh bạch trong việc tính toán lương, giảm thiểu lỗi khi nhập thông tin giờ làm việc.

---

### 3. Hệ Thống Tính Toán Lương
**Mô Tả:** Tính toán lương của nhân viên dựa trên các thông tin đã nhập như giờ làm việc, lương cơ bản, phụ cấp, các khoản trừ.

**Chức Năng:**
- Truy xuất dữ liệu từ cơ sở dữ liệu.
- Áp dụng công thức tính lương: lương cơ bản + phụ cấp - các khoản trừ.
- Lưu kết quả vào cơ sở dữ liệu.
- Hiển thị thông báo hoàn tất khi tính lương xong.

**Lý Do Thiết Kế:**
Tự động hóa quy trình tính toán lương, giảm thiểu sai sót và tiết kiệm thời gian.

---

### 4. Hệ Thống Tạo Phiếu Lương
**Mô Tả:** Tạo phiếu lương cho nhân viên, có thể xuất ra dưới dạng PDF hoặc Excel.

**Chức Năng:**
- Truy xuất dữ liệu lương từ cơ sở dữ liệu.
- Tạo phiếu lương theo định dạng yêu cầu.
- Gửi phiếu lương qua email hoặc lưu lại để tải xuống.

**Lý Do Thiết Kế:**
Đảm bảo tính chính xác và minh bạch trong việc thông báo lương cho nhân viên.

---

### 5. Hệ Thống Tạo Báo Cáo Lương
**Mô Tả:** Tạo báo cáo tổng hợp về tình hình lương trong công ty, giúp quản lý theo dõi và phân tích.

**Chức Năng:**
- Nhập các tiêu chí báo cáo (tháng, năm, phòng ban, nhân viên cụ thể).
- Tổng hợp và tạo báo cáo lương.
- Xuất báo cáo dưới dạng PDF hoặc Excel.
- Thông báo nếu không có dữ liệu phù hợp.

**Lý Do Thiết Kế:**
Giúp quản lý dễ dàng theo dõi và phân tích chi phí lương trong công ty.

---

### 6. Hệ Thống Quản Lý Phân Quyền và Bảo Mật
**Mô Tả:** Đảm bảo bảo mật và phân quyền cho người dùng trong hệ thống.

**Chức Năng:**
- Đảm bảo người dùng chỉ có thể truy cập các chức năng mà họ có quyền thực hiện.
- Quản lý quyền hạn người dùng dựa trên vai trò (nhân viên, quản lý, bộ phận nhân sự).

**Lý Do Thiết Kế:**
Ngăn chặn truy cập trái phép và bảo vệ dữ liệu nhạy cảm trong hệ thống.

---

### 7. Hệ Thống Quản Lý Mở Rộng và Linh Hoạt
**Mô Tả:** Hệ thống được thiết kế để dễ dàng mở rộng trong tương lai, có thể thêm các chức năng mới như quản lý thưởng, nghỉ phép mà không ảnh hưởng đến các chức năng hiện tại.

**Chức Năng:**
- Cho phép mở rộng các module mà không gây ảnh hưởng đến hoạt động của hệ thống hiện tại.
- Cung cấp API và các cơ chế để tích hợp các tính năng mới.

**Lý Do Thiết Kế:**
Tạo ra một hệ thống linh hoạt, có thể đáp ứng các yêu cầu thay đổi trong tương lai.

---

## Sơ Đồ Các Hệ Thống Con (Subsystems)


Hệ thống Quản Lý Phân Quyền và Bảo Mật hoạt động song song với tất cả các hệ thống con để đảm bảo bảo mật.  
Hệ thống Quản Lý Mở Rộng và Linh Hoạt luôn sẵn sàng để hỗ trợ việc tích hợp thêm tính năng mới.

---

## UML Diagrams

### 1. Use Case Diagram (Sơ đồ ca sử dụng)
![Use Case Diagram](https://www.planttext.com/api/plantuml/png/P9AnIWD148RxUOhX-XJ69AK4HKXZY44VOBqiTmUNkNYt9mIn40jRBIq4evqGY63ZBP9YGzvZdy1NSB9SpYGsm-p-t_mxC-oFdhSp9LAL3sC0uQiaHQyRcbV2gyYyauSYm-FXA4x6KgxrqzmMRuIn-NRoYI0Ho7Ij7bhzXAFG5bD2SawPrH-ExFG1KkahGK4iqUjOVOygjFgH0ko9SPh4iOVNW9XdqXSP8uk7nHsBjB8REO_pexrDeEiKTZ6VpAc8C8YiVkRcNeOy0h_WbsNrpR8pCwKGLM8cFCTojfnGK6BxMvWj9WaF4zbYdk-0ZV_WXU7Why8ssjn4Usudb_dOwblUKB2SSRyH3inNnRVW1c2zTQpL3jpKEnTrA1TV0TldVUZqAwbA6tzf4rWfynP0Mz9WzGj-0G00__y30000)

---

### 2. Sequence Diagrams (Sơ đồ tuần tự)

#### Đăng Nhập (Login)
![Login Sequence Diagram](https://www.planttext.com/api/plantuml/png/P9AnIWD148RxUOhX-XJ69AK4HKXZY44VOBqiTmUNkNYt9mIn40jRBIq4evqGY63ZBP9YGzvZdy1NSB9SpYGsm-p-t_mxC-oFdhSp9LAL3sC0uQiaHQyRcbV2gyYyauSYm-FXA4x6KgxrqzmMRuIn-NRoYI0Ho7Ij7bhzXAFG5bD2SawPrH-ExFG1KkahGK4iqUjOVOygjFgH0ko9SPh4iOVNW9XdqXSP8uk7nHsBjB8REO_pexrDeEiKTZ6VpAc8C8YiVkRcNeOy0h_WbsNrpR8pCwKGLM8cFCTojfnGK6BxMvWj9WaF4zbYdk-0ZV_WXU7Why8ssjn4Usudb_dOwblUKB2SSRyH3inNnRVW1c2zTQpL3jpKEnTrA1TV0TldVUZqAwbA6tzf4rWfynP0Mz9WzGj-0G00__y30000)

#### Nhập Thông Tin Giờ Làm Việc
![Nhập Thông Tin Giờ Làm Việc](https://www.planttext.com/api/plantuml/png/R94zQiD048NxFSL3lI-G8XZ_GC31JPgqGbuamUvOIAE0wXIfKlW08NRI6KnIfCeMBXPyZpr1hf2HxHX1LC_tlJV3_BZziEAuvDeQ5IUyB17DC_z6UCZzbYB45QQsCCj6QwM9SsuGtGJt1Cw2Mr5w9EwQYhMzpCU73QhWNh48xWCc5xm-SfEHKdzf65oVFLnXB67F1Ch2zwv0AiOBZ5zRsKBaf5-QdsXfMlKePwmhp6JoQC5b3FOxoY2jxmMCy1ryCXBqzl1Poud-Yr9mJZtvWWswuVT-avmE81YnEucNxVzJRSTQDadQ9gM6cXRj9tu1003__mC0)

#### Tính Toán Lương
![Tính Toán Lương](https://www.planttext.com/api/plantuml/png/T94zJiD044RxFSN8VIv0WQ8a1GKK20fQurYsXJq6UpR29HKL1GT0sA0K84MaeBA5KepaU-m9k0BZ7o8dKfejTj_CzsRsjzgCKx8Jqb6eR8VY1AnpRSftX91_BB1JEBFHzjn4kKW1PM2TcEeHo3VLCtejS96bv4RRzsbTG6ggLvYRwWl2G73TShE9Kdqp61ttPN04K-drX42yGXyevaAowtLTeATwHkZPHCZBH6TmBtfB4WF-HWyeG42Vtn0M0N_AoJbualaY_daabnBlAAaUxKHgANMap-tGSX2t9VcXHPODtmMAxOVJsnxmFAtN6cvCkI6uQvQvH-_RN77Xo12cNBMJ3pt-zoMpT_DUSn637tCk2-lsiDDQZLsSDt-f_W000F__0m00)

---

### 3. Class Diagram (Sơ đồ lớp)
![Class Diagram](https://www.planttext.com/api/plantuml/png/T54nQWCn4Epl5Oihk_07hWZ6HKWHGi21r6kTE8lihGwj53X27f8oAGq6fyqLAGp-nxqWNyYTo2KMEEeqCxip6dsrdmlnw7oeA5E48Z2vsHpU61xDOSiJUCgWFwQ075RU6IxZdR7IAUAjHxgomSczTGzwq5-IHHz9GKBN9912Ke7GwrNafhDVzZaRWrmVzyTNBiSGQvGVTR9fRJb8WXIw2CeRotBUycx8UjPnsRKlK6-wZnq3nngaQz_70ChfVleM6o5JJtLLastqqCD9OxE_MlgrQPVp-SN9et88eYNxrpEga_aSAcGi-w65vcBuiMy0003__mC0)

---

### 4. Activity Diagram (Sơ đồ hoạt động)
![Activity Diagram](https://www.planttext.com/api/plantuml/png/V90nQiCm68LtdUADpXNieTbR2eKi7OEZMABoRpUM0faxz1IbSJCK0g4PEacK30BVGoVe5IgBG5ietHxlFVxlvtswqxJJyvKsjM99iFnQ-1V2MlezWKImXnQL3Eu9oc_hw0VtM1OilupYeOPUpQ7zWGH4SBiMAiO5aqjaC-7VgOAMz2Ewc40BJiWsl9im8ByQZWPhlsrG3Zswu9wn2EuDQkIOOgpSc61t5F4VsFYzGHdigpb3rN0SUgfIRvOStVYUVla9SHViIUD-FFKVZgkE8wCc_NRxJJiFeOBjvLzpS5h8PLomQTaqwd7EBm000F__0m00)

---

### 5. Component Diagram (Sơ đồ thành phần)
![Component Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bT1Od9sOdggWfB7mztj2YKP3tTFp4jN24YiBChFoL5IgEPIK8ZsoK_Fp5C8JYqgoqnEZGM9X6JcfYguvfKKLQ881oVc90A5d1Dpaajp4aioyr5r0KqjpiaiK71FpKijmfGEIYt8Boh915eF5wtbuaApNK5Nrmwx_TW48QhnEGkV94GtFbTZSJDXAnrIyr90GGy0003__mC0)

