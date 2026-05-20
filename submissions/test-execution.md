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
|TC-12|Mượn sách|Thành viên tạm ngưng bị từ chối mượn sách và được thông báo đúng lí do từ chối|Thành viện bị từ chối nhưng bị thông báo sai lí do "Thành viên hết hạn"|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-04_01.png)|Hệ thống hiển thị sai lí do bị từ chối "Thành viên hết hạn"|
|TC-13|Mượn sách|Thành viên hết hạn bị từ chối mượn sách và được thông báo đúng lí do từ chối|Thành viên bị từ chối và bị thông báo đúng lí do|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-05_01.png)||
|TC-14|Mượn sách|Thành viên hoạt động được phép mượn sách và được thông báo mượn sách thành công|Thành viên được phép mượn và được thông báo thành công|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-06_01.png)||
|TC-15|Mượn sách|Thành viên bị từ chối mượn sách ở trạng thái "Đang mượn"|Không có nút mượn sách ở những sách "Đang mượn"|Chức năng hoạt động bình thường|||
|TC-16|Mượn sách|Thành viên bị từ chối mượn sách khi đã mượn 3 sách|Thành viên có thể mượn tối đa 4 sách|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_01.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_02.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_03.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_04.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_05.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_06.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_07.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_08.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_09.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_10.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_11.png)|Thành viên mượn quá giới hạn 3 sách (Mượn được 4 sách)|
|TC-17|Mượn sách|Thành viên mượn sách thành công và được giao đúng hạn trả|Thành viên mượn sách thành công và được giao hạn 14 ngày kể từ ngày mượn|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-09_01.png)||
|TC-18|Trả sách|Sau khi trả sách, sách trở về trạng thái "Có sẵn"|Sau khi trả sách, sách đã trở về trạng thái "Có sãn"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_sachdangmuon.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_trasachdangmuon.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_sachtrovecosan.png)||
|TC-19|Trả sách|Sau khi trả sách quá hạn, hệ thống hiển thị **cảnh báo quá hạn**|Sau khi trả sách quá hạn, hệ thống chỉ hiện thị mỗi "trả sách thành công"|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_baoquahan.png)|Hệ thống không hiển thị **cảnh báo quá hạn**|
|TC-20|Trả sách|Sách đã trả ở trạng thái "Có sẵn"|Sách đã trở về trạng thái "Có sẵn"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/fba7f78dc0661c44f4b1d7dafc7435f65a64744d/screenshots/REQ-05_sachcosan.png)||


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
