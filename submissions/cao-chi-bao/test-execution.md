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
|01|Độc quyền Thêm thành viên (của thủ thư)|Icon "Thêm thành viên" không xuất hiện|Icon "Thêm thành viên không xuất hiện trên tài khoản người mượn sách|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC01.png)|---|
|02|Thêm thành viên đầy đủ Họ và tên| Hệ thống báo lỗi do thiếu thông tin Họ và tên | Hệ thống phản hồi "Họ tên không được để trống"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC02.png)|---|
|03|Kiểm tra khả năng check cú pháp email| Hệ thống báo lỗi do email thiếu "@"| Hệ thống phản hồi "Email không hợp lệ"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC03.png)|---|
|04|Kiểm tra khả năng check cú pháp email| Hệ thống báo lỗi do email thiếu dấu "."| Thêm thành công thành viên mới dù email không hợp lệ|Chức năng không hoạt động|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC04.png)|email không hợp lệ vẫn được thêm thành công|
|05|Kiểm tra hoạt động cơ bản của tính năng Thêm thành viên| Hệ thống thêm thành viên thành công| Hệ thống báo email không hợp lệ|Chức năng không hoạt động|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC04.png)|Không thể thêm thành viên dù không mắc lỗi khi nhập thông tin|


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
