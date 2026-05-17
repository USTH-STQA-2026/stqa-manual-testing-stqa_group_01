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
| TC-01 | Kiểm tra tính năng '"Tìm kiếm theo Tên sách, Tên tác giả"' và xử lý khi không có dữ liệu khớp.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang hiển thị trong mục 'Sách'| Bước 1. Nhấp chuột vào thanh tìm kiếm. 2. Nhập vào Tên tác giả và xác nhận bộ lọc. 3. Xóa thanh tìm kiếm, nhập vào Tên sách cụ thể. 4. Xóa thanh tìm kiếm, nhập vào một chuỗi ký tự không tồn tại.| '"Nguyễn Minh Đức"', '"Lập trình Flutter cơ bản"' và '"ABCxyz123"'| Sau bước 2, sẽ hiển thị cuốn sách với mã 'BOOK001' (Lập trình Flutter cơ bản) và 'BOOK009' (Nhập môn lập trình Python). Sau bước 3, Hiển thị duy nhất 1 cuốn sách mã 'BOOK001' (Lập trình Flutter cơ bản). Sau bước 4 sẽ hiển thị kết quả chuỗi chính xác 'Không tìm thấy sách nào'| REQ-03| EP và Black-box Testing|
| TC-02 | Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) khi tìm kiếm sách.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang hiển thị trong mục 'Sách'| Bước 1. Nhấp chuột vào thanh tìm kiếm. 2. Nhập chuỗi dữ liệu đầu vào 1. 3. Kiểm tra danh sách hiển thị. 4. Xóa toàn bộ ký tự trong thanh tìm kiếm. 5. Nhập chuỗi dữ liệu đầu vào 2. 6. Kiểm tra danh sách hiển thị.|1. '"nGuyễn mInh ĐứC"' và 2. '"lẬp trìnH flUTTer cơ bẢn"'| Sau bước 3, hệ thống lọc và hiển thị chính xác 2 cuốn sách của tác giả: mã 'BOOK001' (Lập trình Flutter cơ bản) và 'BOOK009' (Nhập môn lập trình Python), các sách khác sẽ bị ẩn. Sau bước 6, hệ thống lọc và hiển thị duy nhất 1 cuốn sách: mã 'BOOK001' (Lập trình Flutter cơ bản).| REQ-03 | EP và Black-box Testing|
|TC-03|Kiểm tra tính năng lọc danh sách theo thể loại với trường hợp hợp lệ và không hợp lệ.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang hiển thị trong mục 'Sách'|Bước 1. Nhấp chuột vào thanh '"Lọc theo thể loại"'. 2. Nhập chính xác tên một thể loại hợp lệ. 3. Kiểm tra danh sách hiển thị. 4. Xóa bộ lọc thanh thể loại. 5. Nhập vào một thể loại không tồn tại trong hệ thống.|"Công nghệ" và "Khoa học ảo tưởng"|Sau bước 3, Chỉ hiển thị 8 cuốn sách thuộc nhóm "Công nghệ" (Mã sách từ 'BOOK001', 'BOOK002', 'BOOK003', 'BOOK005', 'BOOK008', 'BOOK009', 'BOOK010', 'BOOK011'). Bất kỳ sách nào thuộc thể loại khác (như 'Kinh tế', 'Văn học',...) đều bị ẩn khỏi màn hình. Sau bước 5, Toàn bộ danh sách biến mất, hiển thị chuỗi chuỗi chính xác '"Không tìm thấy sách nào"'.|REQ-03|EP và Black-box Testing|
|TC-04| Kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) của tính năng lọc theo thể loại.| Đã truy cập được và đã đăng nhập thành công vào hệ thống và đang hiển thị trong mục 'Sách'| Bước 1. Nhấp chuột vào ô nhập '"Lọc theo thể loại"'. 2. Nhập tên thể loại viết hoàn toàn bằng chữ thường. 3. Nhấp chuột ra ngoài hoặc nhấn Enter để kích hoạt bộ lọc. 4. Kiểm tra sự thay đổi của danh sách sách hiển thị trên màn hình.|'"công nghệ"'|Hệ thống nhận diện bộ lọc không phân biệt hoa thường, giữ nguyên hiển thị chính xác 8 cuốn sách thuộc nhóm thể loại '"Công nghệ"' giống như khi nhập chữ hoa chuẩn (Mã sách từ 'BOOK001', 'BOOK002', 'BOOK003', 'BOOK005', 'BOOK008', 'BOOK009', 'BOOK010', 'BOOK011').|REQ-03| EP và Black-box Testing|

---

## Bước 3: Giải thích các TCs (explanation)

