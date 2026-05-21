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

### IDM — Thêm thành viên (REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| **Họ và tên** | 1. Có nhập chữ (Valid) | Nguyễn Văn A | Thêm thành công |
| | 2. Để trống (Invalid) | *(Để trống)* | Báo lỗi thiếu Họ tên |
| **Email** | 1. Đúng cú pháp (Valid) | `legit@gmail.com` | Thêm thành công |
| | 2. Thiếu ký tự `@` (Invalid) | `haivuemail.com` | Báo lỗi sai định dạng |
| | 3. Thiếu dấu `.` ở domain (Invalid) | `trandat@emailcom` | Báo lỗi sai định dạng |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

### IDM — Borrow Record Lookup (REQ-08)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role accessing records? | Librarian | `librarian@library.com` | Sees ALL borrow records (BR001–BR005) across all members |
| | Member | `ba.nguyen@email.com` | Sees ONLY own borrow records |
| Member ID entered in lookup field? | Own ID | `MEM002` (logged-in user's own ID) | Records of MEM002 are displayed |
| | Another member's ID | `MEM006` (belongs to biet.hoang) | No records shown — access denied |
| | Non-existent ID | `MEM999` | No records found (empty result or error message) |
| Record information completeness? | All required fields present | BR001 | Record ID, book title, borrow date, due date, status all visible |
| Status value displayed? | Active borrow | BR001, BR003 | Status = "Đang mượn" |
| | Returned on time | BR002, BR004 | Status = "Đã trả" |
| | Returned late | BR005 | Status = "Đã trả" |
| | Overdue (after Librarian check) | BR001 (post Check Overdue) | Status = "Quá hạn" |

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
| TC-12 | Kiểm tra phép mượn của thành viên bị tạm ngưng | Thành viên bị tạm ngưng, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản bị tạm ngưng 2. Mượn bất kỳ một sách có sẵn | Tài khoản tạm ngưng (MEM004) | Thành viên không được mượn sách và hiển thị đúng lí do từ chối | REQ-04 | EP |
| TC-13 | Kiểm tra phép mượn của thành viên bị hết hạn | Thành viên bị hết hạn, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản bị hết hạn 2. Mượn bất kỳ một sách có sẵn | Tài khoản hết hạn (MEM005) | Thành viên không được mượn sách và hiển thị đúng lí do từ chối | REQ-04 | EP |
| TC-14 | Kiểm tra phép mượn của thành viên đang hoạt động | Thành viên hoạt động, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Mượn bất kỳ một sách có sẵn | Tài khoản hoạt động (MEM006) | Thành viên được mượn sách và hiển thị mượn sách thành công | REQ-04 | EP |
| TC-15 | Mượn sách đã được mượn | Thành viên hoạt động, sách ở trạng thái "Đang mượn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Tìm sách ở trạng thái "Đang mượn" và cố thử mượn | Tài khoản hoạt động (MEM006) | Thành viên không được mượn sách | REQ-04 | EP |
| TC-16 | Mượn sách quá giới hạn | Thành viên hoạt động, sách ở trạng thái "Có sẵn" | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Mượn 1,2,3,4 sách ở trạng thái "Có sẵn" | Tài khoản hoạt động (MEM006) | Thành viên không mượn được thêm sách khi quá giới hạn và hiển thị đúng lí do từ chối | REQ-04 | EP, BVA | 
| TC-17 | Mượn sách thành công | Thành viên hoạt động, sách ở trạng thái "Có sẵn", mượn số sách dưới giới hạn | 1. Đăng nhập vào hệ thống với tài khoản đang hoạt động 2. Mượn 1/2/3 sách ở trạng thái "Có sẵn" | Tài khoản hoạt động (MEM006) | Thành viên mượn sách thành công và thời hạn là 14 ngày kể từ ngày mượn | REQ-04 | EP, Decision Table |
| TC-18 | Trả sách đang mượn | Sách đang ở trạng thái "Đang mượn" | 1. Vào mục "Mượn/Trả" 2. Ấn nút "Trả sách" của phiếu mượn đang ở trạng thái "Đang mượn" 3. Quay lại mục "Sách" và kiểm tra trạng thái sách vừa trả | Thành viên có phiếu mượn ban đầu sách BOOK013 | Sách trở về trạng thái "Có sẵn" | REQ-05 | EP |
| TC-19 | Hiển thị **cảnh báo quá hạn** | Sách quá hạn đang ở trạng thái "Đang mượn" | 1. Vào mục "Mượn/Trả" 2. Ấn nút "Trả sách" của phiếu mượn đang ở trạng thái "Đang mượn" và quá hạn | Thành viên có phiếu mượn ban đầu sách quá hạn BOOK003 | Hệ thống hiển thị **cảnh báo quá hạn** | REQ-05 | EP |
| TC-20 | Kiểm tra trạng thái sách đã trả | Sách đang ở trạng thái "Đã trả" | 1. Vào mục "Mượn/Trả" 2. Tìm phiếu mượn đang ở trạng thái "Đã trả" 3. Quay lại mục "Sách" và kiểm tra trạng thái sách đã trả | Thành viên có phiếu mượn ban đầu sách đã trả BOOK005 | Sách đang ở trạng thái "Có sẵn" | REQ-05 | EP |
| TC-21 | Kiểm tra Thủ thư nhấn "Kiểm tra quá hạn" → phiếu đang mượn quá hạn được đánh dấu đúng | Đăng nhập tài khoản Thủ thư (`librarian@library.com` / `admin123`). Dữ liệu ở trạng thái ban đầu. | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu BR001 (dueDate: 15/09/2024) và BR003 (dueDate: 15/10/2024) | BR001 (MEM002 + BOOK003, hạn 15/09/2024); BR003 (MEM006 + BOOK013, hạn 15/10/2024) | BR001 và BR003 chuyển trạng thái từ "Đang mượn" sang "Quá hạn" (cả hai đều có dueDate ≤ 18/05/2026) | REQ-06 | EP |
| TC-22 | Kiểm tra phiếu đã trả KHÔNG bị đánh dấu "Quá hạn" sau khi nhấn "Kiểm tra quá hạn" | Đăng nhập Thủ thư. Dữ liệu ở trạng thái ban đầu. | **Bước 1:** Vào tab "Mượn / Trả".<br> **Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br> **Bước 3:** Quan sát trạng thái của BR002 (Đã trả đúng hạn) và BR005 (Đã trả nhưng trễ 5 ngày) | BR002 (Trần Dựa Dẫm + BOOK001, trả 20/08/2024); BR004 (Nguyễn Học Bá + BOOK005, trả 10/07/2024); BR005 (Trần Dựa Dẫm + BOOK006, trả 20/06/2024 — trễ hạn) | BR002, BR004, BR005 giữ nguyên "Đã trả" (không đổi thành "Quá hạn" dù ngày trả sau dueDate) | REQ-06 | EP|
| TC-23 | Kiểm tra Thành viên không thấy nút "Kiểm tra quá hạn" (kiểm soát quyền) | Đăng nhập tài khoản Thành viên (`ba.nguyen@email.com` / `password123`). | **Bước 1:** Đăng nhập tài khoản Thành viên.<br> **Bước 2:** Vào tab "Mượn / Trả".<br> **Bước 3:** Quan sát giao diện, tìm kiếm nút "Kiểm tra quá hạn" | Tài khoản: `ba.nguyen@email.com` / `password123` (vai trò: Thành viên) | Nút **"Kiểm tra quá hạn" không xuất hiện** trong giao diện của Thành viên | REQ-06 | EP  |
| TC-24 | Kiểm tra Thành viên chỉ thấy phiếu quá hạn của chính mình, không thấy của người khác | Bước chuẩn bị: Đăng nhập Thủ thư → nhấn "Kiểm tra quá hạn" → đăng xuất. Sau đó đăng nhập MEM002. | **Bước 1:** Đăng nhập Thủ thư, nhấn "Kiểm tra quá hạn", đăng xuất.<br> **Bước 2:** Đăng nhập `ba.nguyen@email.com` / `password123`.<br> **Bước 3:** Vào tab "Mượn / Trả".<br> **Bước 4:** Quan sát toàn bộ danh sách phiếu quá hạn hiển thị | MEM002 (ba.nguyen): có BR001 (quá hạn). MEM006 (biet.hoang): có BR003 (quá hạn) | MEM002 **chỉ thấy BR001** của mình. **Không thấy BR003** của MEM006 | REQ-06 | EP  |
| TC-25 | Kiểm tra ranh giới hạn trả: Phiếu có `dueDate` bằng đúng ngày hiện tại bị đánh dấu "Quá hạn" | Đăng nhập tài khoản Thành viên, tạo 1 phiếu mượn và giả lập dueDate = ngày hôm nay. Sau đó đăng xuất và đăng nhập tài khoản Thủ thư (`librarian@library.com` / `admin123`). | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu mượn có hạn trả là ngày hôm nay. | Phiếu mượn đang ở trạng thái "Đang mượn" với dueDate trùng khớp chính xác với ngày hiện tại | Phiếu mượn chuyển trạng thái từ "Đang mượn" sang "Quá hạn" | REQ-06 | BVA |
| TC-26 | Kiểm tra phiếu chưa tới hạn (dueDate > ngày hiện tại) KHÔNG bị đánh dấu "Quá hạn" | Đăng nhập tài khoản Thành viên, mượn 1 cuốn sách mới (hạn trả mặc định sẽ là ngày hiện tại + 14 ngày). Sau đó đăng xuất và đăng nhập tài khoản Thủ thư. | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Nhấn nút "Kiểm tra quá hạn".<br>**Bước 3:** Quan sát trạng thái của phiếu mượn mới tạo. | Phiếu mượn mới có dueDate > ngày hiện tại | Phiếu mượn giữ nguyên trạng thái "Đang mượn" (không bị đổi thành "Quá hạn") | REQ-06 | EP |
| TC-27 | Kiểm tra trạng thái mặc định của các phiếu quá hạn TRƯỚC khi nhấn nút "Kiểm tra quá hạn" | Đăng nhập tài khoản Thủ thư. Dữ liệu ở trạng thái ban đầu (đảm bảo CHƯA nhấn nút "Kiểm tra quá hạn"). | **Bước 1:** Vào tab "Mượn / Trả".<br>**Bước 2:** Trực tiếp quan sát trạng thái của các phiếu BR001 và BR003 ngay khi vừa vào trang. | BR001 (MEM002 + BOOK003, hạn 15/09/2024); BR003 (MEM006 + BOOK013, hạn 15/10/2024) | BR001 và BR003 vẫn hiển thị trạng thái mặc định là "Đang mượn" (chứng minh hệ thống không tự động thay đổi nếu thiếu thao tác của Thủ thư) | REQ-06 | EP |
| TC-28| Kiểm tra quyền thêm thành viên của tài khoản không phải thủ thư | Đã đăng nhập tài khoản thành viên | Kiểm tra sự xuất hiện của icon "Thêm thành viên" trên góc phải | Login: ba.nguyen@email.com, Password: password123 | Icon "Thêm thành viên" không xuất hiện | REQ-07 | Decision Table (Phân quyền) |
| TC-29 | Kiểm tra khi thiếu mục "Họ và tên" thì hệ thống có báo lỗi không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập email và SĐT hợp lệ, bỏ trống Họ và tên. Nhấn nút "Thêm". | Email: noname@email.com, SĐT: 0123456791 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi thiếu Họ và tên. | REQ-07 | Decision Table (thiếu tên)|
| TC-30 | Kiểm tra hệ thống có chặn email thiếu @ không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập Họ tên và SĐT hợp lệ. Nhập email có dấu "." nhưng thiếu "@". Nhấn nút "Thêm". | Họ tên: Vũ Hải, Email: haivuemail.com, SĐT: 0133456798 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi định dạng email không hợp lệ. | REQ-07 | EP / BVA |
| TC-31 | Kiểm tra hệ thống có chặn email thiếu dấu . ở domain hay không | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập Họ tên và SĐT hợp lệ. Nhập email có "@" nhưng thiếu dấu "." ở sau đó. Nhấn nút "Thêm". | Họ tên: Trần Đạt, Email: trandat@emailcom, SĐT: 0123456798 |Hệ thống từ chối tạo tài khoản và hiển thị thông báo lỗi định dạng email không hợp lệ. | REQ-07 | EP / BVA |
| TC-32 | Kiểm tra hoạt động bình thường của tính năng | Đã đăng nhập tài khoản Thủ thư, đang ở form Thêm thành viên. |Nhập Họ tên, Email và SĐT. Nhấn nút "Thêm". | Họ tên: Lê Gít, Email: legit@email.com, SĐT: 0234567891 |Hệ thống thêm thành viên thành công. | REQ-07 | EP |
| TC-33 | Verify Librarian can view all borrow records across all members | Logged in as Librarian (`librarian@library.com` / `admin123`). Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Observe the full borrow record list.<br>**Step 3:** Verify BR001 (MEM002), BR002 (MEM003), BR003 (MEM006), BR004 (MEM002), BR005 (MEM003) are all listed. | All 5 seed records: BR001–BR005 | All 5 records are visible to the Librarian with correct member names, book titles, dates, and statuses | REQ-08 | EP |
| TC-34 | Verify Member MEM002 sees only their own records in the default "my records" view | Logged in as MEM002 (`ba.nguyen@email.com` / `password123`). Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Observe the borrow record list shown by default (without entering any search ID).<br>**Step 3:** Check which records are displayed. | MEM002 owns: BR001 (BOOK003 — "Đang mượn"), BR004 (BOOK005 — "Đã trả") | Only **BR001** and **BR004** are displayed. BR002, BR003, BR005 (belonging to other members) are **not visible**. | REQ-08 | EP |
| TC-35 | Verify Member cannot view another member's records using the "lookup by member ID" feature | Logged in as MEM002 (`ba.nguyen@email.com` / `password123`). Initial seed data. | **Step 1** Go to "Mượn / Trả" tab.<br>**Step 2:** Locate the "Tra cứu phiếu mượn" (lookup) search field.<br>**Step 3:** Enter `MEM006` (belonging to biet.hoang).<br>**Step 4:** Observe the result. | Lookup input: `MEM006` (another member's ID) | System shows **no records** or displays an access-denied message. BR003 (MEM006's record) is **not shown** to MEM002. | REQ-08 | EP |
| TC-36 | Verify all required information fields are present in each borrow record | Logged in as Librarian. Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Inspect any borrow record (e.g. BR001).<br>**Step 3:** Check that all 5 fields are visible: Record ID, Book title, Borrow date, Due date, Status. | BR001: MEM002, BOOK003, borrowed 01/09/2024, due 15/09/2024, status "Đang mượn" | Record displays all 5 required fields: **Record ID** (BR001), **Book** (Kiểm thử phần mềm nhập môn), **Borrow date** (01/09/2024), **Due date** (15/09/2024), **Status** ("Đang mượn") | REQ-08 | EP  |

---


---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
