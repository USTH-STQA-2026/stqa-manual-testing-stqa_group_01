# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `STQA_Group_01` |
| **Ngày tạo** | `16/05/2026` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## IDM — Login (REQ-01)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Does the email exist in the DB? | Yes | `librarian@library.com` | Login successful |
| | No | `noone@email.com` | Error message |
| Is the password correct? | Correct | `admin123` | Login successful |
| | Incorrect | `wrongpass` | Error message |
| Is the input field empty? | Not empty | (any value) | Process normally |
| | Empty | `""` | Display "Please enter..." |

## IDM — REQ-02: Book Borrowing, Returning & Display

| Characteristic | Block | Representative Value | Expected Result |
|----------------|-------|----------------------|-----------------|
| Book status? | Available | BOOK001 (Lập trình Flutter cơ bản) | Borrow button "+" displayed, can borrow |
| | Borrowed | BOOK013 (Quản trị nhân sự hiện đại) | Displays "Borrowed", "+" button hidden for others, return button shown for borrower |
| | Lost | BOOK007 (Kinh tế vi mô) | Displays "Lost", cannot borrow |
| Member status? | Active | MEM002 (Nguyễn Học Bá) | Allowed to borrow |
| | Suspended | MEM004 (Lê Cần Cù) | Rejected, error notification |
| | Expired | MEM005 (Phạm Trung Bình) | Rejected, error notification |
| Return action | On time | MEM002 presses return button on BOOK013 | Displays "Returned", status changes to "Available", "+" button reappears |
| | Overdue | MEM001 (Librarian) presses return button on overdue book | Displays "Returned", status changes to "Available" |
| Borrowing info visibility | Member view | MEM002 borrows BOOK001 | Member sees only their own borrowed books |
| | Librarian view | MEM001 (Librarian) checks borrowed list | Librarian sees all borrowed books |
| Book information display | Complete info | BOOK001 — Nguyễn Minh Đức • Technology • 2023 | Author name, category, publication year, book ID all displayed correctly below title |
| Book status display | Available | BOOK008 (Computer Networks) | System displays "Available" correctly |
| | Borrowed | BOOK013 (Quản trị nhân sự hiện đại) | System displays "Borrowed" correctly |
| | Lost | BOOK020 (Introduction to Linguistics) | System displays "Lost" correctly |

## IDM — Book Search (REQ-03)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Does the keyword exist in the DB? | Yes (book title) | `"Flutter"` | Display books containing "Flutter" |
| | Yes (author name) | `"Nguyễn"` | Display books by the author Nguyễn |
| | No | `"XYZ123"` | Empty list |
| Case-sensitive? | Lowercase | `"flutter"` | Same result as "Flutter" |
| | Uppercase | `"FLUTTER"` | Same result as "Flutter" |

## IDM — Borrow Books (REQ-04, REQ-05)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Book status? | Available | BOOK001 | Allow borrowing |
| | Borrowed | BOOK003 | Do not allow |
| | Lost | BOOK007 | Do not allow |
| Member status? | Active | MEM002 | Allow borrowing |
| | Suspended | MEM004 | Reject, error message |
| | Expired | MEM005 | Reject, error message |
| Number of books currently borrowed? | < 3 (BVA: 0, 1, 2) | MEM006 (0 books) | Allow borrowing |
| | = 3 (BVA: limit) | MEM has already borrowed 3 books | Reject, report limit exceeded |

## IDM — Return Books (REQ-05)
| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Book status? | Borrowed | BOOK013 | Allow returning the book |
| | Returned | BOOK005 | Book changes to "Available" status |
| Is the book overdue? | Overdue | BOOK003 | Display **overdue warning** when returning |
| | Not overdue | BOOK013 | Do not display **overdue warning** when returning |

