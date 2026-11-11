# BÀI TẬP CƠ BẢN JQUERY + REGEX

Yêu cầu chung: 
- Tạo một ô nhập (`<input>`), một nút **Kiểm tra** và một thẻ để in kết quả. 
- Khi bấm nút, đọc chuỗi trong ô nhập, kiểm tra bằng regex, rồi in ra **"ĐÚNG pattern"** hoặc **"SAI pattern"**. 
- Mỗi bài thử ít nhất 3 chuỗi đúng và 3 chuỗi sai.

Gợi ý jQuery dùng chung:
- `$("#btn").on("click", ...)` để bắt sự kiện bấm nút
- `$("#txt").val()` để đọc ô nhập
- `$("#result").text(...)` để in kết quả
- `pattern.test(chuỗi)` trả về `true` hoặc `false`

---

Bài 1. Chỉ gồm chữ số

Chuỗi chỉ gồm các chữ số 0–9, có ít nhất 1 chữ số.

- Đúng: `123`, `0`, `20260101`
- Sai: `12a`, `1 2`, `-5`, chuỗi rỗng

Gợi ý: một chữ số là `\d`; "một hoặc nhiều lần" là `+`; dùng `^` và `$` để chuỗi chỉ chứa chữ số.

---

Bài 2. Mã sinh viên

Đúng 10 chữ số.

- Đúng: `2051120001`
- Sai: `205112000` (9 số), `20511200011` (11 số), `20511200a1`

**Gợi ý:** lặp đúng n lần viết là `{n}`; nhớ neo `^` và `$`.

---

Bài 3. Tên đăng nhập

Dài 5–15 ký tự, chỉ gồm chữ thường a–z, chữ số và dấu gạch dưới `_`.

- Đúng: `tien_01`, `abcde`, `hello_world_26`
- Sai: `abcd` (ngắn), `hello_world_2026` (dài), `Tien01` (có chữ hoa), `tien-01`, `tien 01`

Gợi ý:tập ký tự cho phép đặt trong `[ ]`, ví dụ `[a-z]`; lặp từ n đến m lần viết là `{n,m}`.

---

Bài 4. Số điện thoại

Đúng 10 chữ số và bắt đầu bằng số 0.

- Đúng: `0912345678`, `0212345678`
- Sai: `912345678`, `09123456789`, `+84912345678`, `09123a5678`

Gợi ý: ký tự đầu là số `0` viết thẳng; phần còn lại là bao nhiêu chữ số thì dùng `\d{n}`.

---

Bài 5. Email đơn giản

Có dạng `tên@miền.đuôi`, không chứa khoảng trắng.

- Đúng: `a@b.com`, `tien.nguyen@mail.edu.vn`
- Sai: `a@b`, `@b.com`, `a b@c.com`, `abc.com`

Gợi ý: chia email làm 3 khối: trước `@`, dấu `@`, sau `@` (có một dấu chấm ở giữa). "Ký tự không phải khoảng trắng" là `\S`. Dấu chấm thật phải viết `\.`.

---

Bài 6. Mã lớp

2 chữ cái IN HOA, theo sau là 3 chữ số.

- Đúng: `IT101`, `CS999`
- Sai: `it101`, `IT10`, `IT1011`, `ITA01`

Gợi ý: chữ in hoa là `[A-Z]`; ghép hai khối liền nhau, mỗi khối lặp đúng số lần bằng `{n}`.

---

Bài 7. Ngày dạng dd/mm/yyyy (chỉ kiểm tra khuôn dạng)

Gồm 2 chữ số, dấu `/`, 2 chữ số, dấu `/`, 4 chữ số. Chưa cần kiểm tra ngày có thật hay không.

- Đúng: `14/10/2026`, `01/01/2000`
- Sai: `1/1/2026`, `14-10-2026`, `14/10/26`, `14/10/20266`

Gợi ý: dấu `/` trong regex dạng `/.../` phải viết thành `\/`.

---

Chú ý:

Nếu quên `^` và `$` thì chuỗi sai vẫn có thể báo ĐÚNG, vì regex chỉ cần tìm thấy một phần khớp.
