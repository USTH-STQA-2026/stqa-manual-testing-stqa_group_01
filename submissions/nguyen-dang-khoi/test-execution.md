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
|01|Đăng nhập vào hệ thống|Đăng nhập thành công với tài khoản trong hệ thống, thất bại nếu tài khoản không tồn tại|Thành công đăng nhập nếu đúng tài khoản và mật khẩu, thông báo mật khẩu hoặc tài khoản sai nếu thất bại|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/TC01.png)|Email không theo dạng example@gmail.com vẫn có thể đăng nhập bình thường|
| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|----------|------------|-----|
|TC-01|Mượn sách|Sách chuyển sang trạng thái "Đang mượn"|Thành công chuyển sang trạng thái đã mượn|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.41.40.png)|không có|
|TC-02|Mượn sách|Không thể mượn quá 3 quyển, hiển thị thông báo lỗi|Mượn thành công 4 quyển mới báo lỗi|Chức năng không hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.47.49.png)|Lỗi mượn sách quá số lượng cho phép|
|TC-03|Trả sách|Sách chuyển sang trạng thái "Đã trả"|Thành công chuyển sang trạng thái đã trả|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.49.03.png)|không có|
|TC-04|Hiển thị thông tin mượn sách|Thành viên thấy sách mình mượn, Thủ thư thấy tất cả sách được mượn|Chức năng hoạt động bình thường|Thành công hiển thị sách đang mượn đối với thủ thư|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.54.03.png)|không có|

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
