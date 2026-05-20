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
| TC-01 | Kiểm tra người dùng đăng nhập thành công với email và mật khẩu hợp lệ | Người dùng đã có tài khoản trong hệ thống và đang ở trang đăng nhập | 1. Nhập email hợp lệ vào ô "Email". 2. Nhập mật khẩu đúng vào ô "Mật khẩu". 3. Nhấn nút "Đăng nhập" | Tên đăng nhập: `ba.nguyen@email.com`, mật khẩu: `password123` | Hệ thống đăng nhập thành công và chuyển sang trang chủ. Hiển thị tên người dùng và vai trò | REQ-01 | Black-box Testing |
| TC-02 | Kiểm tra hệ thống hiển thị lỗi khi email không tồn tại | Người dùng đang ở trang đăng nhập | 1. Nhập email không tồn tại vào ô "Email". 2. Nhập mật khẩu bất kì. 3. Bấm nút "Đăng nhập" | Tên đăng nhập: `random@email.com`, mật khẩu: `123`| Hệ thống hiển thị "Không tìm thấy thành viên | REQ-01 | Black-box Testing, EP |
| TC-03 | Kiểm tra hệ thống hiển thị lỗi khi nhập sai mật khẩu | Người dùng đã có tài khoản trong hệ thống và đang ở trang đăng nhập | 1. Nhập email hợp lệ vào ô "Email". 2. Nhập mật khẩu sai vào ô "Mật khẩu". 3. Nhấn nút "Đăng nhập" | Tên đăng nhập: `ba.nguyen@email.com`, mật khẩu: `hello` (mật khẩu không chính xác) | Hệ thống hiển thị "Mật khẩu không đúng" | REQ-01 | Black-box Testing, EP |
| TC-04 | Kiểm tra hệ thống từ chối đăng nhập khi email không đúng định dạng | Người dùng đang ở trang đăng nhập, đã có tài khoản trong hệ thống (nhưng email không đúng định dạng) | 1. Nhập một email không đúng định dạng (nhưng có tồn tại trong hệ thống) vào ô "Email" (ví dụ: `example@email`. 2. Nhập đúng mật khẩu vào ô "Mật khẩu". 3. Nhấn nút "Đăng nhập" | Tên đăng nhập: `example@email`, mật khẩu: `password123` | Hệ thống từ chối đăng nhập và báo lỗi "Email không đúng định dạng" | REQ-01 | Black-box Testing, Input Validation |
|TC-05|Tính năng mượn sách|Đăng nhập vào thành viên đang hoạt động|Nhấn vào dấu cộng của những quyển sách đang có sẵn|Nhấn vào dấu cộng của từng quyển sách|Chuyển sang trạng thái đang mượn|REQ-02|EP|
|TC-06|Tính năng trả sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|Nhấn vào nút trả sách đang mượn đối với thành viên, nhấn nút trả sách khi quá hạn đối với thủ thư|Nhấn trả sách|Hiện "Đã trả"|REQ-02|State Transition|
|TC-07|Hiển thị thông tin mượn sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|1. Đăng nhập vào tài khoản thành viên đang hoạt động <br> 2. Mượn sách <br> 3. Đăng nhập vào tài khoản thủ thư <br> 4. Kiểm tra sách được mượn|Thành viên mượn sách|Thủ thư thấy sách được mượn|REQ-02|Decision Table|
|TC-08| Kiểm tra tính năng '"Tìm kiếm theo Tên sách, Tên tác giả"' và xử lý khi không có dữ liệu khớp.| Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào thanh tìm kiếm. <br>2. Nhập vào Tên tác giả và xác nhận bộ lọc. <br>3. Xóa thanh tìm kiếm, nhập vào Tên sách cụ thể. <br>4. Xóa thanh tìm kiếm, nhập vào một chuỗi ký tự không tồn tại.| `"Nguyễn Minh Đức"`, `"Lập trình Flutter cơ bản"` và `"ABCxyz123"`| Sau bước 2, sẽ hiển thị cuốn sách với mã `BOOK001` (Lập trình Flutter cơ bản) và `BOOK009` (Nhập môn lập trình Python). <br>Sau bước 3, Hiển thị duy nhất 1 cuốn sách mã `BOOK001` (Lập trình Flutter cơ bản). <br>Sau bước 4 sẽ hiển thị kết quả chuỗi chính xác `"Không tìm thấy sách nào."`|REQ-03 |EP Testing|
|TC-09| Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) khi tìm kiếm sách.| Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào thanh tìm kiếm. <br>2. Nhập chuỗi dữ liệu đầu vào 1. <br>3. Kiểm tra danh sách hiển thị. <br>4. Xóa toàn bộ ký tự trong thanh tìm kiếm. <br>5. Nhập chuỗi dữ liệu đầu vào 2. <br>6. Kiểm tra danh sách hiển thị.|1. `"nGuyễn mInh ĐứC"` và 2. `"lẬp trìnH flUTTer cơ bẢn"`|Sau bước 3, hệ thống lọc và hiển thị chính xác 2 cuốn sách của tác giả: mã `'BOOK001'` (Lập trình Flutter cơ bản) và `'BOOK009'` (Nhập môn lập trình Python), các sách khác sẽ bị ẩn. <br>Sau bước 6, hệ thống lọc và hiển thị duy nhất 1 cuốn sách: mã `'BOOK001'` (Lập trình Flutter cơ bản).|REQ-03 |EP Testing|
|TC-10|Kiểm tra tính năng lọc danh sách theo thể loại với trường hợp hợp lệ và không hợp lệ.|Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`|Bước 1. Nhấp chuột vào thanh `"Lọc theo thể loại"`. <br>2. Nhập chính xác tên một thể loại hợp lệ. <br>3. Kiểm tra danh sách hiển thị. <br>4. Xóa bộ lọc thanh thể loại. <br>5. Nhập vào một thể loại không tồn tại trong hệ thống.|`"Công nghệ"` và `"Khoa học ảo tưởng"`|Sau bước 3, Chỉ hiển thị 8 cuốn sách thuộc nhóm "Công nghệ" (Mã sách từ `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`). Bất kỳ sách nào thuộc thể loại khác (như `'Kinh tế'`, `'Văn học'`,...) đều bị ẩn khỏi màn hình. <br>Sau bước 5, Toàn bộ danh sách biến mất, hiển thị chuỗi chuỗi chính xác `"Không tìm thấy sách nào"`.|REQ-03|EP Testing|
|TC-11| Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) của tính năng lọc theo thể loại.|Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào ô nhập `"Lọc theo thể loại"`. <br>2. Nhập tên thể loại viết hoàn toàn bằng chữ thường. <br>3. Nhấp chuột ra ngoài hoặc nhấn Enter để kích hoạt bộ lọc. <br>4. Kiểm tra sự thay đổi của danh sách sách hiển thị trên màn hình.|`"công nghệ"`|Hệ thống nhận diện bộ lọc không phân biệt hoa thường, giữ nguyên hiển thị chính xác 8 cuốn sách thuộc nhóm thể loại `"Công nghệ"` giống như khi nhập chữ hoa chuẩn (Mã sách từ `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`).|REQ-03| EP Testing|

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
