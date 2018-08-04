Ahhh, mà lỡ click vào rồi...
##– Rồi nói gì nói đi:
- Nói một chút về cái topic này: nó là mở đầu cho series học Rust dzí tui, được truyền cảm hứng từ 2 topics của boss Đạt: [Khuyến khích mọi người nên học NNLT mới](https://daynhauhoc.com/t/khuyen-khich-moi-nguoi-nen-hoc-ngon-ngu-lap-trinh-moi/71928) và [Series học GoLang của anh Đạt](https://daynhauhoc.com/t/golang-bai-1-tour-of-go-hello-world/71940) nên mình sẽ viết một series về ngôn ngữ lập trình Rust – một NNLT mà hiện tại mình cực kỳ thích (và **rất** lâu rồi chưa viết gì với cũng rớt hạng mất tiêu rồi :'( ). Bản thân mình đánh giá Rust rất đáng học (dĩ nhiên là vậy rồi :joy: không phải thì bỏ công ra viết làm gì?). Trang chủ của RustLang: https://www.rust-lang.org/vi-VN/. Mình muốn Rust được nhiều sự chú ý mà nó đáng ra phải có :hand_splayed:. 
- Series này hướng đến mục tiêu là nắm được cơ bản về Rust.
- Với tư cách là **người cùng học** và là người đã học trước (cũng được mấy tháng rồi, không nhớ là bao lâu nữa, chắc nửa năm), mình sẽ học cùng bạn, hỗ trợ bạn, gợi ý hướng sửa, giải thích chỗ sai, chỉ dẫn tài liệu cho bạn, ... Nhưng với mình, **không có chuyện mình viết code dùm bạn**, kết quả là mình sẽ không rep post của bạn. Bạn học cho bản thân mà, tự sửa sai thì mới tiến bộ được. Lưu ý nữa: mình sẽ không là giáo viên của bạn (vì kinh nghiệm và trình độ của mình không phải thượng thừa với mình không có hứng thú nhận học sinh). Nói trước để các bạn không kỳ vọng quá nhiều.
- Nếu trong quá trình học có gì cần giải đáp, hãy pm mình. Mình sẽ cố gắng trả lời. Mà trong diễn đàn cũng có vài bạn học Rust rồi này, mình để ý nà, nếu các bạn muốn đóng góp thì cứ nói, bảo đảm mình không có trả tiền cho đâu. Hehe.
- Trong lúc viết bài, sai sót là không thể tránh khỏi. Mọi góp ý đều được chào đón!
- Vì mình có lịch học (với hơi lười) :'( nên không có viết bài thường xuyên (dự kiến 1 tuần 1-2 bài), nếu bạn muốn có bài mới thì có thể inbox nhẹ nhàng nhắc nhở mình. Mình cảm ơn trước.

##– Ờ, vậy rồi bạn lấy cái gì mà viết:
- Tài liệu! Tài liệu thì mình sẽ sử dụng kết hợp giữa kinh nghiệm của mình với:
 - [Rust by examples](https://doc.rust-lang.org/stable/rust-by-example): Học Rust kết hợp với thực hành   online. Nếu bạn học một mình và cảm thấy khá là chán khi chỉ ngồi đọc docs và (có thể) phải loay hoay với việc cài đặt đủ thứ thì học ở trang này nhanh, gọn, lẹ.
 - [The Rust Official Docs – Second Edition](https://doc.rust-lang.org/book/second-edition/index.html): Trang chủ của ebook học Rust.
 - [The Rust Standard Library](https://doc.rust-lang.org/std/): Tài liệu cho thư viện chuẩn.
 - [Docs.rs](https://docs.rs/): Trang tài liệu cho các thư viện (viết bằng Rust) khác.
 - Học cho đã cũng đừng quên chúng ta còn [stackoverflow.com](stackoverflow.com) nhé ;) 
 
- Những trang khác:
 - [Rust Playground](http://play.rust-lang.org/): bạn có thể test nhanh code trên trình duyệt.
 - [The Rustonomicon](https://doc.rust-lang.org/nomicon/): Chuyên sâu về Rust (chắc là mình không viết bài về cái này đâu, ai thích thì có thể tham khảo, mình thấy nó cũng không khó hiểu gì lắm đâu).
 - [Rust Sụbrédđít](https://www.reddit.com/r/rust/): the Rust Programming Language subreddit, nơi đây cập nhật tin tức đủ thứ về Rust :crab:
 - Còn nhiều nữa: [4rum cho Rust users](https://users.rust-lang.org/), [Bàn tán về bản thân Rust](https://internals.rust-lang.org/), ...
- Vì mình không có ra bài thường xuyên nên các bạn có thể đọc tài liệu trước cũng được, hãy cảm thấy thoải mái khi gửi tin nhắn hỏi cho mình nhé, nhớ là **đừng bảo mình viết code dùm** nhé :joy: mình cho ăn bơ á. Lưu ý là các tài liệu được viết bằng tiếng Anh, nếu bạn "không đọc được" thì bạn có 2 lựa chọn: "có gì to tát đâu :smirk:" - Học tiếng  Anh luôn, mần gì cử;hoặc "tui hổng thích ăn sung còn trên cây :relieved:" - Đợi mình viết bài, hoặc chủ động đi hỏi (dĩ nhiên là lâu hơn).

##– Ừhm, cũng ổn đấy, nói nữa đi:
- Rust cũng có các điểm thuận lợi và bất lợi. Ngay từ trang chủ, đập vào mắt là Rust:
 1. Nhanh, Rust là ngôn ngữ biên dịch và không có GC (garbage collector: bộ dọn rác) như các ngôn ngữ thông dịch hay biên dịch (như Go) khác. Tốc độ thực tiệm cận với C/C++. Tham khảo chỉ mang tính tham khảo [the benchmarksgame](https://benchmarksgame-team.pages.debian.net/benchmarksgame/faster/rust.html).
 2. Move semantics (không biết dịch sao cho vừa lòng) và Guaranteed Memory Safety (đảm bảo an toàn bộ nhớ): nghĩa là khi một biến gán giá trị cho một biến khác thì cũng sẽ chuyển *quyền sở hữu* của nó cho biến đó, dĩ nhiên là nó không thể nào đọc/ghi được giá trị nữa. Thực tế: bạn không thể nào có quyển sách đó nếu bạn đã đưa nó cho người khác. Xét 2 ví dụ đơn giản giữa C++ và Rust (xem ở cuối section này).
 3. Type inference: Rust compiler có khả năng suy luận ra kiểu của biến. Như ví dụ bên dưới: mình hoàn toàn bỏ qua được `Vec<int>` trong `let v: Vec<int> ...`, Rust compiler vẫn biết được kiểu của `v` là `Vec<int>`.
 4. Prevent data races: Khi bạn sử dụng nhiều threads cùng đọc ghi đồng thời vào một vùng nhớ sẽ dẫn đến data races, Rust không cho phép điều này xảy ra. Ví dụ thực tế, cả lớp (các threads) cùng tự ý ghi vào bảng (vùng nhớ) thì sẽ dẫn đến một mớ hỗn độn, kết quả là dữ liệu bên trong vùng nhớ không còn chính xác nữa (bạn có thể tham khảo với từ khóa `data races là gì` với Google.
 5. Rust hỗ trợ generics, pattern matching (powered by some functional programming languages). Rust code có thể gọi C code, có nghĩa là: bạn vẫn có thể dùng các thư viện có sẵn khác mà không cần phải đợi thư viện đó viết bằng Rust, và cũng như, bạn có thể viết các thư viện cho các ngôn ngữ khác như Python, Java, ... với native code.
 6. Rust đi chung với toolchains rất hiệu quả. Chỉ với lệnh `cargo`, bạn chỉ cầm thêm tên thư viện vào file Cargo.toml của projet rồi chạy `cargo build --release` là nó sẽ làm từ A-Z cho bạn: tải thư viện, biên dịch, optimize luôn. Không có khó khăn gì ở đây hết!
 7. Trình biên dịch của Rust cho ra lỗi rất hữu ích (hầu hết các trường hợp). Hữu ích đến nỗi, bạn có thể nhắm mắt làm theo hướng dẫn của trình biên dịch mà không cần dùng não. (Đùa thôi, bạn phải dùng não, nhưng đó cũng là sự thật của mình lúc mới học Rust).
 8. Còn nữa ... (chừng nào nhớ ra với dịch được thì update tiếp :joy: )

```
// C++
#include <iostream>
#include <vector>
int main() {
   std::vector<int> v  = {0, 1, 2, 3};
   std::vector<int> v2 = v;
   std::cout << "v[1]: " << v[1] << std::endl;
   return 0;
}
```
```rust
fn main() {
   let v: Vec<int> = vec![0, 1, 2, 3];
   let v2 = v;
   println!("v[1]: {}", v[1]);
}
```
Trong 2 ví dụ trên, C++ hoàn toàn có thể compile và chạy được nhưng Rust không cho phép compile vì sau khi gán, `v` không còn quyền truy cập tới vùng nhớ đó nữa.
Đây cũng là một trong các quy tắc nghiêm ngặt của Rust. Cũng vì các quy tắc đó làm cho chương trình của Rust xanh sạch đẹp và không có lỗi runtime.

- Rust cũng có nhiều điểm bất lợi, ý kiến riêng của mình:
 1. Phức tạp: Rust đã phức tạp và cả phức tạp dần theo thời gian. Team Rust làm việc rất tâm huyết :triumph: ngôn ngữ ngày có nhiều cập nhật và đổi mới, mình nghĩ đây cũng là điểm mạnh và cũng là điểm yếu. Vì thay đổi quá nhiều dẫn đến ngôn ngữ "không ổn định", các thư viện cũ sẽ gặp nhiều rắc rối nếu không được update thường xuyên (mặc dù đã có các tools. Bạn nên học dần để dễ dàng bắt kịp :3 Mình không cho là Rust khó học, Rust chỉ "hơi" phức tạp một xíu, concepts hơi lạ so với bạn một chút xíu và sẽ mất thời gian hơn một xíu nhưng cũng đáng mà :D 
 2. Mọi thứ cần rõ ràng: vì lý do rustc cũng chỉ là "cái máy" nên nó không thật sự linh hoạt. Code bạn viết ra cần  rõ ràng, đôi khi **thứ tự khai báo biến** cũng là nguyên nhân dẫn đến lỗi.
 3. Có thể còn nhiều điểm yếu khác nữa mà mình chưa biết ...

Chi tiết và sinh động hơn, các bạn hãy đọc bài của chú thefullsnack tại [đây](https://thefullsnack.com/posts/rust-intro.html) (chú trả tiền cho con vì pr dùm chú đi :P ).

##– Rồi cài đặt sao?

Trang chủ đã hướng dẫn khá là rõ ràng, có cả tiếng Việt nữa: https://www.rust-lang.org/vi-VN/install.html
Đối với các bạn sử dụng *nix thì vẫn có các package riêng lẻ như rustc, cargo, ... mình thấy nó sẽ khá rối và update thì phải đợi mirror. Mình muốn đơn giản thì chỉ cần theo hướng dẫn là đủ. Nếu trong quá trình cài đặt xuất hiện lỗi thì bạn có thể reply post này, mình sẽ cố gắng hỗ trợ. (Mình không có lưu ý gì vì mình chưa cài lỗi bao giờ :smile:) 

##– Tui thắc mắc cái này nè:
1. Q: Kinh nghiệm kiểu abc, xyz,... như tui thì có học được không?
A: Muốn thì được hết. Nhưng có thể sẽ phức tạp hơn các ngôn ngữ bạn từng học nên cần thời gian. Vì phức tạp nên cũng dễ nản, chuyện đương nhiên mà! Nhưng đừng lo, nó sẽ đáng công sức bạn bỏ ra. Lý do? Nó :clap: sẽ :clap: không  :clap: bao :clap: giờ :clap: có :clap: Segmentation :clap: Fault!  :clap:
2. Q: Khoảng bao lâu thì tui sẽ nắm vững cơ bản như cú pháp?
A: Tùy vào mỗi người, một vài tuần gì đấy, mình đoán vậy. Chưa bao gồm thời gian học sử dụng macros (cái này nâng cao rồi :3 )
3. Q: Học Rust thì làm được gì?
A: Ừhm, C/C++ làm được gì thì Rust làm được cái đó! Như: games, browsers, OSes, websites, wasm apps, ... và hệ thống nhúng (Rust làm được nhưng chắc chưa bằng C được, mình không rõ mảng này cho lắm).
4. Q: So sánh Rust với ngôn ngữ X, Y, Z,... đi?
A: Bạn có thể tham khảo Google, cũng khá nhiều. Bản thân Rust phức tạp hơn (và phức tạp dần theo thời gian) so với hầu hết các ngôn ngữ phổ biến khác nên sẽ khó khăn cho nhiều người kể cả người có kinh nghiệm lập trình lâu năm. Nếu bạn chưa học lập trình bao giờ, hoàn toàn ổn nếu bạn chọn Rust là ngôn ngữ đầu tiên, nhưng nếu Rust là ngôn ngữ thứ 2 thì có vẻ căng đấy vì những khái niệm của Rust sẽ làm cho bạn rối với ngôn ngữ bạn vừa học (nếu bạn không bị rối thì quá tốt rồi :D ).
5. Q: Nói quá trời nói rồi công ty nào xài Rust?
A: Bạn có thể tìm thấy ở [đây](https://www.rust-lang.org/en-US/friends.html).
6. Q: Muốn coi thử một chương trình viết bằng Rust thì trông nó như thế nào?
A: Mình từng viết một cái [interpreter cho Brainf*ck bằng Rust](https://daynhauhoc.com/t/i-challenge-dnh-to/56821/4) này. Vì mình muốn nó chạy nhanh một chút nên phải làm nhiều -> dài. Sau khi học xong, bạn có thể viết 1 cái chẳng hạn :D Hay lớn hơn nữa không chừng?

Hỏi thêm đi rồi mình sẽ update câu trả lời vào phần này, mình sẽ cố gắng trả lời trong giới hạn. Giờ thì mình mỏi tay quá rồi, khi khác gõ tiếp nhé :heart:

