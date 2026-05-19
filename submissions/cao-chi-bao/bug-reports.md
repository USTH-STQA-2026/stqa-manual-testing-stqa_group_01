# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `19/05/2026` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-04` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Cao Chí Bảo` |
| **Ngày phát hiện** | `19/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
`Hệ thống chấp nhận email sai format khi thêm thành viên`

**Môi trường:**
- Trình duyệt: Chrome `148`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`Đăng nhập tài khoản thủ thư, truy cập chức năng thêm thành viên`

**Bước tái hiện:**
1. `Truy cập hệ thống mượn sách https://stqa.rbc.vn/ và đăng nhập vào tài khoản thủ thư`
2. `Click icon "Thêm thành viên" ở góc phải`
3. `Nhập thông tin đầy đủ về Họ và tên và SĐT cùng email thiếu "@"`

**Kết quả mong đợi:**
`Hệ thống báo lỗi do email sai cú pháp`

**Kết quả thực tế:**
`Thêm thành viên thành công`

**Tác động:**
`Hệ thống bị lưu dữ liệu sai, gây lỗi khi gửi email thông báo mượn/trả sách sau này.`

**Minh chứng:**
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC04.png)

**Đề xuất xử lý:**
`Bổ sung/ kiểm tra lại hàm kiểm tra định dạng để chặn và báo lỗi ngay tại ô Email.` 

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `TC-05` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Cao Chí Bảo` |
| **Ngày phát hiện** | `19/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
`Hệ thống không cho phép thêm thành viên với thông tin đầy đủ và hợp lệ`

**Bước tái hiện:**
1. `Truy cập hệ thống mượn sách https://stqa.rbc.vn/ và đăng nhập vào tài khoản thủ thư`
2. `Click icon "Thêm thành viên" ở góc phải`
3. `Nhập các thông tin đầy đủ và đúng cú pháp`

**Kết quả mong đợi:**
`Hệ thống báo thêm thành viên thành công`

**Kết quả thực tế:**
`Hệ thống báo email không hợp lệ`

**Tác động:**
`<!-- -->`

**Minh chứng:**
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/)

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
