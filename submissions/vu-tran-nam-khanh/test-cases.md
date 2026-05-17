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
| TC-01 | Kiểm tra tính không phân biệt chữ HOA/thường (case-Insensitivity) khi tìm kiếm sách.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"| Bước 1. Ấn vào hộp tìm kiếm 2. Gõ "nGuyễn mInh ĐứC" 3. Kiểm tra kết quả tìm đuọc và xoá phần nhập 4. Gõ "lẬp trìnH flUTTer cơ bẢn" 5. Kiểm tra kết quả tìm đuọc| "nGuyễn mInh ĐứC" và "lẬp trìnH flUTTer cơ bẢn"| Sau bước 3, ệ thống lọc và hiển thị chính xác 2 cuốn sách của tác giả: mã BOOK001 (Lập trình Flutter cơ bản) và BOOK009 (Nhập môn lập trình Python). Các sách khác sẽ bị ẩn. Sau bước 6, hệ thống lọc và hiển thị duy nhất 1 cuốn sách: mã BOOK001 (Lập trình Flutter cơ bản).| REQ-03 | EP và Black-box Testing|
| TC-02 | Kiểm tra tính năng "tìm kiếm theo Tên sách, Tên tác giả" và xử lý khi không có dữ liệu khớp.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"| Bước 1. Nhấp chuột vào thanh tìm kiếm. 2. Nhập vào Tên tác giả và xác nhận bộ lọc. 3. Xóa thanh tìm kiếm, nhập vào Tên sách cụ thể. 4. Xóa thanh tìm kiếm, nhập vào một chuỗi ký tự không tồn tại.| "Nguyễn Minh Đức", "Lập trình Flutter cơ bản" và "ABCxyz123"| Sau bước 2, sẽ hiển thị cuốn sách với mã BOOK001 (Lập trình Flutter cơ bản) và BOOK009 (Nhập môn lập trình Python); Sau bước 3, Hiển thị duy nhất 1 cuốn sách mã BOOK001 (Lập trình Flutter cơ bản); Sau bước 4 sẽ hiển thị kết quả chuỗi chính xác "Không tìm thấy sách nào"| REQ-03| EP và Black-box Testing|
|TC-03|Kiểm tra tính năng lọc danh sách sách bằng một thể loại hợp lệ có sẵn trên hệ thống| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"|Bước 1. Nhấp chuột vào thanh "Lọc theo thể loại". 2. Nhập hoặc chọn giá trị dữ liệu đầu vào. 3. Kiểm tra sự thay đổi của danh sách sách hiển thị trên màn hình.|"Công nghệ"|Hệ thống sẽ chỉ hiển thị các cuốn sách có gắn thẻ "Công nghệ", bao gồm các mã: BOOK001, BOOK002, BOOK003, BOOK005, BOOK008, BOOK009, BOOK010, và BOOK011. Bất kỳ sách nào thuộc thể loại khác (như Kinh tế, Văn học...) đều bị ẩn khỏi màn hình.|REQ-03|EP và Black-box Testing|
|TC-04|Kiểm tra xử lý của hệ thống khi lọc bằng một thể loại không hợp lệ / không có trong danh sách hỗ trợ|Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang ở trong mục "Sách"| Bước 1. Nhấp chuột vào thanh "Lọc theo thể loại". 2. Nhập một chuỗi ký tự không nằm trong danh sách 6 thể loại có sẵn. 3. Nhấn xác nhận (Enter/Click ngoài) và kiểm tra màn hình hiển thị.|"Khoa học giả tưởng"|Toàn bộ các thẻ sách biến mất khỏi màn hình giao diện. Hệ thống hiển thị chính xác chuỗi thông báo "Không tìm thấy sách nào" ở khu vực danh sách.|REQ-03| EP và Black-box Testing|

---

## Bước 3: Giải thích các TCs (explanation)