## IDM — Overdue Book Handling (REQ-06)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| User role? | Librarian | `librarian@library.com` | Sees the "Check overdue" button and can click it |
| | Member | `ba.nguyen@email.com` | Does not see the "Check overdue" button |
| Borrowing slip status? | Borrowed, dueDate ≤ today | BR001 (due 15/09/2024) | Marked as "Overdue" after clicking the button |
| | Borrowed, dueDate > today | Newly created slip today | Remains "Borrowed" |
| | Returned, dueDate ≤ today | BR002, BR005 | Remains "Returned", not changed to "Overdue" |
| Visibility scope for Member? | Own slip | BR001 (owned by MEM002) | Sees own overdue slips |
| | Another member’s slip | BR003 (owned by MEM006) | Does not see another member’s slip |

## IDM — Add Member (REQ-07)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| **Full name** | 1. Text entered (Valid) | Nguyễn Văn A | Added successfully |
| | 2. Left blank (Invalid) | *(Blank)* | Show missing full name error |
| **Email** | 1. Valid format | `legit@gmail.com` | Added successfully |
| | 2. Missing `@` | `haivuemail.com` | Show invalid format error |
| | 3. Missing `.` in domain | `trandat@emailcom` | Show invalid format error |

## IDM — `<!-- Self-added group for REQ-05 to REQ-08 -->`

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| `<!-- Self-filled group -->` | | | |

