# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày thực thi** | `16/05/2026` |
| **Trình duyệt** | Chrome + Firefox |
| **Hệ điều hành** | Windows + MacOS + Linux |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Đăng nhập | Đăng nhập thành công với email và mật khẩu hợp lệ | Hệ thống chuyển sang trang chủ và hiển thị tên người dùng trên AppBar |Pass |![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/normal%20login)|-|
| TC-02 | Đăng nhập | Hiển thị lỗi khi email không tồn tại | Hệ thống hiển thị thông báo “Không tìm thấy thành viên” | Pass | |-|
| TC-03 | Đăng nhập | Hiển thị lỗi khi mật khẩu không đúng | Hệ thống hiển thị thông báo “Mật khẩu không đúng” | Pass | |-|
| TC-04 | Đăng nhập | Từ chối email không đúng định dạng và không cho phép đăng nhập | Hệ thống chấp nhận email `example@email` và đăng nhập thành công | Fail | | BUG-01 |
|TC-05|Mượn sách|Sách chuyển sang trạng thái "Đang mượn"|Thành công chuyển sang trạng thái đã mượn|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.41.40.png)|không có|
|TC-06|Trả sách|Sách chuyển sang trạng thái "Đã trả"|Thành công chuyển sang trạng thái đã trả|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.49.03.png)|không có|
|TC-07|Hiển thị thông tin mượn sách|Thành viên thấy sách mình mượn, Thủ thư thấy tất cả sách được mượn|Thành công hiển thị sách đang mượn đối với thủ thư|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.54.03.png)|không có|
|TC-08|Tìm kiếm và Lọc sách (REQ-03)|Tìm kiếm chính xác theo cả Tên sách và Tên tác giả. Nếu chuỗi nhập không tồn tại, phải hiển thị câu thông báo `'Không tìm thấy sách nào.'`.|Bộ lọc hoạt động tốt với tên tác giả và tên sách cụ thể. Khi nhập chuỗi rác "ABCxyz123", màn hình ẩn hết sách và hiển thị chính xác `'Không tìm thấy sách nào.'`.|Kết quả đúng (Pass)|Sau bước 2: <img width="2048" height="1189" alt="REQ-03_TC-01_01" src="https://github.com/user-attachments/assets/d6ae9610-25bb-4028-a694-420714d83541" /> <br>Sau bước 3: <img width="2048" height="1189" alt="REQ-03_TC-01_02" src="https://github.com/user-attachments/assets/bd1bb0a1-4a8f-4984-b04f-5e9a2829bb9e" /> <br>Sau bước 4: <img width="2048" height="1189" alt="REQ-03_TC-01_03" src="https://github.com/user-attachments/assets/c0f0a146-793b-496f-a056-f7bdd4017c8f" />|-|
|TC-09|Tìm kiếm và Lọc sách (REQ-03)|Hệ thống tìm kiếm không phân biệt hoa/thường. Nhập chữ hỗn hợp vẫn lọc ra đúng 2 sách của tác giả `"Nguyễn Minh Đức"` và 1 sách `"Lập trình Flutter cơ bản"`.|Hệ thống xử lý chuẩn hóa chuỗi tốt, hiển thị chính xác các thẻ sách tương ứng với cả hai chuỗi dữ liệu hỗn hợp.|Kết quả đúng (Pass)|Sau bước 3: <img width="2048" height="1189" alt="REQ-03_TC-02_01" src="https://github.com/user-attachments/assets/4d56dfee-0697-4502-b6a5-8e9798957c8b" /> <br>Sau bước 6: <img width="2048" height="1189" alt="REQ-03_TC-02_02" src="https://github.com/user-attachments/assets/b50df567-28d1-4914-854c-71cc4294edb2" />|-|
|TC-10|Tìm kiếm và Lọc sách (REQ-03)|Nhập thể loại `"Công nghệ"` hiển thị đúng 8 sách ngành này. Nhập thể loại không tồn tại hiển thị câu thông báo 'Không tìm thấy sách nào.'.|Hệ thống lọc chính xác danh sách 8 mã sách Công nghệ. Khi nhập thể loại không hợp lệ, danh sách trống và hiển thị đúng thông báo `'Không tìm thấy sách nào.'`.|Kết quả đúng (Pass)|Sau bước 3: <img width="2048" height="1189" alt="REQ-03_TC-03_01" src="https://github.com/user-attachments/assets/eb646747-1f1e-4594-81a1-ee7280943c7c" /> <br>Sau bước 5: <img width="2048" height="1189" alt="REQ-03_TC-03_02" src="https://github.com/user-attachments/assets/8a2f2f1f-ac4f-4295-93c7-3f5d6f673f82" />|-|
|TC-11|Tìm kiếm và Lọc sách (REQ-03)|Bộ lọc thể loại không phân biệt hoa/thường. Nhập chữ thường `"công nghệ"` vẫn phải giữ nguyên hiển thị 8 sách Công nghệ.|Hệ thống xử lý phân biệt chữ hoa/thường. Khi nhập chữ thường "công nghệ", toàn bộ danh sách bị ẩn và trả về giao diện rỗng kèm theo hiển thị thông báo `'Không tìm thấy sách nào.'`.|Kết quả sai (Fail)|<img width="2048" height="1189" alt="REQ-03_TC-04_01" src="https://github.com/user-attachments/assets/6eafa568-41e2-452b-a0bb-29453ea0a9f0" />|Bug được trình bày cụ thể hơn qua report `BUG-02`|
 

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
