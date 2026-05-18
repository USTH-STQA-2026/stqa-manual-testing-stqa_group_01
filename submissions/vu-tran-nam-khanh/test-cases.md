# Test Cases — Bảng trường hợp kiểm thử

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày tạo** | `16/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.

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

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| TC-01 | Kiểm tra tính năng '"Tìm kiếm theo Tên sách, Tên tác giả"' và xử lý khi không có dữ liệu khớp.| Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào thanh tìm kiếm. <br>2. Nhập vào Tên tác giả và xác nhận bộ lọc. <br>3. Xóa thanh tìm kiếm, nhập vào Tên sách cụ thể. <br>4. Xóa thanh tìm kiếm, nhập vào một chuỗi ký tự không tồn tại.| `"Nguyễn Minh Đức"`, `"Lập trình Flutter cơ bản"` và `"ABCxyz123"`| Sau bước 2, sẽ hiển thị cuốn sách với mã `BOOK001` (Lập trình Flutter cơ bản) và `BOOK009` (Nhập môn lập trình Python). <br>Sau bước 3, Hiển thị duy nhất 1 cuốn sách mã `BOOK001` (Lập trình Flutter cơ bản). <br>Sau bước 4 sẽ hiển thị kết quả chuỗi chính xác `"Không tìm thấy sách nào."`|REQ-03 |EP và Black-box Testing|
| TC-02 | Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) khi tìm kiếm sách.| Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào thanh tìm kiếm. <br>2. Nhập chuỗi dữ liệu đầu vào 1. <br>3. Kiểm tra danh sách hiển thị. <br>4. Xóa toàn bộ ký tự trong thanh tìm kiếm. <br>5. Nhập chuỗi dữ liệu đầu vào 2. <br>6. Kiểm tra danh sách hiển thị.|1. `"nGuyễn mInh ĐứC"` và 2. `"lẬp trìnH flUTTer cơ bẢn"`|Sau bước 3, hệ thống lọc và hiển thị chính xác 2 cuốn sách của tác giả: mã `'BOOK001'` (Lập trình Flutter cơ bản) và `'BOOK009'` (Nhập môn lập trình Python), các sách khác sẽ bị ẩn. <br>Sau bước 6, hệ thống lọc và hiển thị duy nhất 1 cuốn sách: mã `'BOOK001'` (Lập trình Flutter cơ bản).|REQ-03 |EP và Black-box Testing|
|TC-03|Kiểm tra tính năng lọc danh sách theo thể loại với trường hợp hợp lệ và không hợp lệ.|Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`|Bước 1. Nhấp chuột vào thanh `"Lọc theo thể loại"`. <br>2. Nhập chính xác tên một thể loại hợp lệ. <br>3. Kiểm tra danh sách hiển thị. <br>4. Xóa bộ lọc thanh thể loại. <br>5. Nhập vào một thể loại không tồn tại trong hệ thống.|`"Công nghệ"` và `"Khoa học ảo tưởng"`|Sau bước 3, Chỉ hiển thị 8 cuốn sách thuộc nhóm "Công nghệ" (Mã sách từ `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`). Bất kỳ sách nào thuộc thể loại khác (như `'Kinh tế'`, `'Văn học'`,...) đều bị ẩn khỏi màn hình. <br>Sau bước 5, Toàn bộ danh sách biến mất, hiển thị chuỗi chuỗi chính xác `"Không tìm thấy sách nào"`.|REQ-03|EP và Black-box Testing|
|TC-04| Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) của tính năng lọc theo thể loại.|Đăng nhập thành công vào hệ thống và đang ở trong mục `'Sách'`| Bước 1. Nhấp chuột vào ô nhập `"Lọc theo thể loại"`. <br>2. Nhập tên thể loại viết hoàn toàn bằng chữ thường. <br>3. Nhấp chuột ra ngoài hoặc nhấn Enter để kích hoạt bộ lọc. <br>4. Kiểm tra sự thay đổi của danh sách sách hiển thị trên màn hình.|`"công nghệ"`|Hệ thống nhận diện bộ lọc không phân biệt hoa thường, giữ nguyên hiển thị chính xác 8 cuốn sách thuộc nhóm thể loại `"Công nghệ"` giống như khi nhập chữ hoa chuẩn (Mã sách từ `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`).|REQ-03| EP và Black-box Testing|

---

## Bước 3: Giải thích các TCs (explanation)

# TC-01 :

**- Kỹ thuật sử dụng :**
1. Black-box Testing: Kiểm tra phản hồi đầu ra hiển thị trên màn hình (danh sách thẻ sách hoặc chuỗi thông báo lỗi) tương ứng với dữ liệu chuỗi văn bản đầu vào.
2. EP (Phân lớp tương đương): Tập hợp dữ liệu tìm kiếm được chia làm 2 phân vùng lớn: Lớp dữ liệu tồn tại trong DB (gồm phân nhóm Tên sách và phân nhóm Tên tác giả) và Lớp dữ liệu hoàn toàn không tồn tại trong DB. Chuỗi "ABCxyz123" là đại diện cho phân vùng không tồn tại nhằm kiểm tra luồng xử lý ngoại lệ.


# TC-02 :


**- Kỹ thuật sử dụng :**

1. Black-box Testing: Thao tác hoàn toàn trên giao diện người dùng bằng cách giả lập hành vi nhập văn bản vào hộp tìm kiếm, hoàn toàn không can thiệp hay đọc mã nguồn xử lý chuỗi của framework Flutter Web.
2. EP (Phân lớp tương đương): Miền dữ liệu đầu vào của thanh tìm kiếm được chia làm các lớp định dạng ký tự: Chữ thường, Chữ HOA, và Chữ hỗn hợp (xen kẽ HOA/thường). TC-02 chọn lớp chữ hỗn hợp để làm giá trị đại diện kiểm thử khả năng chuẩn hóa chuỗi của hệ thống.


# TC-03 :

**- Kỹ thuật áp dụng :**

1. Black-box Testing: Thao tác kiểm thử thuần túy dựa trên các thành phần UI hiển thị đầu vào và đầu ra của hệ thống, hoàn toàn không can thiệp vào mã nguồn lưu trữ mảng dữ liệu (in-memory) của ứng dụng.
2. EP (Phân lớp tương đương): Miền dữ liệu nhập vào thanh lọc được chia thành 2 phân vùng tương đương: Nhóm các chuỗi ký tự thuộc 6 thể loại quy định trên màn hình (đại diện bởi "Công nghệ") và Nhóm các chuỗi văn bản nằm ngoài danh mục hệ thống hỗ trợ (đại diện bởi "Khoa học giả tưởng").

# TC-04 : 

**- Kỹ thuật áp dụng**

1. Black-box Testing: Tester chỉ đứng từ góc độ người dùng cuối để nhập dữ liệu thô từ bàn phím và đối chiếu sự thay đổi trực quan của các thẻ thành phần trên màn hình giao diện.
2. EP (Phân lớp tương đương): Phân chia miền định dạng văn bản đầu vào của thanh lọc thể loại thành các khối định dạng ký tự khác nhau. TC-04 sử dụng một giá trị đại diện cho khối "Chữ viết thường hoàn toàn" nhằm kiểm tra toàn vẹn chức năng tự động chuyển đổi định dạng chuỗi của ứng dụng.
