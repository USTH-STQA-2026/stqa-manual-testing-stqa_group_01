# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày thực thi** | `16/05/2026` |
| **Trình duyệt** | Chrome + Firefox |
| **Hệ điều hành** | Windows + MacOS + Linux |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Đăng nhập | Đăng nhập thành công với email và mật khẩu hợp lệ | Hệ thống chuyển sang trang chủ và hiển thị tên người dùng trên AppBar |Pass |![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/normal%20login)|-|
| TC-02 | Đăng nhập | Hiển thị lỗi khi email không tồn tại | Hệ thống hiển thị thông báo “Không tìm thấy thành viên” | Pass | |-|
| TC-03 | Đăng nhập | Hiển thị lỗi khi mật khẩu không đúng | Hệ thống hiển thị thông báo “Mật khẩu không đúng” | Pass | |-|
| TC-04 | Đăng nhập | Từ chối email không đúng định dạng và không cho phép đăng nhập | Hệ thống chấp nhận email `example@email` và đăng nhập thành công | Fail | | BUG-01 |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
