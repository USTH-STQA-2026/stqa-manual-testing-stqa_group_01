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
| An01 | Xử lý sách quá hạn (REQ-06) | BR001 và BR003 chuyển sang trạng thái "Quá hạn" sau khi Thủ thư nhấn "Kiểm tra quá hạn" | Sau khi nhấn "Kiểm tra quá hạn", BR001 (dueDate: 15/09/2024) và BR003 (dueDate: 15/10/2024) đều hiển thị trạng thái "Quá hạn" | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An01.png) | — |
| An02 | Xử lý sách quá hạn (REQ-06) | Phiếu đã trả (BR002, BR005) giữ nguyên trạng thái "Đã trả", không bị đổi thành "Quá hạn" | Sau khi nhấn "Kiểm tra quá hạn", BR002 và BR005 vẫn hiển thị "Đã trả" — không bị thay đổi trạng thái | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An02.png) | — |
| An03 | Xử lý sách quá hạn (REQ-06) | Tài khoản Thành viên không thấy nút "Kiểm tra quá hạn" | Đăng nhập bằng `ba.nguyen@email.com`, vào tab "Mượn / Trả" — nút "Kiểm tra quá hạn" không xuất hiện trong giao diện | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An03.png) | — |
| An04 | Xử lý sách quá hạn (REQ-06) | Thành viên MEM002 chỉ thấy phiếu quá hạn của mình (BR001), không thấy phiếu của MEM006 (BR003) | Sau khi Thủ thư nhấn "Kiểm tra quá hạn" và đăng xuất, MEM002 đăng nhập và thấy chỉ thấy phiếu quá hạn của mình| Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An04.png) | — |
| An05 | Xử lý sách quá hạn (REQ-06) | Phiếu có `dueDate` bằng đúng ngày hiện tại bị đánh dấu "Quá hạn" | Phiếu BR006 (hạn trả trùng với ngày hệ thống giả lập) được chuyển sang trạng thái "Quá hạn" | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An05.png) | — |
| An06 | Xử lý sách quá hạn (REQ-06) | Phiếu chưa tới hạn (`dueDate` > ngày hiện tại) KHÔNG bị đánh dấu "Quá hạn" | Phiếu BR006 (hạn trả ở tương lai) vẫn giữ nguyên trạng thái "Đang mượn" sau khi check | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An06.png) | — |
| An07 | Xử lý sách quá hạn (REQ-06) | Các phiếu quá hạn hiển thị mặc định là "Đang mượn" TRƯỚC khi nhấn nút | Trước khi nhấn nút "Kiểm tra quá hạn", BR001 và BR003 vẫn đang hiển thị trạng thái "Đang mượn" | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An07.png) | — |
| An08 | Borrow Record Lookup (REQ-08) | Librarian can view all borrow records (BR001–BR005) across all members | Logged in as Librarian → "Mượn / Trả" tab → all 5 records (BR001–BR005) are visible with correct member names, book titles, dates, and statuses | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An08.png) | — |
| An09 | Borrow Record Lookup (REQ-08) | Member MEM002 sees only their own records (BR001, BR004) in the default view — no other members' records shown | Logged in as MEM002 → "Mượn / Trả" tab → only BR001 ("Đang mượn") and BR004 ("Đã trả") are displayed; BR002, BR003, BR005 are not visible | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An09.png) | — |
| An10 | Borrow Record Lookup (REQ-08) | Member MEM002 enters MEM006's ID in the lookup field — should NOT see BR003 | Logged in as MEM002 → "Mượn / Trả" tab → entered MEM006 in the "Tra cứu phiếu mượn" search field → BR003 (Quản trị nhân sự hiện đại, belonging to Hoàng Cá Biệt) is displayed to MEM002 — unauthorized access | **Fail** | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An10.png) | BUG-AN |
| An11 | Borrow Record Lookup (REQ-08) | All 5 required fields are present in each borrow record: Record ID, Book, Borrow date, Due date, Status | Logged in as Librarian → inspected BR001 → all fields visible: BR001, "Kiểm thử phần mềm nhập môn", 01/09/2024, 15/09/2024, "Đang mượn" (before clicking "Kiểm tra sách quá hạn") | Pass | ![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An11.png) | — |

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
