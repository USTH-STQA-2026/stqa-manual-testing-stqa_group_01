# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày tạo** | `16/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| TC_REQ07_01 | Kiểm tra quyền thêm thành viên của tài khoản không phải thủ thư | Đã đăng nhập tài khoản thành viên | Kiểm tra sự xuất hiện của icon "Thêm thành viên" trên góc phải | Login: ba.nguyen@email.com, Password: password123 | Icon "Thêm thành viên" không xuất hiện | REQ-07 | Decision Table (Phân quyền) |
| TC_REQ07_2 | Kiểm tra khi thiếu mục "Họ và tên" thì hệ thống có báo lỗi không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập email và SĐT hợp lệ, bỏ trống Họ và tên. Nhấn nút "Thêm". | Email: noname@email.com, SĐT: 0123456791 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi thiếu Họ và tên. | REQ-07 | Decision Table |
| TC_REQ07_3 | Kiểm tra hệ thống có chặn email thiếu @ không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập Họ tên và SĐT hợp lệ. Nhập email có dấu "." nhưng thiếu "@". Nhấn nút "Thêm". | Họ tên: Vũ Hải, Email: haivuemail.com, SĐT: 0133456798 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi định dạng email không hợp lệ. | REQ-07 | EP / BVA |
| TC_REQ07_4 | Kiểm tra hệ thống có chặn email thiếu dấu . ở domain hay không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập Họ tên và SĐT hợp lệ. Nhập email có "@" nhưng thiếu dấu "." ở sau đó. Nhấn nút "Thêm". | Họ tên: Trần Đạt, Email: trandat@emailcom, SĐT: 0123456798 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi định dạng email không hợp lệ. | REQ-07 | EP / BVA |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|Thêm thành viên mới|04|REQ-07|EP, BVA|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
