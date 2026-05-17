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
| 01 | Kiểm tra tính không phân biệt chữ HOA/thường (case-Insensitivity) khi tìm kiếm sách.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"| Bước 1. Ấn vào hộp tìm kiếm 2. Gõ "nGuyễn mInh ĐứC" 3. Kiểm tra kết quả tìm đuọc và xoá phần nhập 4. Gõ "lẬp trìnH flUTTer cơ bẢn" 5. Kiểm tra kết quả tìm đuọc| "nGuyễn mInh ĐứC" và "lẬp trìnH flUTTer cơ bẢn"| Sau bước 3, ệ thống lọc và hiển thị chính xác 2 cuốn sách của tác giả: mã BOOK001 (Lập trình Flutter cơ bản) và BOOK009 (Nhập môn lập trình Python). Các sách khác sẽ bị ẩn. Sau bước 6, hệ thống lọc và hiển thị duy nhất 1 cuốn sách: mã BOOK001 (Lập trình Flutter cơ bản).| REQ-03 | EP và Black-box Testing|
| 02 | Kiểm tra tính năng "tìm kiếm theo Tên sách, Tên tác giả" và xử lý khi không có dữ liệu khớp.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"| Bước 1. Nhấp chuột vào thanh tìm kiếm. 2. Nhập vào Tên tác giả và xác nhận bộ lọc. 3. Xóa thanh tìm kiếm, nhập vào Tên sách cụ thể. 4. Xóa thanh tìm kiếm, nhập vào một chuỗi ký tự không tồn tại.| "Nguyễn Minh Đức", "Lập trình Flutter cơ bản" và "ABCxyz123"| Sau bước 2, sẽ hiển thị thông  cuốn sách với mã BOOK001 (Lập trình Flutter cơ bản) và BOOK009 (Nhập môn lập trình Python); Sau bước 3, Hiển thị duy nhất 1 cuốn sách mã BOOK001 (Lập trình Flutter cơ bản); Sau bước 4 sẽ hiển thị kết quả chuỗi chính xác "Không tìm thấy sách nào"| REQ-3| EP và Black-box Testing|

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
