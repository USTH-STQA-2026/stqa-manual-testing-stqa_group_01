# Test Cases — Bảng trường hợp kiểm thử

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày tạo** | `16/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### REQ-02: Xem danh sách sách / View Book List

| Mục | Nội dung |
|-----|---------|
| **Mô tả** | Hiển thị tất cả sách trong thư viện |
| **Thông tin mỗi sách** | Tên sách, tác giả, thể loại, năm xuất bản, trạng thái (Có sẵn / Đã mượn) |
| **Quyền truy cập** | Cả Thủ thư và Thành viên đều xem được |
| **Cập nhật real-time** | Khi sách được mượn/trả → trạng thái cập nhật ngay lập tức |

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|--------|
|TC-01|Tính năng mượn sách|Đăng nhập vào thành viên đang hoạt động|Nhấn vào dấu cộng của những quyển sách đang có sẵn|Nhấn vào dấu cộng của từng quyển sách|Chuyển sang trạng thái đang mượn, hiển thị sách "Đang mượn" đối với người khác và hiện nút trả sách đối vớ người mượn|REQ-02|EP|
|TC-02|Tính năng trả sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|Nhấn vào nút trả sách đang mượn đối với thành viên, nhấn nút trả sách khi quá hạn đối với thủ thư|Nhấn trả sách|Hiện "Đã trả" và hiện "Có sẵn" và nút dấu cộng đối với người mượn và thành viên khác|REQ-02|State Transition|
|TC-03|Hiển thị thông tin mượn sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|1. Đăng nhập vào tài khoản thành viên đang hoạt động <br> 2. Mượn sách <br> 3. Đăng nhập vào tài khoản thủ thư <br> 4. Kiểm tra sách được mượn|Thành viên mượn sách|Thủ thư thấy sách được mượn|REQ-02|Decision Table|
|TC-04|Hiển thị đầy đủ thông tin sách|Đăng Nhập vào một tài khoản bất kì|Nhìn thông tin sách ở dưới tên của sách|Hiển thị đầy đủ tên tác giả, thể loại, năm sản xuất, mã sách|EP|
|TC-05|Hiển thị trạng thái của sách|Đăng nhập vào một tài khoản bất kì|Nhìn vào trạng thái của sách|Hiển thị đúng trạng thái, tình trạng của từng quyển sách|Nếu đang được mượn hiện "Đang mượn", có sẵn hiện "Có sẵn", thất lạc hiện "Thất lạc"|EP|

---

## Tổng hợp trong phạm vi REQ-02

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
|Mượn Sách|1|REQ-02|EP|
|Trả Sách|1|REQ-02|State Transition|
|Hiển thị thông tin mượn sách|1|REQ-02|Decision Table|
|Tổng|3|1 REQ|EP, State Transition, Decision Table|
