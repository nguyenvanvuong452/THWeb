# BÀI TẬP JQUERY + REGEX KẾT HỢP (15 BÀI)

**Cách làm chung:** mỗi bài dùng **jQuery** để bắt sự kiện, đọc và ghi nội dung trên trang, và dùng **Regex** để kiểm tra hoặc xử lý chuỗi. Với mỗi regex, tự thử ít nhất 3 chuỗi đúng và 3 chuỗi sai trước khi nộp. Có thể kiểm tra nhanh trong F12 → Console hoặc trên regex101.com (chọn JavaScript).

**Mức độ:** ⭐ dễ · ⭐⭐ vừa · ⭐⭐⭐ khá

---

## Bài 1 ⭐ Kiểm tra mã sinh viên khi đang gõ

**Đề bài:** Tạo ô nhập "Mã sinh viên" (đúng 10 chữ số). Khi người dùng gõ:
- Hợp lệ: viền xanh và hiện chữ xanh "✓ Hợp lệ".
- Sai: viền đỏ và hiện chữ đỏ "Mã SV gồm đúng 10 chữ số".
- Ô trống: không hiện gì.

**Gợi ý:** dùng sự kiện `input`; regex cần neo `^` `$`; đổi giao diện bằng `addClass` / `removeClass` hoặc `toggleClass`.

---

## Bài 2 ⭐ Ô chỉ cho nhập số

**Đề bài:** Ô "Số lượng": ký tự không phải chữ số bị xóa ngay khi gõ hoặc dán (dán `1a2b3` thì còn `123`). Bên dưới hiển thị "Đã loại bỏ X ký tự không hợp lệ" nếu có ký tự bị xóa.

**Gợi ý:** dùng `replace` với `\D` và cờ `g`; gán lại giá trị bằng `.val(...)`; số ký tự bị xóa là độ dài cũ trừ độ dài mới.

---

## Bài 3 ⭐ Kiểm tra số điện thoại và email khi rời ô

**Đề bài:** Form có hai ô: Số điện thoại và Email. Khi rời khỏi ô, kiểm tra và báo lỗi ngay bên dưới ô đó. Nút "Gửi" chỉ bật khi cả hai ô hợp lệ.
- SĐT: bắt đầu bằng `0` hoặc `+84`, tiếp theo là đầu số 3, 5, 7, 8 hoặc 9, rồi 8 chữ số.
- Email: dạng `tên@miền.đuôi`, tên miền có thể nhiều cấp (ví dụ `mail.edu.vn`).