# TC-01 :
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Mã TC-01 được đánh số liên tục trong phân nhóm tính năng.
2. REQ cụ thể: Liên kết chặt chẽ đến tài liệu đặc tả REQ-03.
3. Mục tiêu kiểm thử rõ ràng: Mô tả chính xác việc xác thực khả năng lọc theo cả hai điều kiện (Tên sách/Tên tác giả) trên cùng một thanh tìm kiếm và kiểm tra kịch bản không có dữ liệu.
4. Tiền điều kiện cụ thể: Đảm bảo hệ thống ở màn hình danh sách mặc định để các phép tìm kiếm kế tiếp không bị ảnh hưởng bởi dữ liệu thừa.
5. Dữ liệu đầu vào cụ thể: Cung cấp 3 chuỗi dữ liệu rõ ràng: tên tác giả "Nguyễn Minh Đức", tên sách "Lập trình Flutter cơ bản", và chuỗi ký tự rác "ABCxyz123".
6. Bước thực hiện chi tiết: Các bước thao tác tuần tự hóa một chuỗi các hành động liên tiếp của người dùng thực tế một cách logic.
7. Kết quả mong đợi kiểm chứng được: Quy định rõ ràng sự thay đổi giao diện theo từng bước mốc dữ liệu. Đặc biệt, oracle bắt buộc hệ thống phải hiển thị chính xác chuỗi ký tự tiếng Anh 'No books found.' theo đúng yêu cầu nghiêm ngặt của SRS thay vì hiển thị tiếng Việt tự do.

- Kỹ thuật sử dụng :
1. Black-box Testing: Kiểm tra phản hồi đầu ra hiển thị trên màn hình (danh sách thẻ sách hoặc chuỗi thông báo lỗi) tương ứng với dữ liệu chuỗi văn bản đầu vào.
2. EP (Phân lớp tương đương): Tập hợp dữ liệu tìm kiếm được chia làm 2 phân vùng lớn: Lớp dữ liệu tồn tại trong DB (gồm phân nhóm Tên sách và phân nhóm Tên tác giả) và Lớp dữ liệu hoàn toàn không tồn tại trong DB. Chuỗi "ABCxyz123" là đại diện cho phân vùng không tồn tại nhằm kiểm tra luồng xử lý ngoại lệ.


# TC-02 :
- Tại sao TC này tốt ?

1. Mã TC rõ ràng: Sử dụng mã TC-02 giúp việc theo dõi kết quả thực thi và liên kết đến các bug report sau này trở nên chính xác, dễ dàng.
2. REQ cụ thể: Gắn trực tiếp với mã yêu cầu nghiệp vụ REQ-03 để kiểm soát độ phủ kiểm thử.
3. Mục tiêu kiểm thử rõ ràng: Nêu rõ mục đích cốt lõi là kiểm tra tính không phân biệt chữ HOA/thường (Case-Insensitivity) của thanh tìm kiếm.
4. Tiền điều kiện cụ thể: Xác định rõ trạng thái bắt đầu (Thủ thư đăng nhập thành công và màn hình đang ở danh mục "Sách") nhằm đảm bảo môi trường kiểm thử luôn đồng nhất.
5. Dữ liệu đầu vào cụ thể: Không viết chung chung là "nhập văn bản bất kỳ", test case chỉ rõ hai chuỗi hoán đổi định dạng chữ phức tạp là "nGuyễn mInh ĐứC" và "lẬp trìnH flUTTer cơ bẢn".
6. Bước thực hiện chi tiết: Đánh số rõ ràng từ bước 1 đến bước 6; tách biệt rạch ròi các hành động nhập liệu, kiểm tra giao diện, và xóa dữ liệu cũ để tránh nhầm lẫn cho tester.
7. Kết quả mong đợi kiểm chứng được: Oracle được viết vô cùng mạnh mẽ bằng cách chỉ rõ mã sách phải hiển thị trên màn hình (BOOK001 và BOOK009) thay vì ghi chung chung là "Hệ thống tìm kiếm được".
Kỹ thuật được áp dụng

- Kỹ thuật sử dụng :

1. Black-box Testing: Thao tác hoàn toàn trên giao diện người dùng bằng cách giả lập hành vi nhập văn bản vào hộp tìm kiếm, hoàn toàn không can thiệp hay đọc mã nguồn xử lý chuỗi của framework Flutter Web.
2. EP (Phân lớp tương đương): Miền dữ liệu đầu vào của thanh tìm kiếm được chia làm các lớp định dạng ký tự: Chữ thường, Chữ HOA, và Chữ hỗn hợp (xen kẽ HOA/thường). TC-02 chọn lớp chữ hỗn hợp để làm giá trị đại diện kiểm thử khả năng chuẩn hóa chuỗi của hệ thống.


# TC-03 :
- Tại sao TC này tốt?

