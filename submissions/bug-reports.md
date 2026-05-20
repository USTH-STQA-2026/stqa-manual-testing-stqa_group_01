# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-04 |
| **REQ liên quan** | REQ-01 |
| **Mức độ** | Medium |
| **Người phát hiện** | Nguyễn Anh Tuấn |
| **Ngày phát hiện** | `17/05/2026` |
| **Trạng thái** | Open |

**Tiêu đề:**
Hệ thống chấp nhận email không đúng định dạng trong chức năng đăng nhập

**Môi trường:**
- Trình duyệt: Firefox
- Hệ điều hành: Ubuntu Linux
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
- Tài khoản thành viên đã được tạo trong hệ thống với email không đúng định dạng: example@email
- Người dùng đang ở màn hình đăng nhập

**Bước tái hiện:**
1. Mở trang đăng nhập của hệ thống.
2. Nhập email: example@email
3. Nhập mật khẩu đúng tương ứng với tài khoản.
4. Nhấn nút Đăng nhập.

**Kết quả mong đợi:**
Hệ thống phải từ chối email không đúng định dạng theo quy tắc: `email@domain.ext`
Hiển thị thông báo lỗi phù hợp và không cho phép đăng nhập.

**Kết quả thực tế:**
Hệ thống chấp nhận email `example@email` và cho phép đăng nhập thành công vào hệ thống.

**Tác động:**
Hệ thống cho phép dữ liệu email không hợp lệ tồn tại và được sử dụng trong quá trình xác thực. Điều này có thể làm giảm tính toàn vẹn dữ liệu,
gây lỗi ở các chức năng sử dụng email sau này, tạo sự mâu thuẫn so với SRS của hệ thống.

**Minh chứng:**
1. Tài khoản có email không đúng định dạng được tạo bởi thủ thư
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/librarian_creating_account.png)
2. Đăng nhập bằng tài khoản trên tại trang đăng nhập
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/login_with_invalid_email_form.png)
3. Hệ thống cho phép đăng nhập bình thường
![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/successful_login.png)

**Đề xuất xử lý:**
Bổ sung kiểm tra định dạng email tại:
- chức năng tạo tài khoản,
- chức năng đăng nhập.
Chỉ chấp nhận email đúng định dạng theo quy tắc: `email@domain.ext`

---
---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-04` |
| **REQ liên quan** | `REQ-03` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Vũ Trần Nam Khánh` |
| **Ngày phát hiện** | `17/05/2026` |
| **Trạng thái** | `Open` |

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
Lập trình viên cần chuẩn hóa cả chuỗi dữ liệu người dùng nhập vào (Input string) và thuộc tính thể loại của sách trong Database về cùng một định dạng (ví dụ: sử dụng function `.toLowerCase()` hoặc `.toUpperCase()`) trước khi thực hiện so sánh chuỗi.
