# Kiến thức nền tảng cho 20 bài tập JavaScript DOM (10 cơ bản + 10 nâng cao)


Tài liệu này liệt kê chi tiết các kiến thức cần giảng trước mỗi bài, để sinh viên hiểu bản chất trước khi code chứ không chỉ chép mẫu.

---

## Bài 1: Đổi màu chữ khi click nút

**Mục tiêu:** Sinh viên hiểu chu trình "chọn phần tử → gắn sự kiện → thay đổi thuộc tính".

### Kiến thức cần nắm

1. **DOM là gì (tổng quan mở đầu, chỉ dạy 1 lần ở bài này)**
   - DOM (Document Object Model) là cây các đối tượng đại diện cho HTML mà trình duyệt dựng lên.
   - JavaScript không "nhìn thấy" file HTML, nó thao tác trên cây DOM này.

2. **Cách chọn phần tử (Selecting Elements)**
   - `document.querySelector('selector')`: trả về **phần tử đầu tiên** khớp với CSS selector (`#id`, `.class`, `tag`).
   - `document.getElementById('id')`: trả về phần tử theo id, nhanh hơn nhưng chỉ dùng được với id.
   - So sánh 2 cách, khuyến khích dùng `querySelector` vì linh hoạt (dùng được mọi loại selector CSS).

3. **Sự kiện (Event) và lắng nghe sự kiện**
   - `element.addEventListener('click', callbackFunction)`: gắn một hàm sẽ chạy khi sự kiện `click` xảy ra.
   - Phân biệt: khai báo hàm callback dạng function thường vs arrow function.
   - Lưu ý: không gọi hàm `callbackFunction()` (có dấu ngoặc) khi gắn, vì sẽ chạy ngay lập tức thay vì chờ sự kiện.

4. **Thay đổi style bằng JS**
   - `element.style.propertyName = 'value'` — ví dụ `element.style.color = 'red'`.
   - Lưu ý cú pháp: thuộc tính CSS có dấu gạch ngang (`background-color`) chuyển thành camelCase trong JS (`backgroundColor`).

5. **Cấu trúc file cơ bản**
   - Đặt thẻ `<script>` trước `</body>` (hoặc dùng `defer`) để đảm bảo HTML đã load xong trước khi JS chạy — giải thích ngắn gọn lỗi thường gặp "Cannot read property of null" khi script chạy trước khi phần tử tồn tại.

---

## Bài 2: Ẩn/hiện phần tử

**Mục tiêu:** Hiểu cách JS thay đổi hiển thị của phần tử và khái niệm "trạng thái" (state) đơn giản qua thuộc tính CSS.

### Kiến thức cần nắm

1. **Các cách ẩn/hiện phần tử**
   - `element.style.display = 'none'` (ẩn hoàn toàn, không chiếm chỗ) vs `'block'`/`'inline'`/`'flex'` (hiện lại).
   - So sánh với `visibility: hidden` (ẩn nhưng vẫn chiếm chỗ) — nên nhắc qua để sinh viên phân biệt.

2. **classList và class CSS**
   - Cách tiếp cận "chuẩn" hơn: định nghĩa class `.hidden { display: none; }` trong CSS, rồi dùng JS toggle class thay vì set style trực tiếp.
   - `element.classList.add('className')`, `.remove('className')`, `.toggle('className')`, `.contains('className')`.
   - Giải thích **tại sao dùng classList tốt hơn set style trực tiếp**: tách biệt logic (JS) và giao diện (CSS), dễ bảo trì.

3. **Kiểm tra điều kiện để đổi trạng thái (nếu dạy theo cách if/else thay vì toggle)**
   - So sánh giá trị hiện tại: `if (element.style.display === 'none') {...} else {...}`.
   - Đây là bước đệm để sinh viên hiểu vì sao `toggle()` ra đời (giảm code lặp if/else).

---

## Bài 3: Đếm số lần click

**Mục tiêu:** Hiểu biến trạng thái (state variable) tồn tại giữa các lần sự kiện, và cách cập nhật nội dung text.

### Kiến thức cần nắm

1. **Biến và scope (phạm vi biến)**
   - Khai báo biến đếm `let count = 0;` **bên ngoài** hàm callback — giải thích tại sao: nếu khai báo bên trong callback, biến sẽ bị reset về 0 mỗi lần click.
   - Đây là kiến thức cốt lõi của bài: khái niệm **closure cơ bản** (không cần nói thuật ngữ "closure" với người mới, chỉ cần minh họa biến ngoài hàm được hàm bên trong "nhớ" và cập nhật).

2. **Toán tử tăng giá trị**
   - `count++`, `count += 1`, `count = count + 1` — dạy 3 cách viết tương đương.