## IDM — Borrow Record Lookup (REQ-08)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role accessing records? | Librarian | `librarian@library.com` | Sees ALL borrow records (BR001–BR005) across all members |
| | Member | `ba.nguyen@email.com` | Sees ONLY own borrow records |
| Member ID entered in lookup field? | Own ID | `MEM002` (logged-in user's own ID) | Records of MEM002 are displayed |
| | Another member's ID | `MEM006` (belongs to biet.hoang) | No records shown — access denied |
| | Non-existent ID | `MEM999` | No records found (empty result or error message) |
| Record information completeness? | All required fields present | BR001 | Record ID, book title, borrow date, due date, status all visible |
| Status value displayed? | Active borrow | BR001, BR003 | Status = "Đang mượn" |
| | Returned on time | BR002, BR004 | Status = "Đã trả" |
| | Returned late | BR005 | Status = "Đã trả" |
| | Overdue (after Librarian check) | BR001 (post Check Overdue) | Status = "Quá hạn" |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| TC Code | Test Objective | Preconditions | Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-01 | Check that the user can log in successfully with a valid email and password | The user already has an account in the system and is on the login page | 1. Enter a valid email in the "Email" field. 2. Enter the correct password in the "Password" field. 3. Click the "Login" button | Username: `ba.nguyen@email.com`, password: `password123` | The system logs in successfully and navigates to the home page. The user name and role are displayed | REQ-01 | Black-box Testing |
| TC-02 | Check that the system displays an error when the email does not exist | The user is on the login page | 1. Enter a non-existent email in the "Email" field. 2. Enter any password. 3. Click the "Login" button | Username: `random@email.com`, password: `123`| The system displays "Member not found" | REQ-01 | Black-box Testing, EP |
| TC-03 | Check that the system displays an error when the password is incorrect | The user already has an account in the system and is on the login page | 1. Enter a valid email in the "Email" field. 2. Enter the wrong password in the "Password" field. 3. Click the "Login" button | Username: `ba.nguyen@email.com`, password: `hello` (incorrect password) | The system displays "Incorrect password" | REQ-01 | Black-box Testing, EP |
| TC-04 | Check that the system rejects login when the email format is invalid | The user is on the login page and already has an account in the system (but the email format is invalid) | 1. Enter an invalid email format (but one that exists in the system) in the "Email" field (for example: `example@email`). 2. Enter the correct password in the "Password" field. 3. Click the "Login" button | Username: `example@email`, password: `password123` | The system rejects the login and shows the error "Invalid email format" | REQ-01 | Black-box Testing, Input Validation |
| TC-05 | Verify that the book list is displayed for both Librarian and Member roles | The user has a valid account and is logged in as either Librarian or Member | 1. Log in to the system. <br> 2. Open the "Books" section. <br> 3. Observe the displayed book list. | Any valid Librarian or Member account | The system displays the full book list successfully for both roles | REQ-02 | EP |
| TC-06 | Verify that each book displays complete information | The user is logged in and is viewing the book list | 1. Open the "Books" section. <br> 2. Observe the information shown for each book card/row. | Any book in the list | Each book displays its title, author, category, publication year, and status | REQ-02 | EP |
| TC-07 | Verify that the correct book status is displayed | The user is logged in and is viewing the book list | 1. Open the "Books" section. <br> 2. Check the status shown for books with different states. | Books in different statuses | The system displays the correct status for each book, such as "Available", "Borrowed", or "Lost" | REQ-02 | EP |
|TC-08| Check the function '"Search by Book Title, Author Name"' and handle cases where there is no matching data.| Successfully log in to the system and are in the `'Books'` section| Step 1. Click on the search bar. <br>2. Enter an author name and confirm the filter. <br>3. Clear the search bar, then enter a specific book title. <br>4. Clear the search bar, then enter a non-existent character string.| `"Nguyễn Minh Đức"`, `"Lập trình Flutter cơ bản"` and `"ABCxyz123"`| After step 2, the book with code `BOOK001` (Lập trình Flutter cơ bản) and `BOOK009` (Nhập môn lập trình Python) will be displayed. <br>After step 3, only 1 book with code `BOOK001` (Lập trình Flutter cơ bản) is displayed. <br>After step 4, the exact string `"No books found."` will be displayed| REQ-03 | EP |
|TC-09| Check case-insensitivity when searching for books.| Successfully log in to the system and are in the `'Books'` section| Step 1. Click on the search bar. <br>2. Enter input string 1. <br>3. Check the displayed list. <br>4. Clear all characters in the search bar. <br>5. Enter input string 2. <br>6. Check the displayed list.|1. `"nGuyễn mInh ĐứC"` and 2. `"lẬp trìnH flUTTer cơ bẢn"`|After step 3, the system filters and displays exactly 2 books by the author: code `'BOOK001'` (Lập trình Flutter cơ bản) and `'BOOK009'` (Nhập môn lập trình Python), while other books are hidden. <br>After step 6, the system filters and displays only 1 book: code `'BOOK001'` (Lập trình Flutter cơ bản).|REQ-03 |EP Testing|
|TC-10|Check the feature for filtering the list by category with valid and invalid cases.|Successfully log in to the system and are in the `'Books'` section|Step 1. Click on the `"Filter by category"` bar. <br>2. Enter the exact name of a valid category. <br>3. Check the displayed list. <br>4. Clear the category filter. <br>5. Enter a category that does not exist in the system.|`"Công nghệ"` and `"Khoa học ảo tưởng"`|After step 3, only 8 books in the "Technology" category are displayed (Book codes `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`). Any books in other categories (such as `'Kinh tế'`, `'Văn học'`, etc.) are hidden from the screen. <br>After step 5, the entire list disappears, and the exact string `"No books found"` is displayed.|REQ-03|EP Testing|
|TC-11| Check case-insensitivity of the category filtering feature.|Successfully log in to the system and are in the `'Books'` section| Step 1. Click on the `"Filter by category"` input field. <br>2. Enter the category name entirely in lowercase. <br>3. Click outside or press Enter to activate the filter. <br>4. Check the change in the displayed book list.|`"công nghệ"`|The system recognizes the filter as case-insensitive and keeps displaying exactly the 8 books in the `"Technology"` category, the same as when entering the standard uppercase text (Book codes `'BOOK001'`, `'BOOK002'`, `'BOOK003'`, `'BOOK005'`, `'BOOK008'`, `'BOOK009'`, `'BOOK010'`, `'BOOK011'`).|REQ-03| EP Testing|
| TC-12 | Check borrowing permission for a suspended member | The member is suspended, and the book is in the "Available" status | 1. Log in with the suspended account 2. Borrow any available book | Suspended account (MEM004) | The member is not allowed to borrow books and the correct rejection reason is displayed | REQ-04 | EP |
| TC-13 | Check borrowing permission for an expired member | The member is expired, and the book is in the "Available" status | 1. Log in with the expired account 2. Borrow any available book | Expired account (MEM005) | The member is not allowed to borrow books and the correct rejection reason is displayed | REQ-04 | EP |
| TC-14 | Check borrowing permission for an active member | The member is active, and the book is in the "Available" status | 1. Log in with the active account 2. Borrow any available book | Active account (MEM006) | The member is allowed to borrow books and the borrowing success message is displayed | REQ-04 | EP |
| TC-15 | Borrow an already borrowed book | The member is active, and the book is in the "Borrowed" status | 1. Log in with the active account 2. Find a book in the "Borrowed" status and try to borrow it | Active account (MEM006) | The member is not allowed to borrow the book | REQ-04 | EP |
| TC-16 | Borrow books over the limit | The member is active, and the book is in the "Available" status | 1. Log in with the active account 2. Borrow 1, 2, 3, 4 books in the "Available" status | Active account (MEM006) | The member cannot borrow more books when over the limit and the correct rejection reason is displayed | REQ-04 | EP, BVA | 
| TC-17 | Successfully borrow books | The member is active, the book is in the "Available" status, and the number of books borrowed is below the limit | 1. Log in with the active account 2. Borrow 1/2/3 books in the "Available" status | Active account (MEM006) | The member borrows books successfully and the due date is 14 days from the borrowing date | REQ-04 | EP, Decision Table |
| TC-18 | Return a borrowed book | The book is in the "Borrowed" status | 1. Go to the "Borrow/Return" section 2. Click the "Return book" button of the borrowing slip in the "Borrowed" status 3. Go back to the "Books" section and check the status of the returned book | Member with the original borrowing slip for book BOOK013 | The book returns to the "Available" status | REQ-05 | EP |
| TC-19 | Display **overdue warning** | The overdue book is in the "Borrowed" status | 1. Go to the "Borrow/Return" section 2. Click the "Return book" button of the borrowing slip in the "Borrowed" and overdue status | Member with the original borrowing slip for overdue book BOOK003 | The system displays an **overdue warning** | REQ-05 | EP |
| TC-20 | Check the status of a returned book | The book is in the "Returned" status | 1. Go to the "Borrow/Return" section 2. Find the borrowing slip in the "Returned" status 3. Go back to the "Books" section and check the returned book status | Member with the original borrowing slip for returned book BOOK005 | The book is in the "Available" status | REQ-05 | EP |
| TC-21 | Check the ability to return other members' books | The book is in the "Borrowed" status, Member with the original borrowing slip for book BOOK013 | 1. Go to the "Borrow/Return" section 2. Click on the "Search borrowing slips" 3. Enter "MEM006" in the search bar 4. Click the "Return book" button of the borrowing slip in the "Borrowed" status | An active member | Must not be able to return the book | REQ-05 | EP |
| TC-22 | Check that when the librarian clicks "Check overdue", overdue borrowing slips are correctly marked | Log in with the Librarian account (`librarian@library.com` / `admin123`). Initial data state. | **Step 1:** Go to the "Borrow / Return" tab.<br>**Step 2:** Click the "Check overdue" button.<br>**Step 3:** Observe the status of BR001 (dueDate: 15/09/2024) and BR003 (dueDate: 15/10/2024) | BR001 (MEM002 + BOOK003, due 15/09/2024); BR003 (MEM006 + BOOK013, due 15/10/2024) | BR001 and BR003 change from "Borrowed" to "Overdue" (both have dueDate ≤ 18/05/2026) | REQ-06 | EP |
| TC-23 | Check that returned slips are NOT marked as "Overdue" after clicking "Check overdue" | Log in as Librarian. Initial data state. | **Step 1:** Go to the "Borrow / Return" tab.<br> **Step 2:** Click the "Check overdue" button.<br> **Step 3:** Observe the status of BR002 (Returned on time) and BR005 (Returned but 5 days late) | BR002 (Trần Dựa Dẫm + BOOK001, returned 20/08/2024); BR004 (Nguyễn Học Bá + BOOK005, returned 10/07/2024); BR005 (Trần Dựa Dẫm + BOOK006, returned 20/06/2024 — late) | BR002, BR004, and BR005 remain "Returned" (not changed to "Overdue" even though the return date is after dueDate) | REQ-06 | EP|
| TC-24 | Check that a Member does not see the "Check overdue" button (access control) | Log in with the Member account (`ba.nguyen@email.com` / `password123`). | **Step 1:** Log in with the Member account.<br> **Step 2:** Go to the "Borrow / Return" tab.<br> **Step 3:** Observe the interface and look for the "Check overdue" button | Account: `ba.nguyen@email.com` / `password123` (role: Member) | The **"Check overdue" button does not appear** in the Member interface | REQ-06 | EP  |
| TC-25 | Check that a Member can only see their own overdue slips, not others' | Preparation: Log in as Librarian → click "Check overdue" → log out. Then log in as MEM002. | **Step 1:** Log in as Librarian, click "Check overdue", log out.<br> **Step 2:** Log in as `ba.nguyen@email.com` / `password123`.<br> **Step 3:** Go to the "Borrow / Return" tab.<br> **Step 4:** Observe the entire list of overdue slips displayed | MEM002 (ba.nguyen): has BR001 (overdue). MEM006 (biet.hoang): has BR003 (overdue) | MEM002 **only sees BR001** of their own. **BR003** belonging to MEM006 is **not visible** | REQ-06 | EP  |
| TC-26 | Check due-date boundary: a slip with `dueDate` equal to the current date is marked "Overdue" | Log in as a Member, create 1 borrowing slip, and simulate dueDate = today. Then log out and log in as Librarian (`librarian@library.com` / `admin123`). | **Step 1:** Go to the "Borrow / Return" tab.<br>**Step 2:** Click the "Check overdue" button.<br>**Step 3:** Observe the status of the borrowing slip whose due date is today. | Borrowing slip in "Borrowed" status with dueDate exactly matching the current date | The borrowing slip changes from "Borrowed" to "Overdue" | REQ-06 | BVA |
| TC-27 | Check that a slip not yet due (dueDate > current date) is NOT marked "Overdue" | Log in as a Member, borrow 1 new book (the default due date will be today + 14 days). Then log out and log in as Librarian. | **Step 1:** Go to the "Borrow / Return" tab.<br>**Step 2:** Click the "Check overdue" button.<br>**Step 3:** Observe the status of the newly created borrowing slip. | Newly created borrowing slip with dueDate > current date | The borrowing slip remains in the "Borrowed" status (not changed to "Overdue") | REQ-06 | EP |
| TC-28 | Check the default status of overdue slips BEFORE clicking "Check overdue" | Log in as Librarian. Initial data state (make sure the "Check overdue" button has NOT been clicked). | **Step 1:** Go to the "Borrow / Return" tab.<br>**Step 2:** Directly observe the status of BR001 and BR003 immediately upon entering the page. | BR001 (MEM002 + BOOK003, due 15/09/2024); BR003 (MEM006 + BOOK013, due 15/10/2024) | BR001 and BR003 still show the default status "Borrowed" (proving the system does not change automatically without Librarian action) | REQ-06 | EP |
|TC-29|Check permission to add members for a non-librarian account|Logged in as a member account|Check whether the "Add member" icon appears in the top-right corner|Login: ba.nguyen@email.com, Password: password123|The "Add member" icon does not appear|REQ-07|Decision Table (Authorization) |
| TC-30 | Check whether the system shows an error when the "Full name" field is missing | Logged in as Librarian, on the Add Member form. | Enter a valid email and phone number, leave Full name blank. Click "Add". | Email: noname@email.com, Phone: 0123456791 | The system rejects the account creation and displays an error message about the missing Full name. | REQ-07 | Decision Table (missing name)|
| TC-31 | Check whether the system blocks emails missing @ | Logged in as Librarian, on the Add Member form. | Enter a valid Full name and phone number. Enter an email containing "." but missing "@". Click "Add". | Full name: Vũ Hải, Email: haivuemail.com, Phone: 0133456798 | The system rejects the account creation and displays an invalid email format error message. | REQ-07 | EP / BVA |
| TC-32 | Check whether the system blocks emails missing a . in the domain | Logged in as Librarian, on the Add Member form. | Enter a valid Full name and phone number. Enter an email with "@" but missing "." after it. Click "Add". | Full name: Trần Đạt, Email: trandat@emailcom, Phone: 0123456798 | The system rejects the account creation and displays an invalid email format error message. | REQ-07 | EP / BVA |
| TC-33 | Check the normal operation of the feature | Logged in as Librarian, on the Add Member form. | Enter Full name, Email, and Phone number. Click "Add". | Full name: Lê Gít, Email: legit@email.com, Phone: 0234567891 | The system adds the member successfully. | REQ-07 | EP |
| TC-34 | Verify Librarian can view all borrow records across all members | Logged in as Librarian (`librarian@library.com` / `admin123`). Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Observe the full borrow record list.<br>**Step 3:** Verify BR001 (MEM002), BR002 (MEM003), BR003 (MEM006), BR004 (MEM002), BR005 (MEM003) are all listed. | All 5 seed records: BR001–BR005 | All 5 records are visible to the Librarian with correct member names, book titles, dates, and statuses | REQ-08 | EP |
| TC-35 | Verify Member MEM002 sees only their own records in the default "my records" view | Logged in as MEM002 (`ba.nguyen@email.com` / `password123`). Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Observe the borrow record list shown by default (without entering any search ID).<br>**Step 3:** Check which records are displayed. | MEM002 owns: BR001 (BOOK003 — "Đang mượn"), BR004 (BOOK005 — "Đã trả") | Only **BR001** and **BR004** are displayed. BR002, BR003, BR005 (belonging to other members) are **not visible**. | REQ-08 | EP |
| TC-36 | Verify Member cannot view another member's records using the "lookup by member ID" feature | Logged in as MEM002 (`ba.nguyen@email.com` / `password123`). Initial seed data. | **Step 1** Go to "Mượn / Trả" tab.<br>**Step 2:** Locate the "Tra cứu phiếu mượn" (lookup) search field.<br>**Step 3:** Enter `MEM006` (belonging to biet.hoang).<br>**Step 4:** Observe the result. | Lookup input: `MEM006` (another member's ID) | System shows **no records** or displays an access-denied message. BR003 (MEM006's record) is **not shown** to MEM002. | REQ-08 | EP |
| TC-37 | Verify all required information fields are present in each borrow record | Logged in as Librarian. Initial seed data. | **Step 1:** Go to "Mượn / Trả" tab.<br>**Step 2:** Inspect any borrow record (e.g. BR001).<br>**Step 3:** Check that all 5 fields are visible: Record ID, Book title, Borrow date, Due date, Status. | BR001: MEM002, BOOK003, borrowed 01/09/2024, due 15/09/2024, status "Đang mượn" | Record displays all 5 required fields: **Record ID** (BR001), **Book** (Kiểm thử phần mềm nhập môn), **Borrow date** (01/09/2024), **Due date** (15/09/2024), **Status** ("Đang mượn") | REQ-08 | EP |
| TC-38 | Verify that book status is updated in real time | A book status has been changed in the system | 1. Open the "Books" section. <br> 2. Refresh or re-open the list if needed. <br> 3. Observe the updated status of the affected book. | A book whose status has just changed | The updated status is displayed immediately and correctly in the book list | REQ-02 | State Transition |


---


---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Login | 4 | REQ-01 | Black-box Testing, EP, Input Validation |
| Borrow/Return core actions | 4 | REQ-02 | EP, State Transition, Decision Table |
| Search and filter book | 4 | REQ-03 | EP |
| Borrowing permission rules | 6 | REQ-04 | EP, BVA, Decision Table |
| Return book behavior | 4 | REQ-05 | EP |
| Overdue handling | 7 | REQ-06 | EP, BVA |
| Add member/Validation | 5 | REQ-07 | EP, BVA, Decision Table |
| Borrow record visibility / Lookup | 4 | REQ-08 | EP |
| **Tổng** | 38 | 8 | Black-box Testing, EP, BVA, Input Validation, Decision Table, State Transition |
