# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày tạo** | `18/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.


### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng? | Thủ thư | `librarian@library.com` | Thấy nút "Kiểm tra quá hạn", có thể nhấn |
| | Thành viên | `ba.nguyen@email.com` | Không thấy nút "Kiểm tra quá hạn" |
| Trạng thái phiếu mượn? | Đang mượn, dueDate ≤ hôm nay | BR001 (hạn 15/09/2024) | Bị đánh dấu "Quá hạn" sau khi nhấn nút |
| | Đang mượn, dueDate > hôm nay | Phiếu mới tạo hôm nay | Giữ nguyên "Đang mượn" |
| | Đã trả, dueDate ≤ hôm nay | BR002, BR005 | Giữ nguyên "Đã trả", không đổi thành "Quá hạn" |
| Phạm vi hiển thị cho Thành viên? | Phiếu của chính mình | BR001 (của MEM002) | Thấy phiếu quá hạn của mình |
| | Phiếu của người khác | BR003 (của MEM006) | Không thấy phiếu của người khác |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| An01 | Kiểm tra Thủ thư nhấn "Kiểm tra quá hạn" → phiếu đang mượn quá hạn được đánh dấu đúng | Đăng nhập tài khoản Thủ thư (`librarian@library.com` / `admin123`). Dữ liệu ở trạng thái ban đầu. | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu BR001 (dueDate: 15/09/2024) và BR003 (dueDate: 15/10/2024) | BR001 (MEM002 + BOOK003, hạn 15/09/2024); BR003 (MEM006 + BOOK013, hạn 15/10/2024) | BR001 và BR003 chuyển trạng thái từ "Đang mượn" sang "Quá hạn" (cả hai đều có dueDate ≤ 18/05/2026) | REQ-06 | EP |
| An02 | Kiểm tra phiếu đã trả KHÔNG bị đánh dấu "Quá hạn" sau khi nhấn "Kiểm tra quá hạn" | Đăng nhập Thủ thư. Dữ liệu ở trạng thái ban đầu. | **Bước 1:** Vào tab "Mượn / Trả".<br> **Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br> **Bước 3:** Quan sát trạng thái của BR002 (Đã trả đúng hạn) và BR005 (Đã trả nhưng trễ 5 ngày) | BR002 (Trần Dựa Dẫm + BOOK001, trả 20/08/2024); BR004 (Nguyễn Học Bá + BOOK005, trả 10/07/2024); BR005 (Trần Dựa Dẫm + BOOK006, trả 20/06/2024 — trễ hạn) | BR002, BR004, BR005 giữ nguyên "Đã trả" (không đổi thành "Quá hạn" dù ngày trả sau dueDate) | REQ-06 | EP|
| An03 | Kiểm tra Thành viên không thấy nút "Kiểm tra quá hạn" (kiểm soát quyền) | Đăng nhập tài khoản Thành viên (`ba.nguyen@email.com` / `password123`). | **Bước 1:** Đăng nhập tài khoản Thành viên.<br> **Bước 2:** Vào tab "Mượn / Trả".<br> **Bước 3:** Quan sát giao diện, tìm kiếm nút "Kiểm tra quá hạn" | Tài khoản: `ba.nguyen@email.com` / `password123` (vai trò: Thành viên) | Nút **"Kiểm tra quá hạn" không xuất hiện** trong giao diện của Thành viên | REQ-06 | EP  |
| An04 | Kiểm tra Thành viên chỉ thấy phiếu quá hạn của chính mình, không thấy của người khác | Bước chuẩn bị: Đăng nhập Thủ thư → nhấn "Kiểm tra quá hạn" → đăng xuất. Sau đó đăng nhập MEM002. | **Bước 1:** Đăng nhập Thủ thư, nhấn "Kiểm tra quá hạn", đăng xuất.<br> **Bước 2:** Đăng nhập `ba.nguyen@email.com` / `password123`.<br> **Bước 3:** Vào tab "Mượn / Trả".<br> **Bước 4:** Quan sát toàn bộ danh sách phiếu quá hạn hiển thị | MEM002 (ba.nguyen): có BR001 (quá hạn). MEM006 (biet.hoang): có BR003 (quá hạn) | MEM002 **chỉ thấy BR001** của mình. **Không thấy BR003** của MEM006 | REQ-06 | EP  |
| An05 | Kiểm tra ranh giới hạn trả: Phiếu có `dueDate` bằng đúng ngày hiện tại bị đánh dấu "Quá hạn" | Đăng nhập tài khoản Thành viên, tạo 1 phiếu mượn và giả lập dueDate = ngày hôm nay. Sau đó đăng xuất và đăng nhập tài khoản Thủ thư (`librarian@library.com` / `admin123`). | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu mượn có hạn trả là ngày hôm nay. | Phiếu mượn đang ở trạng thái "Đang mượn" với dueDate trùng khớp chính xác với ngày hiện tại | Phiếu mượn chuyển trạng thái từ "Đang mượn" sang "Quá hạn" | REQ-06 | BVA |
| An06 | Kiểm tra phiếu chưa tới hạn (dueDate > ngày hiện tại) KHÔNG bị đánh dấu "Quá hạn" | Đăng nhập tài khoản Thành viên, mượn 1 cuốn sách mới (hạn trả mặc định sẽ là ngày hiện tại + 14 ngày). Sau đó đăng xuất và đăng nhập tài khoản Thủ thư. | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu mượn mới tạo. | Phiếu mượn mới có dueDate > ngày hiện tại | Phiếu mượn giữ nguyên trạng thái "Đang mượn" (không bị đổi thành "Quá hạn") | REQ-06 | EP |
| An07 | Kiểm tra trạng thái mặc định của các phiếu quá hạn TRƯỚC khi nhấn nút "Kiểm tra quá hạn" | Đăng nhập tài khoản Thủ thư. Dữ liệu ở trạng thái ban đầu (đảm bảo CHƯA nhấn nút "Kiểm tra quá hạn"). | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Trực tiếp quan sát trạng thái của các phiếu BR001 và BR003 ngay khi vừa vào trang. | BR001 (MEM002 + BOOK003, hạn 15/09/2024); BR003 (MEM006 + BOOK013, hạn 15/10/2024) | BR001 và BR003 vẫn hiển thị trạng thái mặc định là "Đang mượn" (chứng minh hệ thống không tự động thay đổi nếu thiếu thao tác của Thủ thư) | REQ-06 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