**Gợi ý:** sự kiện `blur`; lựa chọn "hoặc" dùng `|` trong nhóm `( )`; dấu `+` và `.` thật phải thoát bằng `\`; bật/tắt nút bằng `.prop("disabled", ...)`.

---

## Bài 4 ⭐ Chuẩn hóa họ tên khi rời ô

**Đề bài:** Ô "Họ tên": khi rời ô, tự bỏ khoảng trắng thừa ở đầu, cuối và giữa các từ, rồi viết hoa chữ cái đầu mỗi từ.
Ví dụ: `"  nguyễn   văn    tiến  "` → `"Nguyễn Văn Tiến"`; `"TRẦN thị bình"` → `"Trần Thị Bình"`.

**Gợi ý:** đưa về chữ thường trước; gộp khoảng trắng bằng `\s+`; `trim()` hai đầu; để viết hoa chữ đầu mỗi từ, `replace` có thể nhận một hàm; chữ cái tiếng Việt có dấu dùng `\p{Ll}` kèm cờ `u`.

---

## Bài 5 ⭐⭐ Định dạng tiền khi gõ và tính tổng

**Đề bài:** Có hai ô "Tiền sách" và "Phí ship". Khi gõ, số tự có dấu chấm ngăn cách hàng nghìn (`1234567` → `1.234.567`). Dòng "Tổng cộng" bên dưới tự cộng hai ô và cũng hiển thị có dấu chấm.

**Gợi ý:** làm hai bước: (1) bỏ ký tự không phải số; (2) chèn dấu chấm vào các vị trí cách nhau 3 chữ số tính từ cuối (tra cứu `\B` và lookahead `(?=...)`). Khi cộng phải bỏ dấu chấm trước rồi mới đổi sang số.

---

## Bài 6 ⭐⭐ Tự định dạng số điện thoại khi gõ

**Đề bài:** Khi gõ số điện thoại, tự chia nhóm dạng `0912 345 678`, tối đa 10 số. Khi đủ 10 số và đầu số hợp lệ (03, 05, 07, 08, 09) thì viền xanh; đủ 10 số mà sai thì viền đỏ.

**Gợi ý:** lấy riêng chữ số bằng `\D`; dùng `slice` để giới hạn độ dài; chia nhóm 4-3-3 bằng ba nhóm bắt `( )`, các nhóm sau cho phép không bắt buộc (`?`) để vẫn chạy khi mới gõ được vài số; khi kiểm tra phải bỏ dấu cách.

---

## Bài 7 ⭐⭐ Ô ngày dd/mm/yyyy tự thêm `/` và kiểm tra ngày có thật

**Đề bài:** Ô "Ngày sinh": chỉ gõ số, hệ thống tự thêm dấu `/` (`14102026` → `14/10/2026`). Khi đủ 10 ký tự, báo ngày hợp lệ hay không: đúng khuôn dạng (ngày 01–31, tháng 01–12) và ngày phải thật sự tồn tại (`29/02/2026` và `31/04/2026` sai, `29/02/2024` đúng).

**Gợi ý:** phần tự thêm `/` làm tương tự bài 6; regex chỉ kiểm tra được khuôn dạng, không biết tháng có bao nhiêu ngày; để kiểm tra ngày có thật, dùng thêm đối tượng `Date` rồi so sánh ngược lại ngày, tháng, năm.

---

## Bài 8 ⭐⭐ Thanh đo độ mạnh mật khẩu

**Đề bài:** Ô mật khẩu có danh sách 5 tiêu chí, tiêu chí nào đạt thì đổi từ ❌ sang ✅: ít nhất 8 ký tự; có chữ thường; có chữ hoa; có chữ số; có ký tự đặc biệt. Bên dưới là thanh tiến độ theo số tiêu chí đạt, đổi màu: từ 2 tiêu chí trở xuống là đỏ "Yếu", 3–4 là cam "Trung bình", 5 là xanh "Mạnh". Thêm nút 👁 để hiện/ẩn mật khẩu.

**Gợi ý:** mỗi tiêu chí dùng một regex nhỏ, gom thành một mảng rồi duyệt bằng vòng lặp; độ rộng thanh tính theo phần trăm; nút hiện/ẩn đổi thuộc tính `type` giữa `password` và `text`.

---

## Bài 9 ⭐⭐ Tô sáng từ khóa trong đoạn văn

**Đề bài:** Có một đoạn văn bản và một ô tìm kiếm. Gõ từ khóa thì mọi vị trí xuất hiện được tô sáng bằng thẻ `<mark>` (không phân biệt hoa thường) và hiện "Tìm thấy N kết quả". Chương trình phải chạy đúng cả khi từ khóa có ký tự đặc biệt như `a+b`, `(x)`, `c++`.

**Gợi ý:** giữ nguyên đoạn văn gốc trong một biến và mỗi lần gõ vẽ lại từ bản gốc; tạo regex từ chuỗi bằng `new RegExp(chuỗi, "gi")`; ký tự đặc biệt của regex phải được thoát (thêm `\` phía trước) trước khi đưa vào `new RegExp`; dùng nhóm bắt để giữ nguyên chữ hoa/thường gốc khi thay.

---

## Bài 10 ⭐⭐ Trích xuất email, số điện thoại, hashtag từ văn bản

**Đề bài:** Một ô văn bản (`<textarea>`) cho dán đoạn văn bất kỳ. Bấm "Trích xuất" thì hiển thị ba danh sách riêng: Email, Số điện thoại, Hashtag, mỗi danh sách kèm số lượng. Kết quả trùng lặp chỉ hiện một lần.

Văn bản mẫu: `Liên hệ a.b@mail.com, c_d@x.edu.vn hoặc 0912 345 678, +84 987654321. #jQuery #Regex_2026`

**Gợi ý:** lấy tất cả kết quả khớp bằng `match` với cờ `g`; `match` có thể trả về `null` nên cần xử lý; loại trùng bằng `Set`; hashtag có chữ tiếng Việt thì dùng `\p{L}` kèm cờ `u`; số điện thoại có thể có dấu cách, dấu chấm hoặc gạch ngang giữa các nhóm.

---

## Bài 11 ⭐⭐ Lọc bảng bằng Regex

**Đề bài:** Bảng sinh viên gồm mã, họ tên, lớp, email (ít nhất 5 dòng). Ô tìm kiếm có checkbox "Dùng Regex":
- Không tick: tìm văn bản thường, không phân biệt hoa thường.
- Tick: coi nội dung ô nhập là regex (ví dụ `^SV00[1-3]`, `CNTT\d`).
- Regex nhập sai (ví dụ `(abc`): hiện cảnh báo đỏ "Regex không hợp lệ", trang không bị lỗi.

**Gợi ý:** tạo regex trong khối `try ... catch`; duyệt từng dòng bằng `.each()`; ẩn/hiện bằng `.toggle(true/false)`; gắn cùng một hàm lọc cho ô nhập và checkbox.

