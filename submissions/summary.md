# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | `STQA_Group_01` |
| **Lớp** | ICT Class 1 |
| **Ngày báo cáo** | 27/05/2026 |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Overall Test Results

| Metric | Value |
|--------|-------|
| Total test cases | 38 |
| Pass | 29 |
| Fail | 9 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass rate** | 73.68% |
| **Number of bugs found** | 9 |

### Functional Group Breakdown

| Functional Group | TC | Pass | Fail | Bug | Assessment |
|------------------|----|------|------|-----|------------|
| Login | 4 | 3 | 1 | 1 | Mostly stable, but email format validation is broken |
| Borrow / Return Core Actions | 3 | 3 | 0 | 0 | Stable |
| Search and Filter Books | 4 | 3 | 1 | 1 | Mostly stable, but category matching needs normalization |
| Borrowing Permission Rules | 6 | 4 | 2 | 2 | Needs attention; authorization and limit checks are incorrect |
| Return-book Behavior | 4 | 2 | 2 | 2 | Needs attention; overdue return feedback is incomplete |
| Overdue Handling | 7 | 7 | 0 | 0 | Stable |
| Add Member / Validation | 5 | 3 | 2 | 2 | Unstable; the add-member validation flow is broken |
| Borrow Record Visibility / Lookup | 4 | 3 | 1 | 1 | Critical privacy issue in record lookup |

### Bug Breakdown by Severity

| Severity | Quantity | Bug IDs |
|----------|----------|---------|
| High | 4 | BUG-04, BUG-07, BUG-08, BUG-09 |
| Medium | 5 | BUG-01, BUG-02, BUG-03, BUG-05, BUG-06 |
| Low | 0 | — |

---

## 3. Testing Techniques Used

| Technique | Applied to which REQ(s)? | Number of TCs used | How it was applied |
|----------|---------------------------|--------------------|-------------------|
| Black-box Testing | REQ-01 | 4 | Used for end-to-end login validation without checking internal implementation details. |
| Equivalence Partitioning (EP) | REQ-01, REQ-02, REQ-03, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | 29 | Used to split inputs into valid/invalid partitions such as existing vs. non-existing emails, available vs. borrowed books, member roles, and visible vs. hidden records. |
| Boundary Value Analysis (BVA) | REQ-04, REQ-06, REQ-07 | 4 | Used for boundary-focused scenarios such as the 3-book borrowing limit, due-date boundary at today, and email-format edge cases. |
| Decision Table Testing | REQ-02, REQ-04, REQ-07 | 4 | Used to verify outcome combinations based on role, member status, and book/record state. |
| State Transition Testing | REQ-02 | 1 | Used to verify that book status changes correctly from Available to Borrowed and back to Returned. |
| Input Validation | REQ-01 | 1 | Used to confirm that invalid email syntax is rejected during login. |

---

## 4. Software Quality Analysis

### 4.1. Strengths

- Core borrow and return operations work correctly in the normal flow.
- Overdue handling is the most stable part of the system: all overdue-related tests passed, including role-based visibility and date-boundary cases.
- Basic search by book title and author works well in most tested cases.
- Access control for the overdue-check button is correctly enforced for member accounts.
- Borrow record display is structurally complete for the librarian view.

### 4.2. Weaknesses

- Login accepts an invalid email format, which weakens data integrity and authentication validation.
- Category filtering is not fully robust because lowercase category input fails.
- Borrowing permission logic has two serious defects: suspended members receive the wrong rejection reason, and the 3-book borrowing limit is enforced incorrectly.
- The return flow for overdue books is incomplete because the overdue warning is missing.
- The add-member feature is unstable: one invalid email case is accepted, while a valid input case is rejected.
- Borrow record lookup has a major privacy flaw because a member can access another member’s records.

---

## 5. Recommended Bug Fix Priority

> Priority is based on severity, business impact, and risk to data/privacy.

| Order | Bug | Severity | Reason for Priority |
|------|-----|----------|--------------------|
| 1 | BUG-08 | High | Direct privacy and access-control violation; a member can view another member’s private borrow records. |
| 2 | BUG-04 | High | Core business rule is violated; the borrowing limit is enforced incorrectly and allows extra borrowing. |
| 3 | BUG-07 | High | The add-member feature’s main success path is broken, so the librarian cannot reliably create members. |
| 4 | BUG-09 | High | It violates the business rule: One member must not be able to manipulate the borrow records of another member, only the librarian can do it. |
| 5 | BUG-01 | Medium | Invalid login email is accepted, which harms data integrity and can propagate bad data across the system. |
| 6 | BUG-02 | Medium | Category filtering fails for lowercase input, causing avoidable search friction and false “no data” results. |
| 7 | BUG-03 | Medium | Wrong rejection message for suspended members reduces clarity and can confuse staff workflows. |
| 8 | BUG-05 | Medium | Overdue return feedback is incomplete; the system misses the required warning. |
| 9 | BUG-06 | Medium | Invalid email is accepted in add-member flow, which can corrupt member data and downstream notifications. |

---

## 6. Conclusion

The system is not ready for release. Although the overdue module and several core borrow/return flows are stable, there are still high-risk defects in access control, borrowing limits, and member management. The most critical issue is the privacy breach in borrow record lookup, followed by the incorrect borrow-limit enforcement and the broken add-member workflow. These defects affect both business rules and data integrity, so they should be fixed before any release decision is made.

---

## 7. Bài học rút ra (Tùy chọn)
1. It is important to have Testing techniques in the development of a software, such as: Input Validation Testing, Boundary Value Analysis, Access Control and Security Testing, Equivalence Partitioning.
2. We should not only test what would work, but also test what would not work (misused, invalid actions, unexpected behaviors).
3. Always verify correct error messages and user feedback: Test case sensitivity, localization, and search usability.
4. Developers should have high security awareness
  - Authentication flaws
  - Authorization flaws
  - Session handling
  - Basic injection vulnerabilities
5. It is important to focus on the System Requirements Specifications if we want our Testing process can be able to point out if the system is functioning correctly or not

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| | | |
