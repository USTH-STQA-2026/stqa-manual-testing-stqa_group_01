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
|01|Đăng nhập vào hệ thống|Đăng nhập thành công với tài khoản trong hệ thống, thất bại nếu tài khoản không tồn tại|Thành công đăng nhập nếu đúng tài khoản và mật khẩu, thông báo mật khẩu hoặc tài khoản sai nếu thất bại|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/TC01.png)|Email không theo dạng example@gmail.com vẫn có thể đăng nhập bình thường|
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
|01|Trả sách|Sau khi trả sách, sách trở về trạng thái "Có sẵn"|Sau khi trả sách, sách đã trở về trạng thái "Có sãn"|Hoạt động như mong đợi|||
|02|Trả sách|Sau khi trả sách quá hạn, hệ thống hiển thị **cảnh báo quá hạn**|Sau khi trả sách quá hạn, hệ thống chỉ hiện thị mỗi "trả sách thành công"|Chưa hoạt động theo yêu cầu||Hệ thống không hiển thị **cảnh báo quá hạn**|
|03|Trả sách|Sách đã trả ở trạng thái "Có sẵn"|Sách đã trở về trạng thái "Có sẵn"|Hoạt động như mong đợi|||
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
|04|Mượn sách|Thành viên tạm ngưng bị từ chối mượn sách và bị thông báo đúng lí do từ chối|Thành viện bị từ chối nhưng bị thông báo sai lí do "Thành viên hết hạn"|Chưa thỏa mãn yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-04_01.png)|Hệ thống hiển thị sai lí do bị từ chối "Thành viên hết hạn"|
|05|Mượn sách|Thành viên hết hạn bị từ chối mượn sách và bị thông báo đúng lí do từ chối|Thành viên bị từ chối và bị thông báo đúng lí do|Hoạt động như mong đợi|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-05_01.png)||
|06|Mượn sách|Thành viên hoạt động được phép mượn sách và bị thông báo "mượn sách thành công|Thành viên được phép mượn và được thông báo thành công|Hoạt động như mong đợi|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-06_01.png)||
|07|Mượn sách|Thành viên bị từ chối mượn sách ở trạng thái đang được mượn|Không có nút mượn sách ở những sách "Đang mượn"|Thỏa mãn yêu cầu|||
|08|Mượn sách|Thành viên bị từ chối mượn sách khi đã mượn 3 sách|Thành viên có thể mượn tối đa 4 sách|Chưa hoạt đông theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_01.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_02.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_03.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_04.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_05.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_06.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_07.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_08.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_09.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_10.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_11.png)|Thành viên mượn quá giới hạn 3 sách (Mượn được 4 sách)|
|09|Mượn sách|Thành viên mượn sách thành công và được giao hạn trả đúng|Thành viên mượn sách thành công và được giao hạn 14 ngày kể từ ngày mượn|Hoạt động như mong đợi|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-09_01.png)||


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