3. **Cập nhật nội dung hiển thị**
   - `element.textContent = giá_trị` để hiển thị số đếm ra màn hình.
   - Phân biệt `textContent` (chỉ text thuần) và `innerHTML` (có thể chèn HTML) — nhấn mạnh dùng `textContent` khi không cần chèn thẻ HTML để tránh rủi ro và nhanh hơn.

4. **Ép kiểu ngầm định khi nối chuỗi**
   - Nếu dùng template string `Số lần click: ${count}`, giải thích cú pháp dấu backtick (`` ` ``) và `${}`.

---

## Bài 4: Thay đổi nội dung văn bản từ input

**Mục tiêu:** Hiểu cách đọc giá trị người dùng nhập và đưa vào DOM.

### Kiến thức cần nắm

1. **Thẻ `<input>` và thuộc tính `.value`**
   - Với input, textarea, select: giá trị người dùng nhập nằm ở thuộc tính `.value`, **không phải** `.textContent` hay `.innerHTML` (khác với div/p/span).
   - Đây là điểm sinh viên hay nhầm nhất — nên nhấn mạnh riêng và cho ví dụ sai để đối chiếu.

2. **Đọc giá trị tại thời điểm sự kiện xảy ra**
   - `const value = inputElement.value;` chỉ lấy đúng giá trị **tại thời điểm dòng code chạy** — nếu người dùng gõ thêm sau đó, biến `value` đã lưu không tự cập nhật (giải thích khác biệt giữa biến snapshot và tham chiếu DOM sống).

3. **Gắn kết input – nút – kết quả (luồng dữ liệu 1 chiều)**
   - Vẽ sơ đồ luồng: `input.value` → (khi click nút) → gán vào `p.textContent`.
   - Đây là mô hình cơ bản của mọi form xử lý dữ liệu sau này.

4. **Xử lý input rỗng (mở rộng, tùy chọn)**
   - Dùng `.trim()` để loại khoảng trắng thừa, kiểm tra `if (value === '')` để nhắc người dùng nhập lại.

---

## Bài 5: Đổi màu nền trang bằng danh sách màu

**Mục tiêu:** Hiểu cách gắn nhiều sự kiện cho nhiều phần tử, và cách xác định "nút nào vừa được click".

### Kiến thức cần nắm

1. **Chọn nhiều phần tử cùng lúc**
   - `document.querySelectorAll('selector')` trả về **NodeList** (giống mảng) chứa tất cả phần tử khớp — khác với `querySelector` chỉ lấy 1 phần tử đầu tiên.
   - Dùng vòng lặp `forEach` để duyệt qua NodeList và gắn sự kiện cho từng phần tử.

2. **Vòng lặp forEach cơ bản**
   - `nodeList.forEach((element) => { ... })` — giải thích tham số `element` đại diện cho từng phần tử trong danh sách.

3. **Đối tượng `event` và `event.target`**
   - Khi gắn `addEventListener('click', function(event) {...})`, tham số `event` chứa thông tin về sự kiện vừa xảy ra.
   - `event.target` là **phần tử cụ thể** đã bị click — quan trọng khi nhiều nút dùng chung 1 hàm xử lý, giúp biết "nút nào" chứ không phải xử lý cứng từng nút.

4. **data-* attribute (nếu muốn dạy cách chuyên nghiệp hơn)**
   - Gắn `data-color="red"` trong HTML, đọc bằng `event.target.dataset.color` trong JS — tránh việc code màu (hardcode) trực tiếp trong JS, tách dữ liệu ra HTML.

5. **Thay đổi màu nền trang**
   - `document.body.style.backgroundColor = 'red'` — nhấn mạnh `document.body` là cách truy cập thẻ `<body>` từ JS.

---

## Bài 6: Thêm phần tử vào danh sách (to-do đơn giản)

**Mục tiêu:** Đây là bài bản lề — sinh viên học cách **tạo phần tử mới bằng JS** thay vì chỉ sửa phần tử có sẵn.

### Kiến thức cần nắm

1. **Tạo phần tử mới**
   - `document.createElement('li')` tạo ra một phần tử `<li>` **trong bộ nhớ**, chưa hiển thị trên trang.
   - Nhấn mạnh: phần tử này chưa có trên DOM cho đến khi được "gắn" vào cây DOM ở bước sau.

2. **Gán nội dung cho phần tử vừa tạo**
   - `newElement.textContent = value;`

3. **Gắn phần tử vào cây DOM**
   - `parentElement.appendChild(newElement)`: thêm phần tử con vào **cuối** danh sách con của phần tử cha.
   - Giải thích khái niệm quan hệ cha–con (parent–child) trong DOM.

4. **Lấy tham chiếu tới phần tử cha (thẻ `<ul>`)**
   - `const list = document.querySelector('#todo-list');` — phải chọn đúng thẻ `<ul>` chứa danh sách trước khi `appendChild`.

5. **Reset input sau khi thêm**
   - `inputElement.value = '';` để xóa nội dung ô input sau khi đã thêm vào danh sách, cải thiện trải nghiệm người dùng.

6. **Ngăn thêm mục rỗng**
   - Kiểm tra `if (value.trim() !== '')` trước khi tạo phần tử mới — ôn lại kiến thức bài 4.

---

## Bài 7: Xóa phần tử khỏi danh sách

**Mục tiêu:** Học cách xóa phần tử động và xử lý sự kiện trên phần tử được tạo ra sau này (event delegation).

### Kiến thức cần nắm

1. **Xóa một phần tử khỏi DOM**
   - `element.remove()`: cách hiện đại, đơn giản nhất để xóa 1 phần tử.
   - (Có thể nhắc cách cũ hơn `parent.removeChild(child)` để sinh viên nhận ra khi đọc code cũ/tài liệu cũ.)

2. **Vấn đề: sự kiện không tự gắn cho phần tử tạo ra sau này**
   - Nếu gắn `addEventListener` cho các nút xóa **tại thời điểm trang load**, các mục `<li>` được thêm sau (ở bài 6) sẽ **không có** nút xóa hoạt động, vì lúc gắn sự kiện chúng chưa tồn tại.
   - Đây là điểm kiến thức quan trọng nhất của bài — cần giải thích kỹ bằng ví dụ trực quan (demo lỗi trước, rồi demo cách sửa).

3. **Giải pháp 1: Gắn sự kiện ngay khi tạo phần tử mới**
   - Trong bước tạo `<li>` mới (bài 6), tạo luôn nút "x" bên trong, và `addEventListener('click', ...)` cho nút đó ngay lúc tạo — trước khi `appendChild`.

4. **Giải pháp 2: Event Delegation (nên dạy nếu sinh viên đã vững, đây là kỹ thuật chuẩn trong thực tế)**
   - Gắn **1 sự kiện duy nhất** trên phần tử cha (`<ul>`), lợi dụng cơ chế **event bubbling** (sự kiện click trên `<li>` con sẽ "nổi bọt" lên `<ul>` cha).
   - Trong hàm xử lý, dùng `event.target` để kiểm tra xem phần tử bị click có phải là nút xóa không (`event.target.classList.contains('delete-btn')`), rồi xóa phần tử cha gần nhất của nó (`event.target.closest('li').remove()`).
   - Giải thích `closest()`: tìm phần tử tổ tiên gần nhất khớp với selector, hữu ích khi cấu trúc HTML lồng nhau.
   - Ưu điểm của event delegation: chỉ cần gắn 1 sự kiện, tự động hoạt động với mọi phần tử được thêm sau này — không gặp vấn đề ở mục 2.

---

## Bài 8: Kiểm tra độ dài chuỗi nhập vào (real-time)

**Mục tiêu:** Phân biệt các loại sự kiện trên input, hiểu sự kiện xảy ra "liên tục" khi gõ phím.

### Kiến thức cần nắm

1. **Phân biệt các sự kiện trên input**
   - `input`: kích hoạt **mỗi khi** giá trị thay đổi (gõ từng ký tự, dán, xóa...).
   - `change`: chỉ kích hoạt khi giá trị thay đổi **và** phần tử mất focus (blur) — thường dùng cho select, checkbox.
   - `keyup`/`keydown`: kích hoạt theo phím bấm, thấp hơn 1 tầng so với `input` (bắt được cả phím không đổi giá trị như mũi tên).
   - Kết luận: dùng `input` là phù hợp nhất cho yêu cầu "hiển thị ngay khi gõ".

2. **Thuộc tính `.length` của chuỗi**
   - `string.length` trả về số ký tự trong chuỗi — ôn lại kiến thức JavaScript cơ bản (không phải DOM) nhưng cần thiết cho bài.

3. **Cập nhật giao diện theo thời gian thực**
   - Kết hợp `addEventListener('input', ...)` + đọc `.value.length` + gán vào `textContent` của phần tử hiển thị — đây là mô hình "lắng nghe – xử lý – cập nhật giao diện" lặp lại xuyên suốt các bài.

4. **(Mở rộng) Giới hạn ký tự và cảnh báo**
   - So sánh `length` với một giá trị tối đa, đổi màu chữ cảnh báo nếu vượt quá — ôn lại kiến thức bài 1 (đổi style) và bài 5 (điều kiện if).

---

## Bài 9: Đổi kiểu chữ khi hover

**Mục tiêu:** Làm quen với các sự kiện chuột khác ngoài `click`.

### Kiến thức cần nắm

1. **Các sự kiện chuột (mouse events)**
   - `mouseover`/`mouseenter`: khi con trỏ chuột di vào phần tử.
   - `mouseout`/`mouseleave`: khi con trỏ chuột rời khỏi phần tử.
   - Phân biệt ngắn gọn `mouseover` vs `mouseenter` (mouseover kích hoạt cả khi di qua phần tử con bên trong, mouseenter thì không) — chỉ cần dạy sơ lược ở mức nhận biết, không đi sâu.

2. **Gắn 2 sự kiện trên cùng 1 phần tử**
   - Có thể gọi `addEventListener` hai lần với hai loại sự kiện khác nhau trên cùng một phần tử.

3. **Thay đổi style chữ**
   - `element.style.fontWeight = 'bold'` / `'normal'`.
   - `element.style.fontStyle = 'italic'` / `'normal'`.
   - Ôn lại cú pháp camelCase của thuộc tính CSS trong JS (đã học ở bài 1).

4. **So sánh cách dùng CSS `:hover` thuần túy**
   - Nhấn mạnh: hiệu ứng hover đơn giản thường nên làm bằng CSS `:hover` (không cần JS) — bài này mang tính luyện tập sự kiện chuột trong JS, nhưng nên cho sinh viên biết trong thực tế khi nào nên dùng CSS thay vì JS.

---

## Bài 10: Form kiểm tra đơn giản (validate rỗng)

**Mục tiêu:** Tổng hợp toàn bộ kiến thức các bài trước vào một bài hoàn chỉnh, thêm kiến thức về sự kiện `submit` của form.

### Kiến thức cần nắm

1. **Sự kiện `submit` trên thẻ `<form>`**
   - `form.addEventListener('submit', function(event) {...})` — gắn sự kiện trên chính thẻ `<form>`, không phải trên nút bấm.

2. **`event.preventDefault()`**
   - Mặc định, khi submit form, trình duyệt sẽ **tải lại trang** (reload). `event.preventDefault()` ngăn hành vi mặc định này để xử lý bằng JS mà không bị mất trạng thái trang.
   - Đây là kiến thức bắt buộc phải nhấn mạnh — lỗi phổ biến nhất của người mới là quên dòng này và không hiểu vì sao trang "tự load lại" và mất kết quả.

3. **Kiểm tra điều kiện dữ liệu (validate)**
   - `if (input.value.trim() === '') { // báo lỗi } else { // báo thành công }`.
   - Ôn lại `.trim()` (bài 4) và if/else.

4. **Hiển thị thông báo động**
   - Tạo sẵn 1 thẻ `<p id="message"></p>` rỗng trong HTML, dùng JS gán `textContent` và đổi `style.color` tùy theo kết quả — tổng hợp kiến thức bài 1 (style) + bài 4 (cập nhật nội dung).

5. **Tổng kết luồng xử lý form chuẩn**
   - Vẽ sơ đồ tổng quát: `submit → preventDefault → lấy giá trị → kiểm tra điều kiện → cập nhật giao diện phản hồi`.
   - Đây chính là khung sườn của **mọi form thực tế** (đăng nhập, đăng ký, liên hệ...) mà sinh viên sẽ gặp lại trong các bài học sau (kể cả khi làm với React sau này).

---

# Phần 2: 10 bài tập nâng cao hơn (Bài 11–20)

Nhóm bài này khó hơn nhóm 1 một chút — bắt đầu đụng tới `localStorage`, `setInterval`, `scroll`, tính toán trên danh sách, và các mẫu UI thực tế (modal, accordion, slideshow). Vẫn giữ nguyên tinh thần: mỗi bài chỉ thêm 1–2 khái niệm mới, còn lại ôn tập từ nhóm 10 bài trước.

## Bài 11: Lọc danh sách theo từ khóa tìm kiếm

**Mục tiêu:** Kết hợp sự kiện `input` (bài 8) với việc thao tác nhiều phần tử (bài 5–6) để lọc dữ liệu hiển thị theo thời gian thực.

### Kiến thức cần nắm

1. **Ôn lại sự kiện `input` (bài 8)** để bắt từng ký tự gõ vào ô tìm kiếm.
2. **Lấy toàn bộ phần tử cần lọc**
   - `document.querySelectorAll('.item')` trả về NodeList, chuyển thành mảng thật bằng `Array.from(nodeList)` hoặc `[...nodeList]` để dùng được các phương thức mảng như `forEach`, `filter`.
3. **So khớp chuỗi không phân biệt hoa thường**
   - `text.toLowerCase().includes(keyword.toLowerCase())` — giải thích vì sao phải hạ chữ thường cả hai vế trước khi so sánh.
4. **Ẩn/hiện theo điều kiện lọc**
   - Với mỗi phần tử: nếu khớp từ khóa thì `style.display = ''` (hoặc `'block'`), nếu không khớp thì `style.display = 'none'` — ôn lại kiến thức bài 2.
5. **Lấy nội dung text để so khớp**
   - Dùng `element.textContent` để lấy nội dung chữ hiện có trong phần tử, làm dữ liệu so sánh (khác với bài 4 là gán textContent, ở đây là đọc textContent).

---

## Bài 12: Chuyển đổi giao diện sáng/tối (Dark Mode) + ghi nhớ lựa chọn

**Mục tiêu:** Giới thiệu `localStorage` — kiến thức quan trọng để dữ liệu "sống sót" qua việc tải lại trang.

### Kiến thức cần nắm

1. **Vấn đề cần giải quyết: biến JS mất khi reload trang**
   - Nhấn mạnh: mọi biến, mọi thay đổi DOM trước giờ đều bị xóa khi F5 — đặt vấn đề để dẫn vào `localStorage`.
2. **`localStorage` là gì**
   - Kho lưu trữ dạng key–value trên trình duyệt, dữ liệu vẫn còn sau khi đóng tab/tắt trình duyệt (khác với biến JS thông thường hay `sessionStorage` chỉ tồn tại trong phiên làm việc).
3. **Các phương thức cơ bản**
   - `localStorage.setItem('key', 'value')`: lưu dữ liệu (giá trị luôn được lưu dạng **chuỗi**, kể cả khi truyền số/boolean).
   - `localStorage.getItem('key')`: đọc dữ liệu, trả về `null` nếu chưa từng lưu.
   - `localStorage.removeItem('key')`: xóa 1 key.
4. **Toggle class + lưu trạng thái**
   - Khi click nút, `document.body.classList.toggle('dark-mode')`, sau đó lưu trạng thái hiện tại vào `localStorage`.
5. **Khôi phục trạng thái khi tải lại trang**
   - Ngay khi trang load (đầu file JS, ngoài mọi hàm sự kiện), kiểm tra `localStorage.getItem('theme')` — nếu là `'dark'` thì tự động thêm class dark-mode. Đây là điểm hay bị bỏ sót nhất: sinh viên thường chỉ lưu mà quên đọc lại lúc khởi động.

---

## Bài 13: Đồng hồ đếm ngược (Countdown Timer)

**Mục tiêu:** Làm quen với hàm chạy lặp lại theo thời gian — nền tảng cho mọi hiệu ứng "tự động" sau này.

### Kiến thức cần nắm

1. **`setInterval(callback, milliseconds)`**
   - Chạy hàm `callback` lặp lại sau mỗi khoảng thời gian (tính bằng mili-giây) cho đến khi bị dừng.
   - Trả về một **id** (số) đại diện cho "bộ đếm" đó — cần lưu lại để có thể dừng sau này.
2. **`clearInterval(intervalId)`**
   - Dừng vòng lặp đã tạo bằng `setInterval` — bắt buộc phải dạy đi kèm `setInterval`, nếu không sinh viên sẽ để đồng hồ chạy mãi kể cả khi về 0 hoặc âm.
3. **Biến đếm thời gian còn lại**
   - Khai báo `let remainingSeconds = 60;` ngoài hàm interval, mỗi lần chạy giảm đi 1 — ôn lại kiến thức "biến sống ngoài hàm callback" (bài 3).
4. **Định dạng hiển thị phút:giây**
   - Tính `Math.floor(remainingSeconds / 60)` (phút) và `remainingSeconds % 60` (giây dư).
   - Dùng `String(number).padStart(2, '0')` để luôn hiển thị 2 chữ số (VD: `05` thay vì `5`) — kiến thức mới về xử lý chuỗi số.
5. **Điều kiện dừng**
   - Khi `remainingSeconds <= 0`, gọi `clearInterval` và hiển thị thông báo kết thúc.

---

## Bài 14: Thanh tiến trình cuộn trang (Scroll Progress Bar)

**Mục tiêu:** Làm quen sự kiện `scroll` và các thuộc tính đo kích thước trang.

### Kiến thức cần nắm

1. **Sự kiện `scroll`**
   - Gắn trên `window`: `window.addEventListener('scroll', callback)` — khác các bài trước gắn sự kiện trên phần tử cụ thể, đây là gắn lên toàn bộ cửa sổ trình duyệt.
2. **Các thuộc tính đo lường cần thiết**
   - `window.scrollY` (hoặc `document.documentElement.scrollTop`): khoảng cách đã cuộn từ đầu trang, tính bằng pixel.
   - `document.documentElement.scrollHeight`: tổng chiều cao toàn bộ nội dung trang.
   - `document.documentElement.clientHeight` (hoặc `window.innerHeight`): chiều cao phần hiển thị (viewport).
   - Công thức tính phần trăm đã cuộn: `scrollY / (scrollHeight - clientHeight) * 100`.
3. **Cập nhật chiều rộng thanh tiến trình**
   - `progressBar.style.width = percent + '%'` — ôn lại thao tác `.style` (bài 1), lưu ý phải nối chuỗi `'%'` vào sau số.
4. **Hiệu năng khi gắn sự kiện scroll (kiến thức mở rộng, nên nhắc qua)**
   - Sự kiện `scroll` bắn ra rất nhiều lần liên tục → nên biết khái niệm "throttle/debounce" tồn tại để tối ưu (không bắt buộc code trong bài cơ bản, chỉ giới thiệu để sinh viên biết hướng nâng cao).

---

## Bài 15: Slideshow ảnh (chuyển ảnh bằng nút Next/Prev)

**Mục tiêu:** Quản lý một chỉ số (index) để điều hướng qua lại trong một tập dữ liệu/mảng phần tử.

### Kiến thức cần nắm

1. **Mảng ảnh và biến chỉ số hiện tại**
   - Lưu danh sách ảnh trong 1 mảng (mảng URL hoặc mảng phần tử `<img>` lấy từ `querySelectorAll`).
   - Biến `let currentIndex = 0;` lưu vị trí ảnh đang hiển thị — ôn lại kiến thức "biến trạng thái ngoài hàm" (bài 3, bài 13).
2. **Tăng/giảm chỉ số có giới hạn vòng (circular index)**
   - Nút Next: `currentIndex = (currentIndex + 1) % images.length` — giải thích toán tử `%` (chia lấy dư) giúp quay vòng về 0 khi vượt quá phần tử cuối.
   - Nút Prev: `currentIndex = (currentIndex - 1 + images.length) % images.length` — giải thích vì sao phải cộng thêm `images.length` trước khi chia dư (tránh số âm).
3. **Cập nhật ảnh hiển thị**
   - Nếu dùng 1 thẻ `<img>` duy nhất: `imgElement.src = images[currentIndex]` — kiến thức mới: thuộc tính `.src` để đổi nguồn ảnh.
   - Nếu dùng nhiều thẻ `<img>` có sẵn và chỉ đổi ẩn/hiện: kết hợp `classList` (bài 2) để show đúng ảnh theo `currentIndex`.
4. **(Mở rộng) Tự động chuyển ảnh**
   - Kết hợp `setInterval` (bài 13) để tự động gọi hàm Next mỗi vài giây.

---

## Bài 16: Accordion / FAQ thu gọn – mở rộng

**Mục tiêu:** Xử lý nhiều nhóm phần tử độc lập với nhau, mỗi nhóm có hành vi mở/đóng riêng.

### Kiến thức cần nắm

1. **Cấu trúc HTML lặp lại (mỗi câu hỏi là 1 khối câu hỏi + câu trả lời)**
   - Nhấn mạnh việc đặt class chung (`.faq-question`) cho tất cả tiêu đề câu hỏi để chọn hàng loạt bằng `querySelectorAll` (ôn bài 5).
2. **Tìm phần tử liên quan bằng quan hệ DOM (DOM traversal)**
   - Kiến thức mới: `element.nextElementSibling` (phần tử anh/em kế tiếp), `element.parentElement` (phần tử cha), `element.closest(selector)` (tổ tiên gần nhất khớp selector — ôn lại bài 7).
   - Đây là cách để từ "câu hỏi vừa click" tìm ra đúng "câu trả lời" tương ứng mà không cần đặt id riêng cho từng cặp.
3. **Toggle hiển thị câu trả lời**
   - Ôn lại `classList.toggle` (bài 2) trên phần tử câu trả lời tìm được ở bước trên.
4. **(Mở rộng) Chỉ cho mở 1 mục tại 1 thời điểm**
   - Trước khi toggle mục vừa click, lặp qua tất cả các mục còn lại và đóng chúng lại (`classList.remove`) — kết hợp `forEach` (bài 5) + `classList` (bài 2).

---

## Bài 17: Giỏ hàng mini — thêm sản phẩm và tính tổng tiền

**Mục tiêu:** Bài tổng hợp: tạo phần tử động (bài 6), xóa phần tử (bài 7), và tính toán số liệu tổng hợp từ danh sách.

### Kiến thức cần nắm

1. **Lưu dữ liệu sản phẩm bằng mảng object**
   - `const cart = [];` rồi mỗi lần thêm: `cart.push({ name: '...', price: 100000 })` — kiến thức mới: object literal và mảng chứa object, thay vì chỉ làm việc trực tiếp trên DOM như các bài trước.
   - Nhấn mạnh nguyên tắc: **dữ liệu (mảng `cart`) là nguồn sự thật**, giao diện DOM chỉ là "bản vẽ lại" của dữ liệu — tư duy này là nền tảng cho React sau này.
2. **Render lại toàn bộ danh sách từ dữ liệu**
   - Viết 1 hàm `renderCart()`: xóa hết nội dung cũ (`container.innerHTML = ''`), rồi dùng `forEach` để `createElement` + `appendChild` lại từng sản phẩm từ mảng `cart` — ôn lại bài 6, nhưng lần này tạo hàng loạt từ dữ liệu thay vì từng cái đơn lẻ.
3. **Tính tổng tiền**
   - Dùng vòng lặp hoặc phương thức mảng `reduce()`: `cart.reduce((sum, item) => sum + item.price, 0)` — giới thiệu sơ lược `reduce` nếu lớp đã quen mảng, hoặc dùng vòng `for` cộng dồn nếu muốn giữ đơn giản.
4. **Định dạng số tiền**
   - `number.toLocaleString('vi-VN')` để hiển thị số có dấu chấm ngăn cách hàng nghìn — kiến thức tiện ích hay dùng trong thực tế.
5. **Xóa sản phẩm khỏi giỏ**
   - Xóa theo index: `cart.splice(index, 1)` rồi gọi lại `renderCart()` — ôn lại tư duy "sửa dữ liệu trước, vẽ lại giao diện sau" thay vì thao tác DOM trực tiếp như bài 7.

---

## Bài 18: Danh sách to-do lưu trữ với localStorage (persist qua reload)

**Mục tiêu:** Kết hợp bài 6/7 (thêm/xóa danh sách) với bài 12 (localStorage) — bài tổng hợp quan trọng.

### Kiến thức cần nắm

1. **Chuyển đổi mảng/object thành chuỗi để lưu**
   - `localStorage` chỉ lưu được **chuỗi**, trong khi danh sách to-do là 1 mảng object → cần `JSON.stringify(array)` để chuyển mảng thành chuỗi JSON trước khi `setItem`.
2. **Đọc lại và chuyển chuỗi thành dữ liệu dùng được**
   - `JSON.parse(jsonString)` để chuyển chuỗi JSON đã lưu về lại thành mảng object — kiến thức mới bắt buộc, hay đi cặp với `JSON.stringify`.
3. **Xử lý trường hợp chưa có dữ liệu**
   - Khi lần đầu mở trang, `localStorage.getItem('todos')` trả về `null` → cần kiểm tra và gán mảng rỗng `[]` mặc định, tránh lỗi khi gọi `JSON.parse(null)`.
4. **Đồng bộ dữ liệu – giao diện – localStorage sau mỗi thao tác**
   - Xây dựng quy tắc: **mỗi khi** thêm hoặc xóa 1 mục, phải làm đủ 3 bước: (1) cập nhật mảng dữ liệu, (2) `renderList()` lại giao diện (ôn bài 17), (3) `localStorage.setItem` lưu lại mảng mới nhất.
   - Đây là mô hình thu nhỏ của các ứng dụng thực tế: dữ liệu → hiển thị → lưu trữ.

---

## Bài 19: Form đăng ký nhiều trường + kiểm tra hợp lệ bằng Regex

**Mục tiêu:** Mở rộng bài 10 với nhiều trường dữ liệu và kiểm tra định dạng chặt chẽ hơn thay vì chỉ kiểm tra rỗng.

### Kiến thức cần nắm

1. **Ôn lại toàn bộ luồng form (bài 10)**
   - `submit`, `preventDefault()`, lấy `.value` của nhiều input.
2. **Regular Expression (Regex) cơ bản**
   - Khái niệm: mẫu (pattern) dùng để kiểm tra chuỗi có đúng định dạng không.
   - `const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;` và `emailPattern.test(value)` trả về `true`/`false`.
   - Chỉ cần dạy sinh viên **dùng** pattern có sẵn (email, số điện thoại Việt Nam...), không cần tự viết regex phức tạp ở trình độ cơ bản.
3. **Kiểm tra nhiều điều kiện cùng lúc**
   - Dùng nhiều `if` độc lập cho từng trường (họ tên không rỗng, email đúng định dạng, mật khẩu đủ độ dài `value.length >= 6`...) — mỗi điều kiện lỗi hiển thị thông báo riêng cạnh từng ô input.
4. **Hiển thị lỗi cạnh từng trường thay vì 1 thông báo chung**
   - Kiến thức mới: mỗi input đi kèm 1 thẻ nhỏ (VD `<span class="error"></span>`) ngay bên dưới để hiển thị lỗi riêng — ôn `textContent`/`style.color` (bài 1, 10) nhưng áp dụng lặp lại cho nhiều cặp input–span.
5. **Chỉ submit thành công khi tất cả điều kiện đều đúng**
   - Dùng 1 biến cờ `let isValid = true;`, nếu bất kỳ điều kiện nào sai thì gán `isValid = false`, cuối cùng kiểm tra biến cờ này trước khi coi là submit thành công — kỹ thuật "flag variable" khá phổ biến khi có nhiều điều kiện.

---

## Bài 20: Modal / Popup xác nhận (mở, đóng, click ra ngoài để đóng)

**Mục tiêu:** Bài tổng hợp cuối — quản lý hiển thị 1 lớp phủ (overlay), và xử lý việc click ra ngoài vùng nội dung để đóng modal (liên quan đến event bubbling).

### Kiến thức cần nắm

1. **Cấu trúc HTML của modal**
   - Lớp phủ nền mờ `.modal-overlay` bao ngoài, bên trong chứa khối nội dung `.modal-content` — giải thích cấu trúc lồng nhau này là bắt buộc để phân biệt click vào "nền" hay click vào "nội dung".
2. **Mở modal**
   - Ôn lại `classList.add`/`toggle` (bài 2) để hiện overlay khi bấm nút mở.
3. **Đóng modal bằng nút đóng (X)**
   - Ôn lại `addEventListener('click', ...)` + `classList.remove` (bài 1, 2).
4. **Đóng modal khi click ra vùng nền tối (kiến thức trọng tâm của bài)**
   - Gắn sự kiện click lên `.modal-overlay` (phần tử cha, bao trùm cả nội dung bên trong).
   - Do cơ chế **event bubbling** (đã học ở bài 7), click vào bất kỳ đâu bên trong `.modal-content` cũng sẽ "nổi bọt" lên tới `.modal-overlay` và có nguy cơ bị đóng nhầm.
   - Giải pháp: kiểm tra `event.target === event.currentTarget` (hoặc so sánh `event.target` có đúng là chính phần tử overlay hay không) — chỉ đóng modal nếu người dùng click **trực tiếp** vào nền, không phải click vào nội dung bên trong rồi mới nổi bọt lên.
   - (Cách khác, nên giới thiệu để so sánh): gọi `event.stopPropagation()` ngay trên `.modal-content` để chặn sự kiện click bên trong không cho nổi bọt lên `.modal-overlay` — giải thích đây là kỹ thuật phổ biến để "chặn bong bóng sự kiện" lan lên phần tử cha.
5. **Đóng modal bằng phím Escape (mở rộng, tùy chọn)**
   - `document.addEventListener('keydown', (e) => { if (e.key === 'Escape') {...} })` — kiến thức mới: đọc phím vừa nhấn qua `event.key`.

---

## Gợi ý trình tự giảng dạy tổng thể (đầy đủ 20 bài)

| Bài | Kiến thức mới trọng tâm | Kiến thức được ôn lại |
|---|---|---|
| 1 | querySelector, addEventListener, style | — |
| 2 | classList, display/visibility | style (bài 1) |
| 3 | biến trạng thái ngoài hàm, textContent | addEventListener (bài 1) |
| 4 | `.value` của input, luồng dữ liệu 1 chiều | textContent (bài 3) |
| 5 | querySelectorAll, forEach, event.target | style, addEventListener |
| 6 | createElement, appendChild | .value, if kiểm tra rỗng (bài 4) |
| 7 | remove(), event delegation, closest() | appendChild (bài 6) |
| 8 | sự kiện `input` (real-time) | style, textContent |
| 9 | sự kiện chuột (mouseover/mouseout) | style (bài 1) |
| 10 | sự kiện `submit`, preventDefault | toàn bộ các bài trước |
| 11 | Array.from/lọc mảng, so khớp chuỗi | sự kiện input (bài 8), display (bài 2) |
| 12 | localStorage (setItem/getItem) | classList (bài 2) |
| 13 | setInterval/clearInterval | biến trạng thái ngoài hàm (bài 3) |
| 14 | sự kiện scroll, đo kích thước trang | style (bài 1) |
| 15 | quản lý index, toán tử % | biến trạng thái (bài 3, 13) |
| 16 | DOM traversal (nextElementSibling, closest) | classList, forEach (bài 2, 5) |
| 17 | mảng object làm nguồn dữ liệu, reduce | createElement, appendChild (bài 6) |
| 18 | JSON.stringify/JSON.parse | localStorage (bài 12), render danh sách (bài 17) |
| 19 | Regex kiểm tra định dạng, flag variable | luồng form, preventDefault (bài 10) |
| 20 | event bubbling, stopPropagation | classList, addEventListener (bài 1, 2, 7) |

Cách sắp xếp này giúp mỗi bài chỉ giới thiệu **1–2 khái niệm mới**, còn lại là ôn tập — giảm tải nhận thức cho sinh viên và tạo cảm giác "lắp ráp" kiến thức dần dần thay vì học rời rạc. Nhóm bài 11–20 cũng bắt đầu làm quen với tư duy "dữ liệu quyết định giao diện" (bài 17, 18) — nền tảng quan trọng khi sinh viên chuyển sang học React sau này.