---

## Bài 12 ⭐⭐⭐ Che thông tin nhạy cảm

**Đề bài:** Một ô văn bản chứa nội dung từ khách hàng. Nút "Ẩn thông tin" sẽ thay:
- Email `tien.nguyen@gmail.com` → `t***@gmail.com`
- SĐT `0912345678` → `091****678`

Nút chuyển thành "Hiện lại", bấm lại thì khôi phục văn bản gốc. Chuỗi 11 chữ số như `20511200011` (mã sinh viên) không được bị đổi.

**Gợi ý:** dùng nhóm bắt `( )` rồi tham chiếu lại bằng `$1`, `$2` trong chuỗi thay thế; để chỉ đổi dãy đúng 10 số, kiểm tra phía trước và phía sau không phải chữ số (tra cứu `(?<!...)` và `(?!...)`); lưu văn bản gốc bằng `.data()` hoặc một biến.

---

## Bài 13 ⭐⭐⭐ Tạo slug từ tiêu đề tiếng Việt

**Đề bài:** Ô "Tiêu đề bài viết". Khi gõ, dòng "Slug" bên dưới tự cập nhật, kèm nút "Sao chép".
Ví dụ: `"Lập Trình jQuery & Regex cho Người Mới Đầu!!  "` → `lap-trinh-jquery-regex-cho-nguoi-moi-dau`

**Gợi ý:** bỏ dấu tiếng Việt bằng `normalize("NFD")` rồi xóa các dấu rời trong dải Unicode `̀`–`ͯ`; chữ `đ` / `Đ` phải xử lý riêng; thay mọi đoạn ký tự không phải chữ hoặc số bằng một dấu `-` (dấu `+` giúp không bị `--`); cuối cùng cắt dấu `-` thừa ở hai đầu.

---

## Bài 14 ⭐⭐⭐ Phân tích đơn hàng dạng văn bản thành bảng

**Đề bài:** Người dùng dán đơn hàng, mỗi dòng theo dạng `Tên sách x số lượng - giá`:

```
Đắc Nhân Tâm x 2 - 120.000đ
Nhà Giả Kim x1 - 89.000đ
dòng lỗi này
Tư Duy Nhanh và Chậm x 3 - 150.000đ
```

Bấm "Phân tích" thì dựng bảng gồm STT, Tên, SL, Đơn giá, Thành tiền, cuối bảng có dòng Tổng cộng (có dấu chấm ngăn cách). Dòng sai định dạng được liệt kê riêng, kèm số dòng.

**Gợi ý:** tách từng dòng bằng `split("\n")`; viết regex theo ba khối (tên, số lượng, giá) bằng các nhóm bắt rồi dùng `exec` để lấy từng nhóm; phần tên nên dùng dạng "lười" `.+?`; đổi giá `120.000` sang số bằng cách bỏ dấu chấm; dòng không khớp thì `exec` trả về `null`.

---

## Bài 15 ⭐⭐⭐ Form đăng ký tổng hợp

**Đề bài:** Form có 6 ô: Mã SV, Họ tên, Email, Số điện thoại, Mật khẩu, Nhập lại mật khẩu.
- Mã SV: chỉ giữ chữ số, đúng 10 số (bài 1, 2).
- Họ tên: tự chuẩn hóa khi rời ô (bài 4).
- Số điện thoại: tự chia nhóm khi gõ, kiểm tra đầu số (bài 6).
- Email: kiểm tra khi gõ hoặc rời ô (bài 3).
- Mật khẩu: có thanh độ mạnh, bắt buộc đủ 5 tiêu chí (bài 8).
- Nhập lại mật khẩu: phải trùng; đổi mật khẩu gốc thì kiểm tra lại ô này.
- Lỗi hiện ngay dưới từng ô; nút "Đăng ký" chỉ bật khi cả 6 ô hợp lệ.
- Bấm "Đăng ký" thì hiển thị thông báo thành công kèm họ tên và xóa form.

**Gợi ý:** gom luật của từng ô vào một object (mỗi ô có hàm kiểm tra và thông báo lỗi), viết một hàm kiểm tra một ô và một hàm kiểm tra cả form để bật/tắt nút; gắn sự kiện chung cho mọi ô bằng event delegation (`$("form").on("input", "input", ...)`) thay vì viết lặp sáu lần.

---

## Nhắc chung

- Regex kiểm tra toàn bộ chuỗi thì cần `^` ở đầu và `$` ở cuối.
- Dùng `prop` (không dùng `attr`) cho `disabled` và `checked`.
- Phần tử được thêm vào trang sau khi tải xong cần event delegation mới nhận được sự kiện.
