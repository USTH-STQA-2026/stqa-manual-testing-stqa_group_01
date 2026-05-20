# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `20/05/2026` |

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
| **TC liên quan** | `TC-11` |
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

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-12` |
| **REQ liên quan** | `REQ-04` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Nguyễn Xuân Dương và Vũ Trần Nam Khánh` |
| **Ngày phát hiện** | `18/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Hệ thống báo lỗi 'Thành viên hết hạn' thay vì 'Thành viên tạm ngưng' khi mượn sách trong tài khoản thành viên ở trạng thái "Tạm ngưng"

**Môi trường:**
- Trình duyệt: Chrome
- Hệ điều hành: `Windows`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`Thành viên bị tạm ngưng, sách ở trạng thái "Có sẵn"`

**Bước tái hiện:**
1. `Đăng nhập vào hệ thống với tài khoản bị tạm ngưng`
2. `Mượn bất kỳ một sách có sẵn`
3. `Kiểm tra phản hồi của hệ thống`

**Kết quả mong đợi:**
- Hệ thống báo lỗi `'Thành viên tạm ngưng'`

**Kết quả thực tế:**
- Hệ thống báo lỗi: `'Thành viên hết hạn'`

**Tác động:**
- Gây lỗi sai lệch luồng thông tin, ảnh hưởng đến quá trình quản lý của thủ thư.  
- Gây lỗi đến sử dụng (UX).

**Minh chứng:**
<img width="2008" height="1160" alt="REQ-04_TC-04_01" src="https://github.com/user-attachments/assets/c67c1c48-f7b2-42d5-b973-44dd0965cf9c" />

**Đề xuất xử lý:**
Cần kiểm tra lại cấu trúc rẽ nhánh logic và bóc tách các mệnh đề kiểm tra điều kiện clauses của trạng thái thành viên.

---

## BUG-04

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | `TC-16` |
| **REQ liên quan** | `REQ-04` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Xuân Dương và Vũ Trần Nam Khánh` |
| **Ngày phát hiện** | `18/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Thành viên mượn đến 4 sách thay vì 3 sách trong hệ thống

**Môi trường:**
- Trình duyệt: Chrome
- Hệ điều hành: `Windows`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`Thành viên hoạt động, sách ở trạng thái "Có sẵn"`

**Bước tái hiện:**
1. `Đăng nhập vào hệ thống với tài khoản đang hoạt động`
2. `Mượn 1,2,3,4 sách ở trạng thái "Có sẵn"`
3. `Kiểm tra kết quả phản hồi của hệ thống`

**Kết quả mong đợi:**
`Khi mượn đến sách thứ 4, hệ thống phải báo lỗi đã mượn đủ 3 sách và từ chối nhận thêm sách`

**Kết quả thực tế:**
`Hệ thống chấp nhận sách thứ 4 và hệ thống từ chối và báo lỗi ở sách thứ 5.`

**Tác động:**
- Vi phạm đến yêu cầu nghiệp vụ.

**Minh chứng:**
- Mượn được 3 sách :
<img width="2008" height="1160" alt="REQ-04_TC-08_07" src="https://github.com/user-attachments/assets/3ad3e644-12b8-4d97-b215-76a48c92b240" />

- Hệ thống vẫn cho mượn được sách thứ 4:

<img width="2008" height="1160" alt="REQ-04_TC-08_09" src="https://github.com/user-attachments/assets/74370bd9-6da7-460e-bdd6-aabb54b48e41" />

<img width="2008" height="1160" alt="REQ-04_TC-08_10" src="https://github.com/user-attachments/assets/afad257d-63c4-4d35-9e5c-3cfa9a4c1be9" />

- Và hệ thống báo lỗi khi mượn sách thứ 5:

<img width="2008" height="1160" alt="REQ-04_TC-08_11" src="https://github.com/user-attachments/assets/5c2bc594-3184-4755-8c38-d790eff7c7e1" />

**Đề xuất xử lý:**
Cần chỉnh sửa điều kiện logic của `borrow_count` thay vì ≤3 thành <3.

---

## BUG-05

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-19` |
| **REQ liên quan** | `REQ-05` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Nguyễn Xuân Dương` |
| **Ngày phát hiện** | `18/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Hệ thống không hiển thị **cảnh báo quá hạn** khi trả sách quá hạn

**Môi trường:**
- Trình duyệt: Firefox
- Hệ điều hành: `Windows`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`Thành viên có phiếu mượn ban đầu ở trạng thái "Đang mượn" và quá hạn, sách quá hạn ở trạng thái "Đang mượn"`

**Bước tái hiện:**
1. `Vào mục "Mượn/Trả`
2. `Ấn nút "Trả sách" ở phiếu mượn của sách quá hạn đang ở đang ở trạng thái "Đang mượn"`
3. `Kiểm tra thông báo của hệ thống`

**Kết quả mong đợi:**
`Hệ thống hiển thị cảnh báo quá hạn`

**Kết quả thực tế:**
`Hệ thống chỉ hiển thị mỗi thông báo trả sách thành công`

**Tác động:**
- Vi phạm đến yêu cầu nghiệp vụ BO-02.

**Minh chứng**

<img width="1912" height="815" alt="REQ-05_baoquahan" src="https://github.com/user-attachments/assets/cbce76bc-3f7f-4c07-92a3-250f8b8cd726" />

**Đề xuất xử lý:**
Kiểm tra cảnh báo quá hạn đã được viết chưa và kiểm tra điều kiện hiển thị cảnh báo đúng chưa 


## BUG-06

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-04` |
| **REQ liên quan** | `REQ-07` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Cao Chí Bảo` |
| **Ngày phát hiện** | `19/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
`Hệ thống chấp nhận email sai format khi thêm thành viên`

**Môi trường:**
- Trình duyệt: Chrome `148`
- Hệ điều hành: `Windows 11`
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
`Đăng nhập tài khoản thủ thư, truy cập chức năng thêm thành viên`

**Bước tái hiện:**
1. `Truy cập hệ thống mượn sách https://stqa.rbc.vn/ và đăng nhập vào tài khoản thủ thư`
2. `Click icon "Thêm thành viên" ở góc phải`
3. `Nhập thông tin đầy đủ về Họ và tên và SĐT cùng email thiếu "@"`

**Kết quả mong đợi:**
`Hệ thống báo lỗi do email sai cú pháp`

**Kết quả thực tế:**
`Thêm thành viên thành công`

**Tác động:**
`Hệ thống bị lưu dữ liệu sai, gây lỗi khi gửi email thông báo mượn/trả sách sau này.`

**Minh chứng:**

![Alt text](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/REQ-07_TC04.png)

**Đề xuất xử lý:**
`Bổ sung/ kiểm tra lại hàm kiểm tra định dạng để chặn và báo lỗi ngay tại ô Email.` 
