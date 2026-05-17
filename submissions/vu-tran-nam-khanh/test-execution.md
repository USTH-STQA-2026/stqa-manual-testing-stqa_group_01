# Test Execution — Kết quả thực thi kiểm thử

> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày thực thi** | `17/05/2026` |
| **Trình duyệt** | Chrome |
| **Hệ điều hành** | Windows + MacOS |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
|TC-01|Tìm kiếm và Lọc sách (REQ-03)|Tìm kiếm chính xác theo cả Tên sách và Tên tác giả. Nếu chuỗi nhập không tồn tại, phải hiển thị câu thông báo `'Không tìm thấy sách nào.'`.|Bộ lọc hoạt động tốt với tên tác giả và tên sách cụ thể. Khi nhập chuỗi rác "ABCxyz123", màn hình ẩn hết sách và hiển thị chính xác `'Không tìm thấy sách nào.'`.|Kết quả đúng (Pass)|minh chứng ở đây|-|
|TC-02|Tìm kiếm và Lọc sách (REQ-03)|Hệ thống tìm kiếm không phân biệt hoa/thường. Nhập chữ hỗn hợp vẫn lọc ra đúng 2 sách của tác giả `"Nguyễn Minh Đức"` và 1 sách `"Lập trình Flutter cơ bản"`.|Hệ thống xử lý chuẩn hóa chuỗi tốt, hiển thị chính xác các thẻ sách tương ứng với cả hai chuỗi dữ liệu hỗn hợp.|Kết quả đúng (Pass)|minh chứng ở đây|-|
|TC-03|Tìm kiếm và Lọc sách (REQ-03)|Nhập thể loại `"Công nghệ"` hiển thị đúng 8 sách ngành này. Nhập thể loại không tồn tại hiển thị câu thông báo 'Không tìm thấy sách nào.'.|Hệ thống lọc chính xác danh sách 8 mã sách Công nghệ. Khi nhập thể loại không hợp lệ, danh sách trống và hiển thị đúng thông báo `'Không tìm thấy sách nào.'`.|Kết quả đúng (Pass)|minh chứng ở đây|-|
|TC-04|Tìm kiếm và Lọc sách (REQ-03)|Bộ lọc thể loại không phân biệt hoa/thường. Nhập chữ thường `"công nghệ"` vẫn phải giữ nguyên hiển thị 8 sách Công nghệ.|Hệ thống xử lý phân biệt chữ hoa/thường. Khi nhập chữ thường "công nghệ", toàn bộ danh sách bị ẩn và trả về giao diện rỗng kèm theo hiển thị thông báo `'Không tìm thấy sách nào.'`.|Kết quả sai (Fail)|minh chứng ở đây|Bug được trình bày cụ thể hơn qua report `BUG-01`|
||||||||

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