# TC-01 :
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Sử dụng mã TC-01 giúp việc theo dõi kết quả thực thi và liên kết đến các bug report sau này trở nên chính xác, dễ dàng.
2. REQ cụ thể: Gắn trực tiếp với mã yêu cầu nghiệp vụ REQ-03 để kiểm soát độ phủ kiểm thử.
3. Mục tiêu kiểm thử rõ ràng: Nêu rõ mục đích cốt lõi là kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) của thanh tìm kiếm.
4. Tiền điều kiện cụ thể: Xác định rõ trạng thái bắt đầu (Thủ thư đăng nhập thành công và màn hình đang ở danh mục "Sách") nhằm đảm bảo môi trường kiểm thử luôn đồng nhất.
5. Dữ liệu đầu vào cụ thể: Không viết chung chung là "nhập văn bản bất kỳ", test case chỉ rõ hai chuỗi hoán đổi định dạng chữ phức tạp là "nGuyễn mInh ĐứC" và "lẬp trìnH flUTTer cơ bẢn".
6. Bước thực hiện chi tiết: Đánh số rõ ràng từ bước 1 đến bước 6; tách biệt rạch ròi các hành động nhập liệu, kiểm tra giao diện, và xóa dữ liệu cũ để tránh nhầm lẫn cho tester.
7. Kết quả mong đợi kiểm chứng được: Oracle được viết vô cùng mạnh mẽ bằng cách chỉ rõ mã sách phải hiển thị trên màn hình (BOOK001 và BOOK009) thay vì ghi chung chung là "Hệ thống tìm kiếm được".
Kỹ thuật được áp dụng

- Kỹ thuật sử dụng :

1. Black-box Testing: Thao tác hoàn toàn trên giao diện người dùng bằng cách giả lập hành vi nhập văn bản vào hộp tìm kiếm, hoàn toàn không can thiệp hay đọc mã nguồn xử lý chuỗi của framework Flutter Web.
2. EP (Phân lớp tương đương): Miền dữ liệu đầu vào của thanh tìm kiếm được chia làm các lớp định dạng ký tự: Chữ thường, Chữ HOA, và Chữ hỗn hợp (xen kẽ HOA/thường). TC-01 chọn lớp chữ hỗn hợp để làm giá trị đại diện kiểm thử khả năng chuẩn hóa chuỗi của hệ thống.

# TC-02 :
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Mã TC-02 được đánh số liên tục trong phân nhóm tính năng.
2. REQ cụ thể: Liên kết chặt chẽ đến tài liệu đặc tả REQ-03.
3. Mục tiêu kiểm thử rõ ràng: Mô tả chính xác việc xác thực khả năng lọc theo cả hai điều kiện (Tên sách/Tên tác giả) trên cùng một thanh tìm kiếm và kiểm tra kịch bản không có dữ liệu.
4. Tiền điều kiện cụ thể: Đảm bảo hệ thống ở màn hình danh sách mặc định để các phép tìm kiếm kế tiếp không bị ảnh hưởng bởi dữ liệu thừa.
5. Dữ liệu đầu vào cụ thể: Cung cấp 3 chuỗi dữ liệu rõ ràng: tên tác giả "Nguyễn Minh Đức", tên sách "Lập trình Flutter cơ bản", và chuỗi ký tự rác "ABCxyz123".
6. Bước thực hiện chi tiết: Các bước thao tác tuần tự hóa một chuỗi các hành động liên tiếp của người dùng thực tế một cách logic.
7. Kết quả mong đợi kiểm chứng được: Quy định rõ ràng sự thay đổi giao diện theo từng bước mốc dữ liệu. Đặc biệt, oracle bắt buộc hệ thống phải hiển thị chính xác chuỗi ký tự tiếng Anh 'No books found.' theo đúng yêu cầu nghiêm ngặt của SRS thay vì hiển thị tiếng Việt tự do.

- Kỹ thuật sử dụng :
1. Black-box Testing: Kiểm tra phản hồi đầu ra hiển thị trên màn hình (danh sách thẻ sách hoặc chuỗi thông báo lỗi) tương ứng với dữ liệu chuỗi văn bản đầu vào.
2. EP (Phân lớp tương đương): Tập hợp dữ liệu tìm kiếm được chia làm 2 phân vùng lớn: Lớp dữ liệu tồn tại trong DB (gồm phân nhóm Tên sách và phân nhóm Tên tác giả) và Lớp dữ liệu hoàn toàn không tồn tại trong DB. Chuỗi "ABCxyz123" là đại diện cho phân vùng không tồn tại nhằm kiểm tra luồng xử lý ngoại lệ.

