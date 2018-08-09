
# Giá trị, các kiểu dữ liệu và khai báo biến.


## Cách khai báo biến.

Để khai báo biến, chúng ta sử dụng từ khóa `let` trước tên biến.
Xem đoạn code kèm comment bên dưới:
``` rust
fn main(){
	// khai báo biến a với kiểu dữ liệu i32
	let a:i32; 
	
	// khai báo biến b với kiểu dữ liệu i32 và giá trị là 10
	let b:i32 = 10; 
	
	// khai báo biến c với giá trị là 10 và kiểu dữ liệu được 
	// Rust compiler tự động xác định dựa vào giá trị. 
	let c = 10;  
}
```
Các biến mặc định là immutable (không thể thay đổi giá trị). Để có thể thay đổi giá trị biến chúng ta dùng từ khóa `mut`. Chi tiết xin đề cập đến ở bài sau.

Để in ra màn hình 1 biến chúng ta dùng `print!("{}", <tên biến>);` hoặc `println!("{}", <tên biến>);` Sẽ nói rõ hơn về chúng ở cuối bài.
``` rust
fn main(){
	let a = 10;
	println!("{}", a);
}
```
output:
```
10
```

## Giá trị và các kiểu dữ liệu cơ bản.

Trong Rust hay các ngôn ngữ lập trình khác, các giá trị tồn tại ở các kiểu khác nhau. Ví dụ: `70` là một số nguyên(integer), `3.14` là một số thực(float), `z` và `A` là các ký tự (kiểu char,  hay character). Character là các giá trị thuộc bảng mã Unicode dài 4byte. `Hello world` là 1 chuỗi thuộc kiểu `&str` (Unicode  UTF8 by default). `true` và `false` thuộc kiểu bool(Boolean). 
Interger có thể được biểu diễn bằng các định dạng khác nhau:
- Thập lục phân (Hexadecimal) bắt đầu với `0x`. Ví dụ: `0x32A` cho 810.
- Bát phân (Octal) bắt đầu với `0o`. Ví dụ: `0o1452` cho 810.
- Nhị phân (Binary) bắt đầu với `0b`. Ví dụ: `0b1100101010` cho 810.

Dấu gạch dưới (Underscores) `_` có thể được dùng cho dễ đọc, ví dụ 1_000_000 tương đương với 1000000.
>Các kiểu dữ liệu số trong Rust gần giống trong Golang. 
>Ví dụ `int32`, `uint32`, `int`, `uint` và `float32` trong Go tương đương với `i32`, `u32`, `isize`, `usize` và `f32` trong Rust. 

### Kiểu số nguyên (Integer)

Kiểu số nguyên trong Rust được bắt đầu bằng `i`, `u` và phía sau là kích thước (tính bằng bit) của nó. Trong đó, `i<n>` nghĩa là kiểu số nguyên có dấu (Signed Integer) có khoảng giá trị từ -2<sup>n-1</sup> đến 2<sup>n-1</sup>-1, `u<n>` là kiểu số nguyên không dấu (Unsigned Integer) có khoảng giá trị từ 0 đến 2<sup>n</sup>-1. 

Dưới đây là các kiểu số nguyên trong Rust:
| Kích thước | Signed | Unsigned |
|--------------|---------|------------|
|8 bit         |`i8`     |`u8`        |
|16 bit        |`i16`	 |`u16`	   	  |
|32 bit		   |`i32`	 |`u32`		  |
|64 bit		   |`i64`	 |`u64`		  |
|128 bit	   |`i128`	 |`u128`	  |

Ngoài ra, Rust còn có 2 kiểu số nguyên phụ thuộc vào kiến trúc hệ điều hành là `isize` (số nguyên có dấu) và `usize` (số nguyên không dấu). Chúng có kích thước 32 bit trong hệ thống 32 bit và 64 bit trong hệ thống 64 bit.

### Kiểu số thực (Float)

Trong Rust có 2 kiểu số thực là `f32` và `f64` tương đương với kích thước 32 và 64 bit.
cách khai báo
``` rust
fn main(){
	let a = 3; // a thuộc kiểu integer(i32 by default), không phải float
	let b = 3.0; // b thuộc kiểu float (f64 by default)
	let c:f32 = 3; // c thuộc kiểu float(f32)
}
```

