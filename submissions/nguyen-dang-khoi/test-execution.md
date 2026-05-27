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

| TC ID | Feature Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|-------|--------------|--------------------------|---------------|------------|----------|-----|
| TC-01 | Borrow Book | Book status changes to "Borrowing" | Successfully changed to borrowed status | Feature works normally | ![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.41.40.png) | None |
| TC-02 | Return Book | Book status changes to "Returned" | Successfully changed to returned status | Feature works normally | ![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.49.03.png) | None |
| TC-03 | Display Borrowing Information | Member sees their own borrowed books; Librarian sees all borrowed books | Successfully displayed borrowed books for librarian | Feature works normally | ![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/screenshot-2026-05-19_15.54.03.png) | None |
| TC-04 | Display Book Information | All book details are shown: author name, genre, publication year, book ID | All book details displayed correctly including author name, genre, publication year, and book ID | Feature works normally |![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/swappy-20260527-103605.png)| None |
| TC-05 | Display Book Status | Correct status displayed: "Borrowing" / "Available" / "Lost" | Book status displayed correctly according to current state | Feature works normally |![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/swappy-20260527-103645.png)| None |
---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 3 |
| Pass | 3 |
| Fail | 0 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | **75%** |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Mượn sách | 1| 1 | 0 | 100% |
| Trả sách | 1 | 1 | 0 | 100% |
| Hiển thị thông tin mượn sách | 1 | 1 | 0 | 100% |
| **Tổng** | **3** | **3** | **0** | **100%** |
