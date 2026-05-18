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
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
|01|Trả sách|Sau khi trả sách, sách trở về trạng thái "Có sẵn"|Sau khi trả sách, sách đã trở về trạng thái "Có sãn"|Hoạt động như mong đợi|||
|02|Trả sách|Sau khi trả sách quá hạn, hệ thống hiển thị **cảnh báo quá hạn**|Sau khi trả sách quá hạn, hệ thống chỉ hiện thị mỗi "trả sách thành công"|Chưa hoạt động theo yêu cầu||Hệ thống không hiển thị **cảnh báo quá hạn**|
|03|Trả sách|Sách đã trả ở trạng thái "Có sẵn"|Sách đã trở về trạng thái "Có sẵn"|Hoạt động như mong đợi|||


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
