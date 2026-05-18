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

### IDM — Trả sách (REQ-05)
| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Đang mượn | BOOK013 | Cho phép trả sách |
| | Đã trả | BOOK005 | Sách chuyển về trạng thái "Có sẵn"  |
| Sách quá hạn? | Quá hạn | BOOK003 | Hiển thị **cảnh báo quá hạn** |
| | Không quá hạn | BOOK013 | Không hiển thị **cảnh báo quá hạn** |

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
| 01 | Trả sách đang mượn | Sách đang ở trạng thái "đang mượn" | 1. Vào mục "Mượn/Trả" 2. Ấn nút "trả sách" của phiếu mượn đang ở trạng thái "đang mượn" 3. Quay lại mục "Sách" và kiểm tra trạng thái sách vừa trả | Thành viên có phiếu mượn ban đầu sách BOOK013 | Sách trở về trạng thái "có sẵn" | REQ-05 | EP |
| 02 | Hiển thị **cảnh báo quá hạn** | Sách quá hạn đang ở trạng thái "đang mượn" | 1. Vào mục "Mượn/Trả" 2. Ấn nút "trả sách" của phiếu mượn đang ở trạng thái "đang mượn" | Thành viên có phiếu mượn ban đầu sách quá hạn BOOK003 | Hệ thống hiển thị **cảnh báo quá hạn** | REQ-05 | EP |
| 03 | Kiểm tra trạng thái sách đã trả | Sách đang ở trạng thái "đã trả" | 1. Vào mục "Mượn/Trả" 2. Tìm phiếu mượn đang ở trạng thái "đã trả" 3. Quay lại mục "Sách" và kiểm tra trạng thái sách đã trả | Thành viên có phiếu mượn ban đầu sách đã trả BOOK005 | Sách đang ở trạng thái "có sẵn" | REQ-05 | EP |
|---|---|---|---|---|---|---|---|
| 04 | Kiểm tra thành viên bị tạm ngưng | Thành viên bị tạm ngưng, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản bị tạm ngưng 2. Mượn bất kỳ một sách có sẵn | Tài khoản tạm ngưng (MEM004) | Thành viên không được mượn sách và hiển thị đúng lí do từ chối | REQ-04 | EP |
| 05 | Kiểm tra thành viên bị hết hạn | Thành viên bị hết hạn, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản bị hết hạn 2. Mượn bất kỳ một sách có sẵn | Tài khoản hết hạn (MEM005) | Thành viên không được mượn sách và hiển thị đúng lí do từ chối | REQ-04 | EP |
| 06 | Kiểm tra thành viên đang hoạt động | Thành viên hoạt động, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt đọng 2. Mượn bất kỳ một sách có sẵn | Tài khoản hoạt động (MEM006) | Thành viên được mượn sách và hiển thị mượn sách thành công | REQ-04 | EP |
| 07 | Mượn sách đã được mượn | Thành viên hoạt động, sách ở trạng thái "Đang mượn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Tìm sách ở trạng thái "đang mượn" và cố thử mượn | Tài khoản hoạt động (MEM006) |Thành viên không được mượn sách | REQ-04 | EP |
| 08 | Mượn sách quá giới hạn | Thành viên hoạt dộng, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Mượn 1,2,3,4 sách ở trạng thái "Có sẵn" | Tài khoản hoạt động (MEM006) | Thành viên bị từ chối mượn thêm sách nếu quá giới hạn và báo lí do từ chối | REQ-04 | EP, BVA | 
| 09 | Mượn sách thành công | Thành viên hoạt động, sách ở trạng thái "Có sẵn", mượn số sách dưới giới hạn | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Mượn 1/2/3 sách ở trạng thái "Có sẵn" | Tài khoản hoạt động (MEM006) | Thành viên mượn sách thành công và thời hạn là 14 ngày kể từ ngày mượn | REQ-04 | EP, Decision Table |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
