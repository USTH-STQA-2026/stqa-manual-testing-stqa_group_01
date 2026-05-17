# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `17/05/2026` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-04 |
| **REQ liên quan** | REQ-01 |
| **Mức độ** | Medium |
| **Người phát hiện** | Nguyễn Anh Tuấn |
| **Ngày phát hiện** | `17/05/2026` |
| **Trạng thái** | Open |

**Tiêu đề:**
Hệ thống chấp nhận email không đúng định dạng trong chức năng đăng nhập

**Môi trường:**
- Trình duyệt: Firefox
- Hệ điều hành: Ubuntu Linux
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
- Tài khoản thành viên đã được tạo trong hệ thống với email không đúng định dạng: example@email
- Người dùng đang ở màn hình đăng nhập

**Bước tái hiện:**
1. Mở trang đăng nhập của hệ thống.
2. Nhập email: example@email
3. Nhập mật khẩu đúng tương ứng với tài khoản.
4. Nhấn nút Đăng nhập.

**Kết quả mong đợi:**
Hệ thống phải từ chối email không đúng định dạng theo quy tắc: `email@domain.ext`
Hiển thị thông báo lỗi phù hợp và không cho phép đăng nhập.

**Kết quả thực tế:**
Hệ thống chấp nhận email `example@email` và cho phép đăng nhập thành công vào hệ thống.

**Tác động:**
Hệ thống cho phép dữ liệu email không hợp lệ tồn tại và được sử dụng trong quá trình xác thực. Điều này có thể làm giảm tính toàn vẹn dữ liệu,
gây lỗi ở các chức năng sử dụng email sau này, tạo sự mâu thuẫn so với SRS của hệ thống.

**Minh chứng:**
1. Tài khoản có email không đúng định dạng được tạo bởi thủ thư
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/librarian_creating_account.png)
2. Đăng nhập bằng tài khoản trên tại trang đăng nhập
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/login_with_invalid_email_form.png)
3. Hệ thống cho phép đăng nhập bình thường
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/successful_login.png)

**Đề xuất xử lý:**
Bổ sung kiểm tra định dạng email tại:
- chức năng tạo tài khoản,
- chức năng đăng nhập.
Chỉ chấp nhận email đúng định dạng theo quy tắc: `email@domain.ext`

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