# TC-03 :
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Định danh TC-03 kế thừa mạch lạc cấu trúc bảng.
2. REQ cụ thể: Ánh xạ chính xác tới tính năng phân loại sách trong REQ-03.
3. Mục tiêu kiểm thử rõ ràng: Xác định rõ hành động kiểm thử luồng chạy thành công (Happy Path) của chức năng chọn lọc phân loại sách.
4. Tiền điều kiện cụ thể: Yêu cầu danh sách sách ở trạng thái mặc định, giúp tester nhận biết rõ ràng sự thu hẹp của danh sách sau khi áp dụng bộ lọc.
5. Dữ liệu đầu vào cụ thể: Sử dụng chính xác chuỗi "Công nghệ", đây là một trong 6 từ khóa thể loại được hệ thống in trực tiếp trên giao diện.
6. Bước thực hiện chi tiết: Gồm 3 bước ngắn gọn, tập trung thẳng vào hành động kích hoạt thanh lọc thể loại và đối chiếu.
7. Kết quả mong đợi kiểm chứng được: Liệt kê đầy đủ và tường tận tất cả các mã sách thuộc nhóm Công nghệ có trong cơ sở dữ liệu seed (BOOK001 đến BOOK011), yêu cầu ẩn toàn bộ các sách thuộc nhóm khác.

- Kỹ thuật sử dụng :
1. Black-box Testing: Thực hiện tương tác trực tiếp với thành phần UI "Lọc theo thể loại" và quan sát phản xạ đóng/mở ẩn hiện của các thẻ thành phần trên màn hình.
2. EP (Phân lớp tương đương): Đầu vào cho tính năng lọc thể loại được chia thành 2 khối tương đương: Lớp dữ liệu các thể loại hợp lệ được hệ thống hỗ trợ (6 thể loại hiển thị trên UI) và Lớp thể loại nằm ngoài danh sách. TC-03 sử dụng giá trị "Công nghệ" làm đại diện cho khối dữ liệu hợp lệ.

# TC-04 : 
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Đạt tiêu chuẩn định danh TC-04.
2. REQ cụ thể: Liên kết chặt chẽ đến REQ-03 để kiểm thử trường hợp ngoại lệ của bộ lọc.
3. Mục tiêu kiểm thử rõ ràng: Tập trung vào kịch bản kiểm thử tiêu cực (Negative Path) khi người dùng cố tình nhập một thể loại không tồn tại.
4. Tiền điều kiện cụ thể: Thiết lập trạng thái hệ thống chuẩn hóa trước khi thực hiện.
5. Dữ liệu đầu vào cụ thể: Định nghĩa giá trị chuỗi cụ thể là "Khoa học giả tưởng" — một thể loại hoàn toàn nằm ngoài 6 nhóm quy định sẵn của thư viện.
6. Bước thực hiện chi tiết: Chỉ dẫn chi tiết hành động nhập liệu và cách thức kết thúc thao tác (Enter/Click ngoài) để kích hoạt bộ lọc của Flutter Web.
7. Kết quả mong đợi kiểm chứng được: Oracle chi tiết và nghiêm ngặt: yêu cầu xóa bỏ toàn bộ danh sách sách hiển thị và hiển thị văn bản cảnh báo duy nhất 'No books found.'.

- Kỹ thuật sử dụng :
1. Black-box Testing: Đánh giá độ tin cậy và khả năng phòng vệ dữ liệu của giao diện khi tiếp nhận các dữ liệu không mong muốn từ bàn phím người dùng.
2. EP (Phân lớp tương đương): Giá trị dữ liệu "Khoa học giả tưởng" được chọn làm đại diện cho phân vùng dữ liệu không hợp lệ (bất kỳ chuỗi văn bản nào không khớp với 6 thể loại quy định của hệ thống ABC) nhằm xác minh tính đồng bộ của thông báo lỗi trên hệ thống.
