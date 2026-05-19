# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `18/05/2026` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-04` |
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

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `TC-08` |
| **REQ liên quan** | `REQ-04` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Nguyễn Xuan Dương và Vũ Trần Nam Khánh` |
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

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-02` |
| **REQ liên quan** | `REQ-05` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Nguyễn Xuan Dương` |
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
- Vi phạm đến yêu phần mềm REQ-05.

**Minh chứng**

<img width="1918" height="800" alt="REQ-05_sachcosan" src="https://github.com/user-attachments/assets/fa5be162-c5ed-40f5-9821-415b5cdb812a" />

**Đề xuất xử lý:**
Kiểm tra cảnh báo quá hạn đã được viết chưa và kiểm tra điều kiện hiển thị cảnh báo đúng chưa 


<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
