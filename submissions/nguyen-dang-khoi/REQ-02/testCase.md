| Mục | Nội dung |
|-----|---------|
| **Mô tả** | Hiển thị tất cả sách trong thư viện |
| **Thông tin mỗi sách** | Tên sách, tác giả, thể loại, năm xuất bản, trạng thái (Có sẵn / Đã mượn) |
| **Quyền truy cập** | Cả Thủ thư và Thành viên đều xem được |
| **Cập nhật real-time** | Khi sách được mượn/trả → trạng thái cập nhật ngay lập tức |


| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|--------|
|TC-01|Tính năng mượn sách|Đăng nhập vào thành viên đang hoạt động|Nhấn vào dấu cộng của những quyển sách đang có sẵn|Nhấn vào dấu cộng|Chuyển sang trạng thái đang mượn|REQ-02|EP|
|TC-02|Phạm vi mượn sách|Đăng nhập vào thành viên đang hoạt động|Nhấn vào dấu cộng 4 quyển sách đang có sẵn|Nhấn vào dấu cộng 4 quyển sách khác nhau|Không thỏa mãn giới hạn quyển sách được mượn là 3 do vẫn thành công mượn được 4 quyển sách|REQ-02|BVA|
|TC-03|Tính năng trả sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|Nhấn vào nút trả sách đang mượn đối với thành viên, nhấn nút trả sách khi quá hạn đối với thủ thư|Nhấn trả sách|Hiện "Đã trả"|REQ-02|State Transition|
|TC-04|Hiển thị thông tin mượn sách|Đăng nhập vào thành viên đang hoạt động hoặc thủ thư|1. Đăng nhập vào tài khoản thành viên đang hoạt động 2. Mượn sách 3. Đăng nhập vào tài khoản thủ thư 4. Kiểm tra sách được mượn|Thành viên mượn sách|Thủ thư thấy sách được mượn|REQ-02|Decision Table|


## Tại sao TC-01 tốt?
1. **Mã TC rõ ràng**: `TC-01` – đánh số liên tục, dễ tham chiếu khi báo cáo lỗi.
2. **REQ cụ thể**: Liên kết đến `REQ-02` để biết đang test yêu cầu nào.
3. **Mục tiêu kiểm thử rõ ràng**: "Tính năng mượn sách" – đọc là hiểu ngay đang test gì.
4. **Tiền điều kiện**: "Đăng nhập vào thành viên đang hoạt động" – người khác đọc có thể tái hiện được.
5. **Dữ liệu đầu vào cụ thể**: Ghi rõ "những quyển sách đang có sẵn" – không viết chung chung "chọn sách".
6. **Bước thực hiện rõ ràng**: Chỉ 1 bước duy nhất, hành động cụ thể.
7. **Kết quả mong đợi kiểm chứng được**: "Chuyển sang trạng thái đang mượn" – có thể verify ngay trên UI.


## Tại sao TC-02 tốt?
1. **Mã TC rõ ràng**: `TC-02` – liên tục, dễ tra cứu.
2. **REQ cụ thể**: Liên kết đến `REQ-02` để biết đang test yêu cầu nào.
3. **Mục tiêu kiểm thử rõ ràng**: "Phạm vi mượn sách" – đọc là biết ngay đang kiểm tra giới hạn.
4. **Tiền điều kiện**: "Đăng nhập vào thành viên đang hoạt động" – người khác có thể tái hiện được.
5. **Dữ liệu đầu vào cụ thể**: Ghi rõ "4 quyển sách khác nhau" – test đúng tại biên vượt giới hạn 3 quyển.
6. **Bước thực hiện rõ ràng**: Nhấn dấu cộng 4 lần trên 4 quyển khác nhau – mỗi bước là một hành động.
7. **Kết quả mong đợi kiểm chứng được**: "Không thỏa mãn giới hạn... vẫn thành công mượn được 4 quyển" – có 2 điều kiện kiểm chứng rõ ràng.


## Tại sao TC-03 tốt?
1. **Mã TC rõ ràng**: `TC-03` – đánh số liên tục, dễ tham chiếu khi báo cáo lỗi.
2. **REQ cụ thể**: Liên kết đến `REQ-02` để biết đang test yêu cầu nào.
3. **Mục tiêu kiểm thử rõ ràng**: "Tính năng trả sách" – đọc là hiểu ngay đang test gì.
4. **Tiền điều kiện**: "Đăng nhập vào thành viên đang hoạt động hoặc thủ thư" – bao phủ cả 2 role liên quan.
5. **Dữ liệu đầu vào cụ thể**: Ghi rõ "sách đang mượn" – không viết chung chung "chọn sách bất kỳ".
6. **Bước thực hiện rõ ràng**: 2 luồng rõ ràng – trả đúng hạn (thành viên) và trả quá hạn (thủ thư).
7. **Kết quả mong đợi kiểm chứng được**: "Hiện Đã trả" – có thể verify ngay trên UI.


## Tại sao TC-04 tốt?
1. **Mã TC rõ ràng**: `TC-04` – đánh số liên tục, dễ tham chiếu khi báo cáo lỗi.
2. **REQ cụ thể**: Liên kết đến `REQ-02` để biết đang test yêu cầu nào.
3. **Mục tiêu kiểm thử rõ ràng**: "Hiển thị thông tin mượn sách" – đọc là hiểu ngay đang kiểm tra quyền xem của từng role.
4. **Tiền điều kiện**: "Đăng nhập vào thành viên đang hoạt động hoặc thủ thư" – bao phủ đủ 2 role cần kiểm tra.
5. **Dữ liệu đầu vào cụ thể**: Ghi rõ 4 bước chuẩn bị dữ liệu – mượn sách bằng thành viên trước, sau đó kiểm tra bằng thủ thư.
6. **Bước thực hiện rõ ràng**: Đánh số 1-2-3-4, mỗi bước là một hành động riêng biệt, dễ follow.
7. **Kết quả mong đợi kiểm chứng được**: "Thành viên mượn sách / Thủ thư thấy sách được mượn" – 2 kết quả ứng với 2 role, kiểm chứng được ngay.


### Kỹ thuật được áp dụng
- **Kỹ thuật EP(*Phân lớp tương đương*)**: Sách có sẵn là đại diện cho phân vùng hợp lệ, đảm bảo coverage mà không cần test từng quyển.
- **Kỹ thuật BVA(*Phân tích giá trị biên*)**: Test tại giá trị biên max+1 (4 > 3), đây là nơi lỗi dễ xảy ra nhất.
- **Kỹ thuật State Transition(*Hệ thống có nhiều trạng thái*)**: Kiểm tra đúng sự chuyển đổi trạng thái Đang mượn → Đã trả, bao phủ cả 2 đường chuyển trạng thái khác nhau.
- **Kỹ thuật Decision Table(*Nhiều điều kiện kết hợp*)**: Có 2 điều kiện (role = Thành viên / Thủ thư) cho ra 2 kết quả khác nhau, Decision Table đảm bảo không bỏ sót tổ hợp nào.