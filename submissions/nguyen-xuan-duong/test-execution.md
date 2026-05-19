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
|01|Trả sách|Sau khi trả sách, sách trở về trạng thái "Có sẵn"|Sau khi trả sách, sách đã trở về trạng thái "Có sãn"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_sachdangmuon.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_trasachdangmuon.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_sachtrovecosan.png)||
|02|Trả sách|Sau khi trả sách quá hạn, hệ thống hiển thị **cảnh báo quá hạn**|Sau khi trả sách quá hạn, hệ thống chỉ hiện thị mỗi "trả sách thành công"|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/f8a198fd435f32a6d3f8792820ab188d6fd51b1b/screenshots/REQ-05_baoquahan.png)|Hệ thống không hiển thị **cảnh báo quá hạn**|
|03|Trả sách|Sách đã trả ở trạng thái "Có sẵn"|Sách đã trở về trạng thái "Có sẵn"|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/fba7f78dc0661c44f4b1d7dafc7435f65a64744d/screenshots/REQ-05_sachcosan.png)||
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
|04|Mượn sách|Thành viên tạm ngưng bị từ chối mượn sách và được thông báo đúng lí do từ chối|Thành viện bị từ chối nhưng bị thông báo sai lí do "Thành viên hết hạn"|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-04_01.png)|Hệ thống hiển thị sai lí do bị từ chối "Thành viên hết hạn"|
|05|Mượn sách|Thành viên hết hạn bị từ chối mượn sách và được thông báo đúng lí do từ chối|Thành viên bị từ chối và bị thông báo đúng lí do|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-05_01.png)||
|06|Mượn sách|Thành viên hoạt động được phép mượn sách và được thông báo mượn sách thành công|Thành viên được phép mượn và được thông báo thành công|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-06_01.png)||
|07|Mượn sách|Thành viên bị từ chối mượn sách ở trạng thái "Đang mượn"|Không có nút mượn sách ở những sách "Đang mượn"|Chức năng hoạt động bình thường|||
|08|Mượn sách|Thành viên bị từ chối mượn sách khi đã mượn 3 sách|Thành viên có thể mượn tối đa 4 sách|Chức năng chưa hoạt động theo yêu cầu|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_01.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_02.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_03.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_04.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_05.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_06.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_07.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_08.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_09.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_10.png)<br>![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-08_11.png)|Thành viên mượn quá giới hạn 3 sách (Mượn được 4 sách)|
|09|Mượn sách|Thành viên mượn sách thành công và được giao đúng hạn trả|Thành viên mượn sách thành công và được giao hạn 14 ngày kể từ ngày mượn|Chức năng hoạt động bình thường|![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/17442cedae656075d4eeb29b2e600691f5011a4c/screenshots/REQ-04/REQ-04_TC-09_01.png)||


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