1. Mã TC rõ ràng: Định danh TC-03 giúp duy trì thứ tự tuần tự trong tài liệu kiểm thử, tạo điều kiện thuận lợi cho việc ánh xạ và truy vết trạng thái thực thi.
2. REQ cụ thể: Liên kết trực tiếp và duy nhất đến yêu cầu chức năng bộ lọc trong REQ-03.
3. Mục tiêu kiểm thử rõ ràng: Nêu bật được mục đích tích hợp sau khi gộp luồng: kiểm tra toàn diện khả năng phản hồi của bộ lọc thể loại đối với cả trường hợp dữ liệu biên chấp nhận được (Happy Path) và dữ liệu nằm ngoài phạm vi xử lý (Negative Path).
4. Tiền điều kiện cụ thể: Xác định rõ ràng trạng thái hệ thống phải ở giao diện danh sách mặc định để bảo toàn tính khách quan khi quan sát số lượng thẻ sách bị thu hẹp hoặc ẩn đi.
5. Dữ liệu đầu vào cụ thể: Ghi rõ ràng hai chuỗi ký tự kiểm thử tương phản: một thể loại chuẩn có trên giao diện là "Công nghệ" và một chuỗi thể loại giả lập không tồn tại là "Khoa học giả tưởng".
6. Bước thực hiện chi tiết: Chia nhỏ quy trình kiểm thử thành 5 bước tuần tự hành động rõ ràng; phân định rạch ròi giữa thao tác nhập, xóa bộ lọc cũ, và nhập dữ liệu ngoại lệ để tránh việc tester thực thi sai cách.
7. Kết quả mong đợi kiểm chứng được: Oracle xác định chính xác sự biến đổi của UI theo từng mốc dữ liệu: yêu cầu hiển thị đúng danh sách 8 mã sách cụ thể từ BOOK001 đến BOOK011 ở bước 3, và bắt buộc xuất hiện chuỗi ký tự chính xác 'No books found.' ở bước 5.

- Kỹ thuật áp dụng :

1. Black-box Testing: Thao tác kiểm thử thuần túy dựa trên các thành phần UI hiển thị đầu vào và đầu ra của hệ thống, hoàn toàn không can thiệp vào mã nguồn lưu trữ mảng dữ liệu (in-memory) của ứng dụng.
2. EP (Phân lớp tương đương): Miền dữ liệu nhập vào thanh lọc được chia thành 2 phân vùng tương đương: Nhóm các chuỗi ký tự thuộc 6 thể loại quy định trên màn hình (đại diện bởi "Công nghệ") và Nhóm các chuỗi văn bản nằm ngoài danh mục hệ thống hỗ trợ (đại diện bởi "Khoa học giả tưởng").

# TC-04 : 
- Tại sao TC này tốt?

1. Mã TC rõ ràng: Định danh mã TC-04 tiếp nối mạch lạc cấu trúc phân nhóm chức năng của REQ-03.
2. REQ cụ thể: Ánh xạ chính xác tới ràng buộc quy tắc nghiệp vụ "Tìm kiếm/Lọc không phân biệt hoa/thường" quy định trong đặc tả hệ thống.
3. Mục tiêu kiểm thử rõ ràng: Định nghĩa rõ ràng mục đích kiểm tra khả năng chuẩn hóa chuỗi và tính không phân biệt chữ HOA/thường (Case-Insensitivity) riêng biệt cho tính năng lọc thể loại.
4. Tiền điều kiện cụ thể: Thiết lập trạng thái ban đầu ổn định (Thủ thư đăng nhập, danh sách ở trạng thái gốc) giúp tester dễ dàng đối chiếu kết quả trả về với trường hợp gõ chữ hoa chuẩn ở TC trước.
5. Dữ liệu đầu vào cụ thể: Xác định chính xác một chuỗi văn bản viết thường hoàn toàn là "công nghệ" (khác với chuỗi hiển thị gốc trên giao diện UI là "Công nghệ").
6. Bước thực hiện chi tiết: Các bước thao tác (1 đến 4) mô tả chi tiết cách thức người dùng kích hoạt bộ lọc trên nền tảng Flutter Web bằng cách "Nhấp chuột ra ngoài hoặc nhấn Enter" để đảm bảo tính tái hiện lỗi cao.
7. Kết quả mong đợi kiểm chứng được: Oracle thiết lập tiêu chuẩn kiểm chứng khách quan: hệ thống bắt buộc phải nhận diện thông minh chuỗi viết thường và hiển thị nguyên vẹn danh sách 8 mã sách thuộc thể loại đó thay vì để danh sách trống và báo lỗi. -> Vì thế, chúng ta ghi nhận kết quả Fail và xuất bản báo cáo lỗi BUG-01.

- Kỹ thuật áp dụng

1. Black-box Testing: Tester chỉ đứng từ góc độ người dùng cuối để nhập dữ liệu thô từ bàn phím và đối chiếu sự thay đổi trực quan của các thẻ thành phần trên màn hình giao diện.
2. EP (Phân lớp tương đương): Phân chia miền định dạng văn bản đầu vào của thanh lọc thể loại thành các khối định dạng ký tự khác nhau. TC-04 sử dụng một giá trị đại diện cho khối "Chữ viết thường hoàn toàn" nhằm kiểm tra toàn vẹn chức năng tự động chuyển đổi định dạng chuỗi của ứng dụng.
