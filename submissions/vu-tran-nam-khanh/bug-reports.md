# Bug Reports — Báo cáo lỗi

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `<!-- 17/05/2026 -->` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-04` |
| **REQ liên quan** | `REQ-03` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | Vũ Trần Nam Khánh |
| **Ngày phát hiện** | 17/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
Tính năng lọc theo thể loại phân biệt chữ HOA/thường, không trả kết quả khi nhập chữ thường

**Môi trường:**
- Trình duyệt: Chrome
- Hệ điều hành: Windows 11 / macOS
- Ngôn ngữ giao diện: Tiếng Việt
- Nền tảng hệ thống: Flutter Web

**Điều kiện tiên quyết:**
Đã đăng nhập thành công vào hệ thống và đang đứng tại tab "Sách".

**Bước tái hiện:**
1. Nhấp chuột vào thanh văn bản đầu vào: "Lọc theo thể loại (VD: Công nghệ, Kinh tế...)".
2. Nhập vào chuỗi văn bản viết thường hoàn toàn: `"công nghệ"`.
3. Nhấn phím Enter hoặc nhấp chuột ra ngoài vùng trống để hệ thống thực thi bộ lọc.
4. Quan sát danh sách sách hiển thị trên màn hình UI.

**Kết quả mong đợi:**
Hệ thống phải xử lý không phân biệt chữ hoa/chữ thường (Case-Insensitive), nhận diện được thể loại và hiển thị danh sách gồm 8 cuốn sách thuộc nhóm "Công nghệ" (Mã sách từ BOOK001, BOOK002, BOOK003, BOOK005, BOOK008, BOOK009, BOOK010, BOOK011).

**Kết quả thực tế:**
Hệ thống xử lý phân biệt chữ hoa/chữ thường. Toàn bộ danh sách sách biến mất hoàn toàn khỏi màn hình, giao diện trả về thông báo lỗi: `'Không tìm thấy sách nào'`. Bộ lọc chỉ hoạt động khi người dùng gõ chuẩn xác từng ký tự in hoa `"Công nghệ"`.

**Tác động:**
Gây ảnh hưởng tiêu cực đến trải nghiệm sử dụng (UX). Người dùng nhập liệu thủ công bằng chữ thường theo thói quen sẽ cho rằng hệ thống không có sách hoặc bị lỗi tính năng lọc dữ liệu, mặc dù dữ liệu thực tế vẫn tồn tại trong hệ thống.

**Minh chứng:**


<img width="1937" height="1159" alt="image" src="https://github.com/user-attachments/assets/1c38bd8d-9068-4e42-a239-0ae97d1a3b35" />


**Đề xuất xử lý:**
Lập trình viên cần chuẩn hóa cả chuỗi dữ liệu người dùng nhập vào (Input string) và thuộc tính thể loại của sách trong Database về cùng một định dạng (ví dụ: sử dụng phương thức `.toLowerCase()` hoặc `.toUpperCase()`) trước khi thực hiện so sánh chuỗi.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
