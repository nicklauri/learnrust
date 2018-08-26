
# Mở đầu
---

Hôm trước ([ngày 2](https://daynhauhoc.com/t/cung-hoc-rust-ngay-thu-2-gia-tri-cac-kieu-du-lieu-khai-bao-bien-println/72631)), chúng ta đã được học về 'Giá trị, các kiểu dữ liệu nguyên thủy của Rust'.
Hôm nay chúng ta sẽ học về một số kiểu dữ liệu dựng sẵn là Vec (viết tắt của vector) và String. Sau bài này, mình muốn các bạn có thể sử dụng được Vec và String ở mức cơ bản.

Hai kiểu dữ liệu này không thuộc kiểu dữ liệu nguyên thủy, nhưng nó là 1 phần của thưchuẩn của Rust. Thực chất, `Vec` và `String` là 1 struct (sẽ được đề cập ở phần sau), chứa ít nhất 1 con trỏ trỏ tới vùng nhớ trong heap và 1 biến chứa số lượng phần tử/ký tự. (Mình đã đơn giản hóa vì thực tế sẽ khác một chút, tham khảo [mã nguồn của Vec](https://github.com/rust-lang/rust/blob/master/src/liballoc/vec.rs#L300) nếu bạn tò mò)
Nếu bạn chưa biết 'vùng nhớ heap' là gì thì hãy tìm kiếm trong diễn đàn nhé.

Hai kiểu dữ liệu này bạn sẽ dùng thường xuyên trong Rust như C++ có `std::vector` và `std::string` vậy. Vì các bạn chưa học struct, function, method, impl struct nên chúng ta sẽ dừng lại ở mức học cách sử dụng. Những vấn đề trên sẽ được đề cập ở các bài sau.
`String` và `Vec` không cần phải `use` nó (như import/include thư viện, đề cập sau) chúng mà vẫn sử dụng được.

# [`std::string::String`](https://doc.rust-lang.org/std/string/struct.String.html)
---

Bản thân 1 `String` hay `&str` đều là một chuỗi UTF-8 *hợp lệ*! Vì chuỗi UTF-8 ( sẽ không có dạng 1 byte - 1 ký tự như ASCII, [tham khảo UTF-8](https://en.wikipedia.org/wiki/UTF-8), nên Rust không cho phép bạn đánh chỉ số nó như `string[10]`, nhưng bạn có thể làm cách khác!

Lưu ý: `String` và `str` (hay thường thấy ở dạng borrowed của nó: `&str`) là khác nhau mặc dù đều lưu trữ dữ liệu chuỗi. Bản chất `String` là một struct (là một kiểu do người dùng định nghĩa, tương tự với C, sẽ đề cập sau), dùng heap và *không thể tự copy* được. Trong khi `str` là một kiểu nguyên thủy, được lưu trữ ở stack, heap hay ngay trên binary, đối với một chuỗi `"hello world"` thì nó là kiểu `&str` (hay chính xác hơn là `&'static str` với `'static` là lifetime). Xét ví dụ sau:

```
// Test bằng cách paste đoạn code này vào play.rust-lang.org
fn main() {
    let str1 = "hello world";
    let str2 = str1;
    println!("str1: {}", str1);
    
    // Lỗi `value used here after move` xảy ra với trường hợp này
    let string1 = String::from("hello world");
    let string2 = string1;      // Sửa: hãy comment dòng này!
    println!("string1: {}", string1);
}
```

Để tránh dài dòng, các ví dụ về code phía sau là phần code được lấy trong hàm main, nên mình sẽ không viết lại `fn main() { /* code goes here */ }`

## Tạo `String`:
---

- `String::new() -> String`: Dấu "::" (tương tự như C++) là cách mà Rust truy cập vào các phần tử bên trong 1 module, 1 enum hay 1 method của 1 struct nào đó (như static method: gọi trực tiếp mà không cần phải tạo đối tượng - instance):

```
let s1 = String::new();
// Hoặc rõ ràng hơn:
let s1: String = String::new();
```
Hai dòng code đó đều tạo ra một chuỗi rỗng và `immutable` (xem lại ngày 2), vì vậy nó chỉ hợp để ví dụ chứ không có ý nghĩa thực tế. Lưu ý: đoạn code trên vẫn hợp lệ tuy mình dùng 2 biến đều tên `s1`, vì vậy, khi bạn dùng `let` để tạo biến thì nó sẽ bỏ giá trị cũ đi và gán giá trị mới vào.
Dùng `new` thì chỉ tạo một instance của String và chưa cấp phát bất kỳ vùng đệm nào, sẵn sàng để thêm chuỗi vào bên trong String (nếu được khai báo với `mut`). Nếu bạn biết trước được độ lớn chuỗi đưa vào thì bạn nên dùng `String::with_capacity(capacity: usize)`

- `String::with_capacity(capacity: usize) -> String`: hàm này tạo một chuỗi rỗng và khởi tạo sẵn vùng nhớ với kích thước cho trước, vì cấp phát vùng nhớ là một thứ khá đắt nên hãy dùng nếu bạn có thể.
```
let string = String::with_capacity(100); // Tạo một chuỗi chứa được tối đa 100 bytes.
```

- `String::from(string: &str) -> String`: tạo một `String` từ `&str`.
```
let string = String::from("Hello world!");
```

- `String::from_utf8(vec: Vec<u8>) -> Result<String, FromUtf8Error>`: và cả họ nhà nó như `from_utf8_lossy(v: &'a [u8]) -> Cow<'a, str>` (UTF-16 cũng tương tự). Với `lossy` trong tên hàm nói rõ là sẽ có thể có một chút 'mất mát' nếu cụm bytes không phải là UTF-8 hợp lệ, các bytes không hợp lệ sẽ được thay bằng replacement character U+FFFD (như này: �). Nếu không có 'lossy' thì nó sẽ kiễm tra chặt chẽ hơn, trả về lỗi `FromUtf8Error` nếu có cụm bytes không hợp lệ.
Vì `String::from_utf8` trả về 1 `Result` nên để lấy kết quả thì ta dùng method `unwrap` để lấy dữ liệu bên trong (sẽ đề cập sau), như việc mở quà, mở ra `String` thì không sao nhưng mở ra thấy `FromUtf8Error` thì chương trình sẽ bị 'hoảng' (panic) và dừng chương trình ở đây.

```
// Sẽ báo lỗi. Sửa bằng cách comment ba dòng phía sau:
let input = b"Hello \xF0\x90\x80World";
let output = String::from_utf8(input);
println!("from_utf8: {}", output.unwrap());

// Không báo lỗi:
let input = b"Hello \xF0\x90\x80World";
let output = String::from_utf8_lossy(input);
println!("from_utf8: {}", output);
```

- `unsafe String::from_utf8_unchecked(bytes: Vec<u8>) -> String`: hàm này là một hàm "không an toàn", nó chỉ giả sử chứ không kiểm tra xem chuỗi có phải UTF-8 hợp lệ. Hàm này chỉ được sử dụng trong `unsafe` block. USE AT YOUR OWN RISK!

- `"this is &str".to_string()` -> String: chuyển một `&str` thành `String`, hoặc dùng `.to_owned()`, `.into()` cũng cho kết quả tương tự nhưng bắt buộc phải khai báo rõ ràng kiểu của biến là `String`. Vì nó có thể `.into()` thành nhiều kiểu khác nên compiler không hiểu `.into()` thành cái gì, buộc bạn phải khai thêm `: String` vào.
```
let s: String = "hello".into();
```

## Methods:
---

Một chữ `self` bên trong method sẽ đánh dấu đây là một method chỉ được gọi thông qua instance. Thật ra bạn có thể gọi có dạng như: `String::method(&mut a_string, param1, param2);`, nhưng như vậy là quá dài dòng nên hãy dùng `a_string.method(param1, param2);` cho tiện nhé ;) Dấu `.` là cách truy method của một instance (và nó phải `pub`(lic) thì mới xài được nhé).
Với từng kiểu `&self`, `&mut self`, `self` nó yêu cầu quyền truy cập tối thiểu đối với bản thân của một đối tượng là "đọc được", "đọc được và ghi được", "sẽ có toàn quyền với đối tượng và giải phóng đối tượng sau khi kết thúc hàm. Có nghĩa là, sau một hàm dùng `self` thì bạn không được dùng lại đối tượng đó nữa!

Một số method yêu cầu kiểu tham số là `&str`: bạn có thể truyền vào 1 `&str` hoặc `&String` (kiểu 'mượn' của String) vẫn được vì String đã `impl` trait cho việc tương thích này. (Sẽ đề cập trong phần `trait`)

- Tất cả các method được dùng trên `&str` đều dùng được trên `String` ;)
- `fn into_bytes(self) -> Vec<u8>`: "ăn" (consume) `String` và trả về 1 vector kiểu `u8`.
- `fn as_str(&self) -> &str`: trả về một "con trỏ" trỏ **chỉ đọc** đến chuỗi chứa trong `String`, tương đương với `&string`:
```
let string = String::from("đís y bíg");
let a_str: &str = &string;
println!("convert to &str: a_str = {}", a_str);
```

- `fn as_mut_str(&mut self) -> &mut str`: như trên nhưng nó còn có thể ghi được:

```
#![allow(unused)]
fn main() {
    let mut s = String::from("foobar");
    {
        // Đặt vào trong scope để s_mut_str tự động giải phóng
        let s_mut_str = s.as_mut_str();
        s_mut_str.make_ascii_uppercase();
        assert_eq!("FOOBAR", s_mut_str);    // Kiểm tra xem s_mut_str có bằng "FOOBAR" hay không?
    }
    println!("s: {}", s);   // Mong đợi kết quả là "FOOBAR" thay vì "foobar" ;)
}
```

- `fn len(&self) -> usize`: lấy độ dài của **số bytes** trong chuỗi, hàm này chỉ đơn giản trả về giá trị của biến length trong struct String, tốc độ thực thi nhanh. Lưu ý: nếu bạn muốn lấy độ dài của một chuỗi UTF-8, hãy dùng `self.chars().count()` sẽ trả về kết quả chính xác hơn nhưng chậm hơn `self.len()` vì nó phải kiểm tra mã UTF-8 hợp lệ cho từng ký tự.
- `fn chars(&self) -> Chars`: trả về 1 struct `Chars` dùng như iterator để lướt qua từng phần tử. Thêm: iterator có hàm `fn count(self) -> usize` trả về số lượng phần tử và "ăn" luôn cái iterator đó. Tham khảo: [`std::str::Chars`](https://doc.rust-lang.org/std/str/struct.Chars.html).
Xét ví dụ tìm độ dài ký tự:

```
#![allow(unused)]
fn main() {
    let s1 = "ascii string";
    println!("s1.len()           = {}", s1.len());
    println!("s1.chars().count() = {}", s1.chars().count());

    let s2 = "hèlô wơ";
    println!("s2.len()           = {}", s2.len());
    println!("s2.chars().count() = {}", s2.chars().count());
    
    // OUTPUT:
    //  s1.len()           = 12
    //  s1.chars().count() = 12
    //  s2.len()           = 10
    //  s2.chars().count() = 7
}
```

- `fn capacity(&self) -> usize`: lấy capacity (sức chứa | kích thước) của chuỗi, tính bằng bytes.
- `fn push(&mut self, ch: char)`: thêm 1 ký tự vào cuối chuỗi.
- `fn push_str(&mut self, string: &str)`: hàm này không trả về gì hết (hay trả về `()`), nó nhiệm vụ thêm 1 chuỗi kiểu `&str` hay `&String`.
- `fn pop(&mut self) -> Option<char>`: đẩy luôn một ký tự ra khỏi chuỗi và trả về 1 `Option` của ký tự đó.
`Option` là một `enum` (đề cập sau :|) có 2 giá trị là `Some(thing)` chứa một giá trị có kiểu `T` trong `Option<T>` và `None` là không có giá trị nào. `Some(...)` không phải là hàm, nó chỉ là một phần tử của enum `Option`. `None` của `Option` trong Rust không có nghĩa là `NULL` trong các ngôn ngữ khác, Rust không có `NULL`. Để trực tiếp lấy kết quả 

- `fn reserve(&mut self, additional: usize)`: hàm này dùng để cấp phát **thêm** cho `String` một khoảng là `additional` bytes, có thể sẽ cấp phát lớn hơn `additional` bytes 1 tí để phòng khi khỏi cấp phát lại nhiều lần. Nếu bạn muốn chỉ cần thêm chính xác `additional` bytes thì dùng hàm dưới.
- `fn reserve_exact(&mut self, additional: usize)`: giống như trên nhưng chỉ mở rộng thêm **chính xác** `additional` bytes, không dư.
- `fn as_bytes(&self) -> &[u8]`: trả về 1 tham chiếu trỏ tới slice tĩnh (immutable) chứa các phần tử u8. Slice cũng là một kiểu primitive của Rust - đề cập sau, tương tự như mảng trong các ngôn ngữ khác và có thể đánh chỉ số!
- `fn truncate(&mut self, new_len: usize)`: cắt chuỗi ngắn lại có độ dại vừa đúng bằng `new_len`, hàm này không có yếu tố cấp phát (lại). Nếu `new_len` lớn hơn `self.len()` thì không làm gì cả.
- `fn is_empty(&self) -> bool`: kiểm tra xem chuỗi có phải rỗng hay không, `true` là rỗng mà `false` là không.
- `fn split_off(&mut self, at: usize) -> String`: cắt làm 2 chuỗi, chuỗi ban đầu còn `[0, at)` và trả về một chuỗi được tạo mới `[at, self.len())`. Capacity của chuỗi ban đầu không thay đổi. Lưu ý với chuỗi UTF-8: nếu `at` nằm ngay giữ của ký tự UTF-8 thì nó sẽ được dới lại phía đầu của ký tự (1 ký tự UTF-8 có từ 1 đến 4 bytes!).
- `fn shrink_to_fit(&mut self)`: làm cho sức chứa của chuỗi đúng bằng độ dài chuỗi.
- `fn remove(&mut self, index: usize) -> char`: bỏ đi một ký tự ở vị trí `index` và trả về nó. Nếu vị trí `index` lớn hơn `self.len()` hay không nằm ở ranh giới giữa các ký tự UTF-8 thì hàm sẽ panic! Độ phức tạp O(n) vì nó copy lại từng ký tự trong chuỗi.
- `fn insert(&mut self, index: usize, ch: char)`: chèn ký tự vào vị trí `index`. Điều kiện panic và độ phức tạp của hàm này như trên.
- `fn insert(&mut self, index: usize, string: &str)`: chèn một chuỗi `&str` hoặc `&String` vào vị tri `index`. Điều kiện panic và độ phức tạp như trên.
- `fn clear(&mut self)`: xóa hết nội dung chuỗi, nhưng không đụng đến capacity của chuỗi.
- `unsafe fn as_mut_vec(&mut self) -> &mut Vec<u8>`: trả về một tham chiếu đọc-ghi là một vector u8 đến chuỗi. Hàm này yêu cầu `unsafe` block vì nó trả về một vector đọc-ghi được và ảnh hưởng đến chuỗi, và nó không thể kiểm tra được dữ liệu vào có đúng chuẩn UTF-8 hay không.

Đây là sơ lược một số hàm riêng của `String` (riêng `fn chars` là từ `&str`), ngoài ra, các hàm khác của `&str` vẫn sử dụng được với `String` như: `trim`/`trim_left`/`trim_right` trả về một chuỗi `&str` với khoảng trắng `' '`, tab `'\t'`, newline `'\n'`, `'\r'` 2 bên/trái/phải được cắt bỏ; `find` tìm chuỗi; ... nhiều hàm khác nữa trong phần `Deref<Target=str>`, bạn có thể tìm đọc ở [đây](https://doc.rust-lang.org/std/string/struct.String.html).
Phần `Trait Implementation` là tất cả các `trait` đã được viết cho `String` bên trong `std`/`core` module ngoài các hàm riêng của String. Nhớ click vào dấu `[+]` để xem chi tiết nhé. Bạn có thể hiểu đơn giản: trait là một kiểu mẫu mà nếu thứ gì được `impl`(ement) trait đó đều có hàm bên trong đó như mô tả của trait đó. Traits sẽ được đề cập trong phần tìm hiểu từ khóa `trait`.

Đối với các hàm trả về có dạng `Result<OkType,ErrorType>` hoặc `Option<Type>`, bạn có thể dùng `self.unwrap()` để "mở gói" ngay và lấy giá trị bên trong đó, nhưng nếu không có gì trong đó (lỗi hoặc `None`) thì chương trình sẽ bị `panic` và kết thúc. Có thể sẽ gặp khó khăn khi gỡ lỗi vì màn hình thông báo bị `panic` rất rườm rà và dễ rối, hãy dùng "pattern-matching" của Rust - sẽ được đề cập trong lúc học từ khóa `match` nhé!

# [`std::vec::Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html)
---

Bản thân `Vec` là một struct, bên trong có chứa một con trỏ trỏ đến dữ liệu trong vùng heap, "ngược" lại với `Vec` là slice `[]`. Dạng thường thấy của slice là dạng borrowed của nó `&[]` (vì cả `str` và `[]` không có độ dài cố định tại compile-time, sẽ nói rõ hơn trong phần primitive types phần 2).

Không như `String` đã được `impl` trait `Display` (có thể tìm thấy ở [offcial docs](https://doc.rust-lang.org/std/string/struct.String.html#impl-Display)) và trait `Debug`, `Vec` chỉ được `impl` trait `Debug` nên bạn không thể dùng `{}` trong `println!("{}", a_vector);` mà phải dùng format debug thành `println!("{:?}", a_vector);`.
Ngoài ra, `Vec` yêu cầu lập trình viên phải chỉ rõ kiểu dữ liệu bên trong của nó là gì. Nhưng ta có compiler đủ thông minh để tự suy luận được kiểu mà `Vec` đang chứa, bằng cách:

    - Đẩy một phần tử vào `Vec`, lúc này, nó sẽ chỉ chứa các giá trị chỉ thuộc kiểu đó.
    - Truyền vector như tham số vào một hàm.
    - Nhận kết quả trả về của một hàm.
    - Được gán giá trị của một `Vec` khác.
    - ...

Và `Vec` cho phép đánh chỉ số.

## Tạo `Vec`:
---

Dùng static methods hoặc dùng macro có sẵn `vec![]` để tạo nhanh một vector. Macro này có thể viết thành `vec!(...)` hay `vec!{...}`, nhưng mỗi cặp ngoặc có ý nghĩa riêng với từng macros đối với lập trình viên, nên sử dụng `vec![]` để thống nhất (nhưng là như nhau với compiler).

-   `fn new() -> Vec<T>` hoặc `Vec::new::<Type>() -> Vec<Type>`: bạn cũng thấy được, cách khai báo có thêm kiểu hơi dài một tí, nhưng sẽ rõ ràng hơn. Bằng cách thêm `::<Type>` giữa `new` và `()`, ta gọi được hàm "tổng quát" (generic), thêm `<Type>` sau `Vec` sẽ là kiểu đầy đủ của 1 `Vec`.

```
// Đúng cú pháp nhưng chưa thể compile được vì thiếu kiểu của v
let mut v = Vec::new();

// vector rỗng, đúng cú pháp nhưng thiếu kiểu của v.
let mutv = vec![];

// vector với kiểu i32 (mặc định, cho số thường không nêu kiểu số),
// compile thành công.
let mut v = vec![1, 2, 3];

// mảng 2 chiều:
let mut v2d = Vec::new::<Vec<i32>>();
let mut v2d = vec![vec![1, 2], vec![3, 4]];
println!("v2d: {:?}", v2d);
```

- `fn with_capacity(capacity: usize) -> Vec<T>`: tương tự với `String`, tạo một vector rỗng với vùng nhớ bằng `capacity * std::mem::size_of::<T>()` (`std::mem::size_of::<T>()` là cách để lấy kích thưởng của kiểu `T`, như `sizeof` với C/C++).

Chuyển một slice `&[T]` thành `Vec<T>`:
```
let ref_slice_i32 = &[1, 2, 3];
let vector = ref_slice_i32.to_vec();
```

## Methods:
---

- `fn len(&self) -> usize`: trả về số phần tử đang giữ hiện tại.
- `fn capacity(&self) -> usize`: sức chứa của vector có thể giữ được bao nhiêu **phần tử** (không phải bytes nhé).
- `fn reserve(&mut self, additional: usize)`: tương tự với `String` nhưng `additional` là số lượng phần tử chứ không phải bytes.
- `fn reserver_exact(&mut self, additional: usize)`: như trên và số lượng thêm vào không làm tròn như `reserve`.
- `fn shrink_to_fit(&mut self)`: tương tự `String`.
- `fn truncate(&mut self, len: usize)`: tương tự với `String`.
- `fn as_slice(&self) -> &[T]`: trả về slice chỉ-đọc, tương đương với `&a_vector[..]` (dấu `..` là toán tử, không phải do tác giả lười viết).
- `fn as_mut_slice(&mut self) -> &mut [T]`: trả về slice đọc-ghi, tương đương với `&mut a[..]`
- `fn swap_remove(&mut self, index: usize) -> T`: bỏ phần tử thứ `index` và trả về giá trị tại đó (tương tự với `String.remove`), nhưng nó khác `String.remove` ở chỗ: vì không cần phải theo thứ tự, nó sẽ đem phần tử cuỗi vào thay thế chỗ của phần tử bị remove nên không ảnh hưởng tốc độ thực thi (độ phức tạp O(1)). Điều kiện panic!: `index >= self.len()`. (Thứ tự của các phần tử bên trong vector sẽ bị thay đổi!)
- `fn remove(&mut self, index: usize) -> T`: tương tự với `String.remove`. Điều kiện panic!: `index >= self.len()`.
- `fn insert(&mut self, index: usize, element: T)`: chèn tại vị trí `index` là phần tử `element` và đẩy các phần tử còn lại về phía bên phải (phía cuối).
- `fn push(&mut self, element: T)`: thêm `element` vào cuối vector. Điều kiện panic!: số lượng phần tử lớn hơn cực đại của kiểu `usize`.
- `fn pop(&mut self) -> Option<T>`: đẩy phần tử cuối ra khỏi vector và trả về `Some(phần_tử)` nếu có phần_tử hoặc `None` nếu vector rỗng.
- `fn append(&mut self, other: &mut Vec<T>)`: chuyển hết các phần tử bên trong `other` sang `self` và để lại `other` là một vector rỗng. Điều kiện panic!: như `Vec.push`.
- `fn clear(&mut self)`: bỏ tất cả phần tử bên trong vector.
- `fn is_empty(&self) -> bool`: kiểm tra xem vector có rỗng hay không, tương tự `String.is_empty`.
- `fn split_off(&mut self, at: usize) -> Vec<T>`: tương tự như `String.split_off`. Điều kiện panic!: `at > self.len()`.
- `fn resize(&mut self, new_len: usize, value: T) where T: Clone`: thay đổi độ dài vector đúng bằng `new_len`, nếu `new_len <= self.len()` hàm này chỉ `self.truncate(new_len)`, nếu `new_len > self.len()` thì nó sẽ mở rộng để `self.len() == new_len` và copy `value` vào những chỗ mới. `where T: Clone` yêu cầu kiểu `T` phải được `impl` trait `Clone`.
- `fn extend_from_slice(&mut self, other: &[T])`: tạo bản sao (clone) và thêm tất cả phần tử trong slice vào cuối vector. Có thể dùng với vector để chỉ gộp mà không xóa đi dữ liệu bên trong vector kia, bằng cách đưa `&a_vector` vào chỗ của `other`.

Đây chỉ là sơ lược các hàm riêng của `Vec`, bạn có thể tham khảo thêm ở [đây](https://doc.rust-lang.org/std/vec/struct.Vec.html). Slice cũng có các hàm của riêng nó và hoàn toàn có thể dùng trên `Vec` ở mục `Deref<Target=[T]>`.