### Các phép toán
Rust hỗ trợ các phép toán cơ bản sử dụng cho tất cả các kiểu dữ liệu số: cộng (addition), trừ (subtraction), nhân (multiplication), chia (division) và chia lấy phần dư (remainder).
Ví dụ:
```rust
fn main() {
    // addition
    let sum = 5 + 10;
    println!("{}", sum); // 15

    // subtraction
    let difference = 95.5 - 4.3;
    println!("{}", difference); // 91.2
    
    // multiplication
    let product = 4 * 30;
    println!("{}", product); // 120
    
    // division
    let quotient = 56.7 / 32.2; // float number
    let quotient2 = 56 / 32; // integer number
    println!("{}", quotient); // 1.7608695652173911
    println!("{}", quotient2); // 1
    

    // remainder
    let remainder = 43 % 5;
    println!("{}", remainder); // 3
}
```

### Kiểu luận lý (Boolean)
Giống trong hầu hết các ngôn ngữ lập trình, kiểu `bool` trong rust có 2 giá trị là `true` và `false`
``` rust
fn main(){
	let a:bool = false; // khai báo `a` kiểu bool giá trị false
	let b = true; // rust compiler tự suy luận `b` thuộc kiểu bool
}
```

### Kiểu kí tự (Character)
Kiểu `char` trong Rust được biểu diễn bên trong dấu nháy đơn `'` là các ký tự thuộc bảng mã Unicode:
``` rust
fn main(){
	let a = 'a';
	let b = '😻';
	println!("{}", a);
	println!("{}", b);
}
```
output:
```
a
😻
```

### Kiểu chuỗi (String)
Trong Rust có 2 kiểu chuỗi là `&str` và `String`. `String` sẽ được giới thiệu sau. 
``` rust
fn main(){
	let s = "Hello World"; // kiểu &'static str ('static là lifetime, chúng ta chưa quan tâm.)
	println!("{}", s); // Hello World
}
```

### Empty type `()`
`()` trong Rust có nghĩa là không có giá trị. Các hàm trả về kiểu `()` tương đương với các hàm không trả về giá trị. Ví dụ:
``` rust
fn main() -> (){
}
```
Tương đương với 
``` rust
fn main(){
}
```
`()` không tương đương với `null` trong các ngôn ngữ khác. `null` là giá trị còn `()` không phải là giá trị.

## Nói thêm về `println!`

`println!` tương đương với `print!` khác biệt là `println!` sẽ thêm ký tự xuống dòng ở cuối chuỗi được in ra.

Như các ví dụ phía trên, cách rõ nhất để biết giá trị của biến là hiển thị nó ra. 
``` rust
fn main(){
	let a = 10;
	println!("giá trị của biến a là: {}", a);
}
```

Đối số đầu tiên của  macro `println!` là 1 chuỗi định dạng kèm theo là các `{}` (placeholder). Giá trị các hằng số hay các biến sẽ được chuyển thành chuỗi và lần lượt thay thế vào các vị trí `{}`. Ví dụ:

``` rust
fn main(){
	println!("{}, {}, {}", 1, false, "hello world")";
}
```
output: 
```
1, false, hello world
```

**Các placeholder có thể được đánh thứ tự để sử dụng nhiều lần:**
``` rust
fn main(){
	let name = "Rust";
	let version = 1.28;
	println!("{0} là 1 ngôn ngữ lập trình dạng biên dịch. 
Phiên bản mới nhất của {0} hiện tại là {1}", name, version);
}
```
output :
```
Rust là 1 ngôn ngữ lập trình dạng biên dịch. 
Phiên bản mới nhất của Rust hiện tại là 1.28

```

**Cũng có thể đặt tên cho các đối số:**
``` rust
println!("Ngôn ngữ lập trình là {name}", name = "Rust");
```
output:
```
Ngôn ngữ lập trình là Rust
```

**Các định dạng đặc biệt có thể được biểu thị bên trong `{}` sau dấu `:`**
Ví dụ:
``` rust 
    println!("Số 18 trong hệ thập lục phân là {:0x}.", 18);
    println!("Số 18 trong hệ nhị phân là {:0b}", 18);   
    println!("Số 18 trong hệ bát phân là {:0o}", 18);
```

output:
```
Số 18 trong hệ thập lục phân là 12.
Số 18 trong hệ nhị phân là 10010
Số 18 trong hệ bát phân là 22
```

Các kiểu format như trên gồm có:
- `?` cho mục đích debug
- `o` cho số hệ bát phân
- `x`  cho số hệ thập lục phân ở dạng viết thường
- `X`  cho số hệ thập lục phân ở dạng viết hoa
- `p` cho con trỏ (địa chỉ)
- `b` cho số hệ nhị phân
- `e` cho biểu diễn số mũ số thực dạng viết thường
- `E` cho biểu diễn số mũ số thực dạng viết hoa


macro `format!` trả về giá trị kiểu `String` cũng có cách dùng tương tự với `println!`. 
Xem thêm tại https://doc.rust-lang.org/std/fmt/

