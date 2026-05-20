# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

BUG-An

| Attribute | Details |
|-----------|---------|
| **Bug ID** | BUG-02 |
| **Related TC** | An10|
| **Related REQ** | REQ-08 |
| **Severity** | High |
| **Discovered by** | Huynh Gia An|
| **Date discovered** | 20/05/2026 |
| **Status** | Open |

**Title:**
Member can view another member's private borrow records by entering their Member ID in the "Tra cứu phiếu mượn" lookup field

**Environment:**
- Browser: Chrome (latest version)
- Operating System: Windows / MacOS / Linux
- Interface language: Vietnamese (default)

**Preconditions:**
- System is at initial seed data state
- Logged in as Member MEM002 (`ba.nguyen@email.com` / `password123`)

**Steps to Reproduce:**
1. Log in as Member MEM002 (`ba.nguyen@email.com` / `password123`)
2. Navigate to the **"Mượn / Trả"** tab
3. Locate the **"Tra cứu phiếu mượn"** (borrow record lookup) search field
4. Enter `MEM006` (the Member ID belonging to `biet.hoang@email.com`) into the search field
5. Observe the records returned

**Expected Result:**
The system returns **no records** or displays an access-denied / unauthorized message. MEM002 must not be able to view BR003 (Quản trị nhân sự hiện đại — belonging to MEM006). *(SRS REQ-08: "Member can only view their own borrow records. NOT allowed to view records of other members.")*

**Actual Result:**
BR003 (**Quản trị nhân sự hiện đại**, borrowed by `biet.hoang` / MEM006, due 15/10/2024, status "Đang mượn") is **fully displayed** to MEM002 — including book title, borrow date, due date, and status.

**Impact:**
Serious privacy and access control violation. Any Member can freely look up and read another member's borrowing history simply by knowing (or guessing) their Member ID. In a real-world deployment, this would constitute a data protection breach.

**Evidence:**
![AltText](https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_01/blob/main/screenshots/An10.png)

**Suggested Fix:**
When a Member submits a lookup query, the backend/controller must validate that the searched Member ID matches the currently logged-in user's ID. If it does not match, the system must return an empty result set or an access-denied message. This filter should be enforced server-side (or in the state management layer), not only on the UI.

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
