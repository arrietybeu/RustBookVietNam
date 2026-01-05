# Lập trình một Trò chơi Đoán số

Hãy cùng nhảy vào Rust bằng cách làm việc qua một dự án thực hành! Chương này giới thiệu cho bạn một số khái niệm Rust phổ biến bằng cách cho bạn thấy cách sử dụng chúng trong một chương trình thực tế. Bạn sẽ học về `let`, `match`, các phương thức, các hàm liên kết, các crate bên ngoài, và nhiều hơn nữa! Trong các chương tiếp theo, chúng ta sẽ khám phá các ý tưởng này chi tiết hơn. Trong chương này, bạn sẽ chỉ thực hành các kiến thức cơ bản.

Chúng ta sẽ triển khai một bài toán lập trình cổ điển cho người mới bắt đầu: một trò chơi đoán số. Đây là cách nó hoạt động: Chương trình sẽ tạo một số nguyên ngẫu nhiên từ 1 đến 100. Sau đó nó sẽ nhắc người chơi nhập một dự đoán. Sau khi một dự đoán được nhập, chương trình sẽ cho biết liệu dự đoán quá thấp hay quá cao. Nếu dự đoán đúng, trò chơi sẽ in một thông báo chúc mừng và thoát.

## Thiết lập một Dự án Mới

Để thiết lập một dự án mới, hãy đến thư mục _projects_ mà bạn đã tạo trong Chương 1 và tạo một dự án mới bằng Cargo, như sau:

```console
$ cargo new guessing_game
$ cd guessing_game
```

Lệnh đầu tiên, `cargo new`, nhận tên của dự án (`guessing_game`) làm đối số đầu tiên. Lệnh thứ hai chuyển đến thư mục của dự án mới.

Hãy xem file _Cargo.toml_ được tạo ra:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial
rm -rf no-listing-01-cargo-new
cargo new no-listing-01-cargo-new --name guessing_game
cd no-listing-01-cargo-new
cargo run > output.txt 2>&1
cd ../../..
-->

<span class="filename">Tên file: Cargo.toml</span>

```toml
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/Cargo.toml}}
```

Như bạn đã thấy trong Chương 1, `cargo new` tạo một chương trình "Hello, world!" cho bạn. Hãy kiểm tra file _src/main.rs_:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/src/main.rs}}
```

Bây giờ hãy biên dịch chương trình "Hello, world!" này và chạy nó trong cùng một bước bằng lệnh `cargo run`:

```console
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/output.txt}}
```

Lệnh `run` rất hữu ích khi bạn cần lặp lại nhanh chóng trên một dự án, như chúng ta sẽ làm trong trò chơi này, nhanh chóng kiểm tra từng lần lặp trước khi chuyển sang lần tiếp theo.

Mở lại file _src/main.rs_. Bạn sẽ viết tất cả code trong file này.

## Xử lý một Dự đoán

Phần đầu tiên của chương trình trò chơi đoán số sẽ yêu cầu đầu vào từ người dùng, xử lý đầu vào đó, và kiểm tra rằng đầu vào ở dạng mong đợi. Để bắt đầu, chúng ta sẽ cho phép người chơi nhập một dự đoán. Nhập code trong Listing 2-1 vào _src/main.rs_.

<Listing number="2-1" file-name="src/main.rs" caption="Code nhận một dự đoán từ người dùng và in nó ra">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:all}}
```

</Listing>

Code này chứa rất nhiều thông tin, vì vậy hãy cùng xem qua từng dòng. Để nhận đầu vào từ người dùng và sau đó in kết quả ra đầu ra, chúng ta cần đưa thư viện `io` input/output vào phạm vi. Thư viện `io` đến từ thư viện chuẩn, được gọi là `std`:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:io}}
```

Theo mặc định, Rust có một tập hợp các item được định nghĩa trong thư viện chuẩn mà nó đưa vào phạm vi của mọi chương trình. Tập hợp này được gọi là _prelude_, và bạn có thể thấy mọi thứ trong đó [trong tài liệu thư viện chuẩn][prelude].

Nếu một kiểu bạn muốn sử dụng không có trong prelude, bạn phải đưa kiểu đó vào phạm vi một cách rõ ràng với câu lệnh `use`. Sử dụng thư viện `std::io` cung cấp cho bạn một số tính năng hữu ích, bao gồm khả năng chấp nhận đầu vào từ người dùng.

Như bạn đã thấy trong Chương 1, hàm `main` là điểm vào của chương trình:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:main}}
```

Cú pháp `fn` khai báo một hàm mới; dấu ngoặc đơn, `()`, cho biết không có tham số; và dấu ngoặc nhọn, `{`, bắt đầu thân của hàm.

Như bạn cũng đã học trong Chương 1, `println!` là một macro in một chuỗi ra màn hình:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print}}
```

Code này đang in một lời nhắc nói rõ trò chơi là gì và yêu cầu đầu vào từ người dùng.

### Lưu trữ Giá trị với Biến

Tiếp theo, chúng ta sẽ tạo một _biến_ để lưu trữ đầu vào của người dùng, như thế này:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:string}}
```

Bây giờ chương trình đang trở nên thú vị! Có rất nhiều điều đang diễn ra trong dòng nhỏ này. Chúng ta sử dụng câu lệnh `let` để tạo biến. Đây là một ví dụ khác:

```rust,ignore
let apples = 5;
```

Dòng này tạo một biến mới có tên `apples` và gắn nó với giá trị `5`. Trong Rust, các biến là bất biến (immutable) theo mặc định, có nghĩa là một khi chúng ta gán giá trị cho biến, giá trị sẽ không thay đổi. Chúng ta sẽ thảo luận khái niệm này chi tiết trong phần ["Biến và Tính khả biến"][variables-and-mutability]<!-- ignore --> ở Chương 3. Để làm cho một biến có thể thay đổi (mutable), chúng ta thêm `mut` trước tên biến:

```rust,ignore
let apples = 5; // immutable
let mut bananas = 5; // mutable
```

> Lưu ý: Cú pháp `//` bắt đầu một comment tiếp tục cho đến cuối dòng. Rust bỏ qua mọi thứ trong các comment. Chúng ta sẽ thảo luận về comment chi tiết hơn trong [Chương 3][comments]<!-- ignore -->.

Quay lại chương trình trò chơi đoán số, bây giờ bạn biết rằng `let mut guess` sẽ giới thiệu một biến có thể thay đổi có tên `guess`. Dấu bằng (`=`) nói với Rust rằng chúng ta muốn gắn thứ gì đó vào biến ngay bây giờ. Ở bên phải dấu bằng là giá trị mà `guess` được gắn vào, đó là kết quả của việc gọi `String::new`, một hàm trả về một instance mới của `String`. [`String`][string]<!-- ignore --> là một kiểu chuỗi được cung cấp bởi thư viện chuẩn, là một đoạn văn bản có thể mở rộng, được mã hóa UTF-8.

Cú pháp `::` trong dòng `::new` cho biết rằng `new` là một hàm liên kết (associated function) của kiểu `String`. Một _hàm liên kết_ là một hàm được triển khai trên một kiểu, trong trường hợp này là `String`. Hàm `new` này tạo một chuỗi mới, rỗng. Bạn sẽ tìm thấy hàm `new` trên nhiều kiểu bởi vì đó là một tên phổ biến cho một hàm tạo ra một giá trị mới của một loại nào đó.

Tóm lại, dòng `let mut guess = String::new();` đã tạo một biến có thể thay đổi hiện đang được gắn với một instance mới, rỗng của `String`. Phù!

### Nhận Đầu vào từ Người dùng

Nhớ lại rằng chúng ta đã bao gồm chức năng input/output từ thư viện chuẩn với `use std::io;` ở dòng đầu tiên của chương trình. Bây giờ chúng ta sẽ gọi hàm `stdin` từ module `io`, điều này sẽ cho phép chúng ta xử lý đầu vào từ người dùng:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:read}}
```

Nếu chúng ta không import module `io` với `use std::io;` ở đầu chương trình, chúng ta vẫn có thể sử dụng hàm bằng cách viết lời gọi hàm này là `std::io::stdin`. Hàm `stdin` trả về một instance của [`std::io::Stdin`][iostdin]<!-- ignore -->, đây là một kiểu đại diện cho một handle đến đầu vào chuẩn cho terminal của bạn.

Tiếp theo, dòng `.read_line(&mut guess)` gọi phương thức [`read_line`][read_line]<!-- ignore --> trên handle đầu vào chuẩn để lấy đầu vào từ người dùng. Chúng ta cũng truyền `&mut guess` làm đối số cho `read_line` để nói với nó chuỗi nào để lưu trữ đầu vào của người dùng. Công việc đầy đủ của `read_line` là lấy bất cứ thứ gì người dùng gõ vào đầu vào chuẩn và thêm nó vào một chuỗi (mà không ghi đè nội dung của nó), vì vậy chúng ta truyền chuỗi đó làm đối số. Đối số chuỗi cần phải có thể thay đổi để phương thức có thể thay đổi nội dung của chuỗi.

`&` cho biết rằng đối số này là một _reference_, cung cấp cho bạn một cách để cho nhiều phần của code của bạn truy cập một phần dữ liệu mà không cần sao chép dữ liệu đó vào bộ nhớ nhiều lần. Reference là một tính năng phức tạp, và một trong những lợi thế chính của Rust là việc sử dụng reference an toàn và dễ dàng như thế nào. Bạn không cần biết nhiều chi tiết đó để hoàn thành chương trình này. Hiện tại, tất cả những gì bạn cần biết là, giống như biến, reference là bất biến theo mặc định. Do đó, bạn cần viết `&mut guess` thay vì `&guess` để làm cho nó có thể thay đổi. (Chương 4 sẽ giải thích reference kỹ lưỡng hơn.)

<!-- Old headings. Do not remove or links may break. -->

<a id="handling-potential-failure-with-the-result-type"></a>

### Xử lý Lỗi Tiềm ẩn với `Result`

Chúng ta vẫn đang làm việc trên dòng code này. Bây giờ chúng ta đang thảo luận về dòng văn bản thứ ba, nhưng lưu ý rằng nó vẫn là một phần của một dòng code logic duy nhất. Phần tiếp theo là phương thức này:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:expect}}
```

Chúng ta có thể đã viết code này như:

```rust,ignore
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

Tuy nhiên, một dòng dài khó đọc, vì vậy tốt nhất là chia nó ra. Thường là khôn ngoan khi giới thiệu một dòng mới và khoảng trắng khác để giúp chia nhỏ các dòng dài khi bạn gọi một phương thức với cú pháp `.method_name()`. Bây giờ hãy thảo luận về dòng này làm gì.

Như đã đề cập trước đó, `read_line` đặt bất cứ thứ gì người dùng nhập vào chuỗi chúng ta truyền cho nó, nhưng nó cũng trả về một giá trị `Result`. [`Result`][result]<!-- ignore --> là một [_enumeration_][enums]<!-- ignore -->, thường được gọi là _enum_, đây là một kiểu có thể ở một trong nhiều trạng thái có thể. Chúng ta gọi mỗi trạng thái có thể là một _variant_.

[Chương 6][enums]<!-- ignore --> sẽ đề cập đến enum chi tiết hơn. Mục đích của các kiểu `Result` này là mã hóa thông tin xử lý lỗi.

Các variant của `Result` là `Ok` và `Err`. Variant `Ok` cho biết thao tác thành công, và nó chứa giá trị được tạo thành công. Variant `Err` có nghĩa là thao tác thất bại, và nó chứa thông tin về cách hoặc tại sao thao tác thất bại.

Các giá trị của kiểu `Result`, giống như các giá trị của bất kỳ kiểu nào, có các phương thức được định nghĩa trên chúng. Một instance của `Result` có một [phương thức `expect`][expect]<!-- ignore --> mà bạn có thể gọi. Nếu instance của `Result` này là một giá trị `Err`, `expect` sẽ khiến chương trình crash và hiển thị thông báo mà bạn truyền làm đối số cho `expect`. Nếu phương thức `read_line` trả về một `Err`, nó có thể là kết quả của một lỗi đến từ hệ điều hành cơ bản. Nếu instance của `Result` này là một giá trị `Ok`, `expect` sẽ lấy giá trị trả về mà `Ok` đang giữ và trả về chỉ giá trị đó cho bạn để bạn có thể sử dụng nó. Trong trường hợp này, giá trị đó là số byte trong đầu vào của người dùng.

Nếu bạn không gọi `expect`, chương trình sẽ biên dịch, nhưng bạn sẽ nhận được một cảnh báo:

```console
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-02-without-expect/output.txt}}
```

Rust cảnh báo rằng bạn chưa sử dụng giá trị `Result` được trả về từ `read_line`, cho biết rằng chương trình chưa xử lý một lỗi có thể xảy ra.

Cách đúng để loại bỏ cảnh báo là thực sự viết code xử lý lỗi, nhưng trong trường hợp của chúng ta, chúng ta chỉ muốn crash chương trình này khi một vấn đề xảy ra, vì vậy chúng ta có thể sử dụng `expect`. Bạn sẽ học về việc phục hồi từ lỗi trong [Chương 9][recover]<!-- ignore -->.

### In Giá trị với Placeholder `println!`

Ngoài dấu ngoặc nhọn đóng, chỉ còn một dòng nữa để thảo luận trong code cho đến nay:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print_guess}}
```

Dòng này in chuỗi hiện chứa đầu vào của người dùng. Cặp dấu ngoặc nhọn `{}` là một placeholder: Hãy nghĩ về `{}` như những cái kìm cua nhỏ giữ một giá trị tại chỗ. Khi in giá trị của một biến, tên biến có thể đi vào bên trong dấu ngoặc nhọn. Khi in kết quả của việc đánh giá một biểu thức, đặt dấu ngoặc nhọn rỗng trong chuỗi định dạng, sau đó theo chuỗi định dạng với một danh sách các biểu thức được phân tách bằng dấu phẩy để in trong mỗi placeholder dấu ngoặc nhọn rỗng theo cùng thứ tự. In một biến và kết quả của một biểu thức trong một lời gọi đến `println!` sẽ trông như thế này:

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```

Code này sẽ in `x = 5 and y + 2 = 12`.

### Kiểm tra Phần Đầu tiên

Hãy kiểm tra phần đầu tiên của trò chơi đoán số. Chạy nó bằng `cargo run`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-01/
cargo clean
cargo run
input 6 -->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 6.44s
     Running `target/debug/guessing_game`
Guess the number!
Please input your guess.
6
You guessed: 6
```

Tại thời điểm này, phần đầu tiên của trò chơi đã hoàn thành: Chúng ta đang nhận đầu vào từ bàn phím và sau đó in nó ra.

## Tạo một Số Bí mật

Tiếp theo, chúng ta cần tạo một số bí mật mà người dùng sẽ cố gắng đoán. Số bí mật nên khác nhau mỗi lần để trò chơi vui khi chơi nhiều lần. Chúng ta sẽ sử dụng một số ngẫu nhiên từ 1 đến 100 để trò chơi không quá khó. Rust chưa bao gồm chức năng số ngẫu nhiên trong thư viện chuẩn của nó. Tuy nhiên, team Rust cung cấp một [crate `rand`][randcrate] với chức năng đó.

<!-- Old headings. Do not remove or links may break. -->
<a id="using-a-crate-to-get-more-functionality"></a>

### Tăng Chức năng với một Crate

Nhớ rằng một crate là một tập hợp các file code nguồn Rust. Dự án chúng ta đã xây dựng là một binary crate, là một file thực thi. Crate `rand` là một library crate, chứa code được dự định sử dụng trong các chương trình khác và không thể được thực thi một mình.

Sự phối hợp của Cargo với các crate bên ngoài là nơi Cargo thực sự tỏa sáng. Trước khi chúng ta có thể viết code sử dụng `rand`, chúng ta cần sửa đổi file _Cargo.toml_ để bao gồm crate `rand` như một dependency. Mở file đó ngay bây giờ và thêm dòng sau vào cuối, bên dưới tiêu đề phần `[dependencies]` mà Cargo đã tạo cho bạn. Hãy chắc chắn chỉ định `rand` chính xác như chúng tôi có ở đây, với số phiên bản này, hoặc các ví dụ code trong hướng dẫn này có thể không hoạt động:

<!-- When updating the version of `rand` used, also update the version of
`rand` used in these files so they all match:
* ch07-04-bringing-paths-into-scope-with-the-use-keyword.md
* ch14-03-cargo-workspaces.md
-->

<span class="filename">Tên file: Cargo.toml</span>

```toml
{{#include ../listings/ch02-guessing-game-tutorial/listing-02-02/Cargo.toml:8:}}
```

Trong file _Cargo.toml_, mọi thứ theo sau một tiêu đề là một phần của phần đó tiếp tục cho đến khi một phần khác bắt đầu. Trong `[dependencies]`, bạn nói với Cargo crate bên ngoài nào mà dự án của bạn phụ thuộc vào và phiên bản nào của các crate đó bạn yêu cầu. Trong trường hợp này, chúng ta chỉ định crate `rand` với chỉ định phiên bản ngữ nghĩa `0.8.5`. Cargo hiểu [Semantic Versioning][semver]<!-- ignore --> (đôi khi được gọi là _SemVer_), đây là một tiêu chuẩn để viết số phiên bản. Chỉ định `0.8.5` thực sự là viết tắt của `^0.8.5`, có nghĩa là bất kỳ phiên bản nào ít nhất là 0.8.5 nhưng dưới 0.9.0.

Cargo coi các phiên bản này có API công khai tương thích với phiên bản 0.8.5, và đặc tả này đảm bảo rằng bạn sẽ nhận được bản phát hành bản vá mới nhất vẫn sẽ biên dịch với code trong chương này. Bất kỳ phiên bản 0.9.0 hoặc lớn hơn không được đảm bảo có cùng API như những gì các ví dụ sau sử dụng.

Bây giờ, mà không thay đổi bất kỳ code nào, hãy build dự án, như được hiển thị trong Listing 2-2.

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
rm Cargo.lock
cargo clean
cargo build -->

<Listing number="2-2" caption="Đầu ra từ việc chạy `cargo build` sau khi thêm crate `rand` như một dependency">

```console
$ cargo build
  Updating crates.io index
   Locking 15 packages to latest Rust 1.85.0 compatible versions
    Adding rand v0.8.5 (available: v0.9.0)
 Compiling proc-macro2 v1.0.93
 Compiling unicode-ident v1.0.17
 Compiling libc v0.2.170
 Compiling cfg-if v1.0.0
 Compiling byteorder v1.5.0
 Compiling getrandom v0.2.15
 Compiling rand_core v0.6.4
 Compiling quote v1.0.38
 Compiling syn v2.0.98
 Compiling zerocopy-derive v0.7.35
 Compiling zerocopy v0.7.35
 Compiling ppv-lite86 v0.2.20
 Compiling rand_chacha v0.3.1
 Compiling rand v0.8.5
 Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
  Finished `dev` profile [unoptimized + debuginfo] target(s) in 2.48s
```

</Listing>

Bạn có thể thấy các số phiên bản khác nhau (nhưng tất cả sẽ tương thích với code, nhờ SemVer!) và các dòng khác nhau (tùy thuộc vào hệ điều hành), và các dòng có thể theo thứ tự khác nhau.

Khi chúng ta bao gồm một dependency bên ngoài, Cargo tìm nạp các phiên bản mới nhất của mọi thứ mà dependency đó cần từ _registry_, đây là một bản sao dữ liệu từ [Crates.io][cratesio]. Crates.io là nơi mọi người trong hệ sinh thái Rust đăng các dự án Rust mã nguồn mở của họ để người khác sử dụng.

Sau khi cập nhật registry, Cargo kiểm tra phần `[dependencies]` và tải xuống bất kỳ crate nào được liệt kê chưa được tải xuống. Trong trường hợp này, mặc dù chúng ta chỉ liệt kê `rand` như một dependency, Cargo cũng lấy các crate khác mà `rand` phụ thuộc vào để hoạt động. Sau khi tải xuống các crate, Rust biên dịch chúng và sau đó biên dịch dự án với các dependency có sẵn.

Nếu bạn ngay lập tức chạy `cargo build` lại mà không thực hiện bất kỳ thay đổi nào, bạn sẽ không nhận được bất kỳ đầu ra nào ngoài dòng `Finished`. Cargo biết nó đã tải xuống và biên dịch các dependency, và bạn chưa thay đổi bất cứ điều gì về chúng trong file _Cargo.toml_ của bạn. Cargo cũng biết rằng bạn chưa thay đổi bất cứ điều gì về code của mình, vì vậy nó cũng không biên dịch lại. Không có gì để làm, nó chỉ đơn giản là thoát.

Nếu bạn mở file _src/main.rs_, thực hiện một thay đổi nhỏ, sau đó lưu nó và build lại, bạn sẽ chỉ thấy hai dòng đầu ra:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
touch src/main.rs
cargo build -->

```console
$ cargo build
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.13s
```

Các dòng này cho thấy Cargo chỉ cập nhật bản build với thay đổi nhỏ của bạn đối với file _src/main.rs_. Các dependency của bạn chưa thay đổi, vì vậy Cargo biết nó có thể tái sử dụng những gì nó đã tải xuống và biên dịch cho những thứ đó.

<!-- Old headings. Do not remove or links may break. -->
<a id="ensuring-reproducible-builds-with-the-cargo-lock-file"></a>

#### Đảm bảo Bản build Có thể Tái tạo

Cargo có một cơ chế đảm bảo rằng bạn có thể rebuild cùng một artifact mỗi khi bạn hoặc bất kỳ ai khác build code của bạn: Cargo sẽ chỉ sử dụng các phiên bản của các dependency bạn đã chỉ định cho đến khi bạn chỉ định khác. Ví dụ, giả sử rằng tuần tới phiên bản 0.8.6 của crate `rand` ra mắt, và phiên bản đó chứa một bản sửa lỗi quan trọng, nhưng nó cũng chứa một regression sẽ phá vỡ code của bạn. Để xử lý điều này, Rust tạo file _Cargo.lock_ lần đầu tiên bạn chạy `cargo build`, vì vậy bây giờ chúng ta có điều này trong thư mục _guessing_game_.

Khi bạn build một dự án lần đầu tiên, Cargo tìm ra tất cả các phiên bản của các dependency phù hợp với tiêu chí và sau đó ghi chúng vào file _Cargo.lock_. Khi bạn build dự án của mình trong tương lai, Cargo sẽ thấy rằng file _Cargo.lock_ tồn tại và sẽ sử dụng các phiên bản được chỉ định ở đó thay vì làm tất cả công việc tìm ra phiên bản lại. Điều này cho phép bạn có một bản build có thể tái tạo tự động. Nói cách khác, dự án của bạn sẽ ở lại ở 0.8.5 cho đến khi bạn nâng cấp một cách rõ ràng, nhờ vào file _Cargo.lock_. Bởi vì file _Cargo.lock_ quan trọng cho các bản build có thể tái tạo, nó thường được checked vào source control với phần còn lại của code trong dự án của bạn.

#### Cập nhật một Crate để Nhận Phiên bản Mới

Khi bạn _muốn_ cập nhật một crate, Cargo cung cấp lệnh `update`, lệnh này sẽ bỏ qua file _Cargo.lock_ và tìm ra tất cả các phiên bản mới nhất phù hợp với các đặc tả của bạn trong _Cargo.toml_. Cargo sau đó sẽ ghi các phiên bản đó vào file _Cargo.lock_. Nếu không, theo mặc định, Cargo sẽ chỉ tìm kiếm các phiên bản lớn hơn 0.8.5 và nhỏ hơn 0.9.0. Nếu crate `rand` đã phát hành hai phiên bản mới 0.8.6 và 0.999.0, bạn sẽ thấy như sau nếu bạn chạy `cargo update`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
cargo update
assuming there is a new 0.8.x version of rand; otherwise use another update
as a guide to creating the hypothetical output shown here -->

```console
$ cargo update
    Updating crates.io index
     Locking 1 package to latest Rust 1.85.0 compatible version
    Updating rand v0.8.5 -> v0.8.6 (available: v0.999.0)
```

Cargo bỏ qua bản phát hành 0.999.0. Tại thời điểm này, bạn cũng sẽ nhận thấy một thay đổi trong file _Cargo.lock_ của bạn ghi chú rằng phiên bản của crate `rand` bạn hiện đang sử dụng là 0.8.6. Để sử dụng phiên bản `rand` 0.999.0 hoặc bất kỳ phiên bản nào trong chuỗi 0.999._x_, bạn sẽ phải cập nhật file _Cargo.toml_ để trông như thế này thay thế (đừng thực sự thực hiện thay đổi này vì các ví dụ sau giả định bạn đang sử dụng `rand` 0.8):

```toml
[dependencies]
rand = "0.999.0"
```

Lần tiếp theo bạn chạy `cargo build`, Cargo sẽ cập nhật registry của các crate có sẵn và đánh giá lại các yêu cầu `rand` của bạn theo phiên bản mới bạn đã chỉ định.

Có nhiều điều hơn để nói về [Cargo][doccargo]<!-- ignore --> và [hệ sinh thái của nó][doccratesio]<!-- ignore -->, mà chúng ta sẽ thảo luận trong Chương 14, nhưng hiện tại, đó là tất cả những gì bạn cần biết. Cargo làm cho việc tái sử dụng thư viện rất dễ dàng, vì vậy Rustacean có thể viết các dự án nhỏ hơn được lắp ráp từ một số package.

### Tạo một Số Ngẫu nhiên

Hãy bắt đầu sử dụng `rand` để tạo một số để đoán. Bước tiếp theo là cập nhật _src/main.rs_, như được hiển thị trong Listing 2-3.

<Listing number="2-3" file-name="src/main.rs" caption="Thêm code để tạo một số ngẫu nhiên">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-03/src/main.rs:all}}
```

</Listing>

Đầu tiên, chúng ta thêm dòng `use rand::Rng;`. Trait `Rng` định nghĩa các phương thức mà các trình tạo số ngẫu nhiên triển khai, và trait này phải nằm trong phạm vi để chúng ta sử dụng các phương thức đó. Chương 10 sẽ đề cập đến trait chi tiết.

Tiếp theo, chúng ta thêm hai dòng ở giữa. Trong dòng đầu tiên, chúng ta gọi hàm `rand::thread_rng` cung cấp cho chúng ta trình tạo số ngẫu nhiên cụ thể mà chúng ta sẽ sử dụng: một trình cục bộ cho thread thực thi hiện tại và được seed bởi hệ điều hành. Sau đó, chúng ta gọi phương thức `gen_range` trên trình tạo số ngẫu nhiên. Phương thức này được định nghĩa bởi trait `Rng` mà chúng ta đã đưa vào phạm vi với câu lệnh `use rand::Rng;`. Phương thức `gen_range` nhận một biểu thức range làm đối số và tạo một số ngẫu nhiên trong range. Loại biểu thức range chúng ta đang sử dụng ở đây có dạng `start..=end` và bao gồm cả giới hạn dưới và trên, vì vậy chúng ta cần chỉ định `1..=100` để yêu cầu một số từ 1 đến 100.

> Lưu ý: Bạn sẽ không chỉ biết trait nào để sử dụng và phương thức và hàm nào để gọi từ một crate, vì vậy mỗi crate có tài liệu với hướng dẫn sử dụng nó. Một tính năng gọn gàng khác của Cargo là chạy lệnh `cargo doc --open` sẽ build tài liệu được cung cấp bởi tất cả các dependency của bạn cục bộ và mở nó trong trình duyệt của bạn. Nếu bạn quan tâm đến chức năng khác trong crate `rand`, ví dụ, hãy chạy `cargo doc --open` và nhấp vào `rand` trong thanh bên bên trái.

Dòng mới thứ hai in số bí mật. Điều này hữu ích trong khi chúng ta đang phát triển chương trình để có thể kiểm tra nó, nhưng chúng ta sẽ xóa nó khỏi phiên bản cuối cùng. Nó không phải là một trò chơi nhiều nếu chương trình in câu trả lời ngay khi nó bắt đầu!

Hãy thử chạy chương trình một vài lần:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-03/
cargo run
4
cargo run
5
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 7
Please input your guess.
4
You guessed: 4

$ cargo run
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 83
Please input your guess.
5
You guessed: 5
```

Bạn nên nhận được các số ngẫu nhiên khác nhau, và tất cả nên là các số từ 1 đến 100. Làm tốt lắm!

## So sánh Dự đoán với Số Bí mật

Bây giờ chúng ta có đầu vào của người dùng và một số ngẫu nhiên, chúng ta có thể so sánh chúng. Bước đó được hiển thị trong Listing 2-4. Lưu ý rằng code này sẽ chưa biên dịch được, như chúng ta sẽ giải thích.

<Listing number="2-4" file-name="src/main.rs" caption="Xử lý các giá trị trả về có thể của việc so sánh hai số">

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-04/src/main.rs:here}}
```

</Listing>

Đầu tiên, chúng ta thêm một câu lệnh `use` khác, đưa một kiểu gọi là `std::cmp::Ordering` vào phạm vi từ thư viện chuẩn. Kiểu `Ordering` là một enum khác và có các variant `Less`, `Greater`, và `Equal`. Đây là ba kết quả có thể xảy ra khi bạn so sánh hai giá trị.

Sau đó, chúng ta thêm năm dòng mới ở cuối sử dụng kiểu `Ordering`. Phương thức `cmp` so sánh hai giá trị và có thể được gọi trên bất cứ thứ gì có thể được so sánh. Nó nhận một reference đến bất cứ thứ gì bạn muốn so sánh với: Ở đây, nó đang so sánh `guess` với `secret_number`. Sau đó, nó trả về một variant của enum `Ordering` mà chúng ta đã đưa vào phạm vi với câu lệnh `use`. Chúng ta sử dụng một biểu thức [`match`][match]<!-- ignore --> để quyết định phải làm gì tiếp theo dựa trên variant nào của `Ordering` được trả về từ lời gọi đến `cmp` với các giá trị trong `guess` và `secret_number`.

Một biểu thức `match` được tạo thành từ các _arm_. Một arm bao gồm một _pattern_ để khớp, và code nên được chạy nếu giá trị được đưa cho `match` phù hợp với pattern của arm đó. Rust lấy giá trị được đưa cho `match` và xem qua pattern của từng arm lần lượt. Pattern và cấu trúc `match` là các tính năng Rust mạnh mẽ: Chúng cho phép bạn thể hiện nhiều tình huống khác nhau mà code của bạn có thể gặp phải, và chúng đảm bảo bạn xử lý tất cả chúng. Các tính năng này sẽ được đề cập chi tiết trong Chương 6 và Chương 19, tương ứng.

Hãy đi qua một ví dụ với biểu thức `match` chúng ta sử dụng ở đây. Giả sử rằng người dùng đã đoán 50 và số bí mật được tạo ngẫu nhiên lần này là 38.

Khi code so sánh 50 với 38, phương thức `cmp` sẽ trả về `Ordering::Greater` vì 50 lớn hơn 38. Biểu thức `match` nhận giá trị `Ordering::Greater` và bắt đầu kiểm tra pattern của từng arm. Nó nhìn vào pattern của arm đầu tiên, `Ordering::Less`, và thấy rằng giá trị `Ordering::Greater` không khớp với `Ordering::Less`, vì vậy nó bỏ qua code trong arm đó và chuyển sang arm tiếp theo. Pattern của arm tiếp theo là `Ordering::Greater`, _khớp_ với `Ordering::Greater`! Code liên quan trong arm đó sẽ thực thi và in `Too big!` ra màn hình. Biểu thức `match` kết thúc sau lần khớp thành công đầu tiên, vì vậy nó sẽ không xem xét arm cuối cùng trong kịch bản này.

Tuy nhiên, code trong Listing 2-4 sẽ chưa biên dịch được. Hãy thử nó:

<!--
The error numbers in this output should be that of the code **WITHOUT** the
anchor or snip comments
-->

```console
{{#include ../listings/ch02-guessing-game-tutorial/listing-02-04/output.txt}}
```

Cốt lõi của lỗi nói rằng có _mismatched types_ (các kiểu không khớp). Rust có một hệ thống kiểu mạnh, tĩnh. Tuy nhiên, nó cũng có suy luận kiểu. Khi chúng ta viết `let mut guess = String::new()`, Rust có thể suy luận rằng `guess` nên là một `String` và không làm cho chúng ta viết kiểu. Mặt khác, `secret_number` là một kiểu số. Một vài kiểu số của Rust có thể có giá trị từ 1 đến 100: `i32`, một số 32-bit; `u32`, một số 32-bit không dấu; `i64`, một số 64-bit; cũng như những kiểu khác. Trừ khi được chỉ định khác, Rust mặc định là `i32`, đó là kiểu của `secret_number` trừ khi bạn thêm thông tin kiểu ở nơi khác sẽ khiến Rust suy luận một kiểu số khác. Lý do cho lỗi là Rust không thể so sánh một chuỗi và một kiểu số.

Cuối cùng, chúng ta muốn chuyển đổi `String` mà chương trình đọc làm đầu vào thành một kiểu số để chúng ta có thể so sánh nó về mặt số với số bí mật. Chúng ta làm như vậy bằng cách thêm dòng này vào thân hàm `main`:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/src/main.rs:here}}
```

Dòng là:

```rust,ignore
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

Chúng ta tạo một biến có tên `guess`. Nhưng chờ đã, chương trình không đã có một biến có tên `guess` rồi sao? Có, nhưng một cách hữu ích là Rust cho phép chúng ta che (shadow) giá trị trước đó của `guess` bằng một giá trị mới. _Shadowing_ cho phép chúng ta tái sử dụng tên biến `guess` thay vì buộc chúng ta tạo hai biến duy nhất, chẳng hạn như `guess_str` và `guess`, ví dụ. Chúng ta sẽ đề cập điều này chi tiết hơn trong [Chương 3][shadowing]<!-- ignore -->, nhưng hiện tại, hãy biết rằng tính năng này thường được sử dụng khi bạn muốn chuyển đổi một giá trị từ một kiểu sang một kiểu khác.

Chúng ta gắn biến mới này với biểu thức `guess.trim().parse()`. `guess` trong biểu thức đề cập đến biến `guess` ban đầu chứa đầu vào dưới dạng chuỗi. Phương thức `trim` trên một instance `String` sẽ loại bỏ bất kỳ khoảng trắng nào ở đầu và cuối, điều mà chúng ta phải làm trước khi chúng ta có thể chuyển đổi chuỗi thành `u32`, chỉ có thể chứa dữ liệu số. Người dùng phải nhấn <kbd>enter</kbd> để thỏa mãn `read_line` và nhập dự đoán của họ, điều này thêm một ký tự dòng mới vào chuỗi. Ví dụ, nếu người dùng gõ <kbd>5</kbd> và nhấn <kbd>enter</kbd>, `guess` trông như thế này: `5\n`. `\n` đại diện cho "newline" (dòng mới). (Trên Windows, nhấn <kbd>enter</kbd> dẫn đến một carriage return và một dòng mới, `\r\n`.) Phương thức `trim` loại bỏ `\n` hoặc `\r\n`, chỉ còn lại `5`.

[Phương thức `parse` trên chuỗi][parse]<!-- ignore --> chuyển đổi một chuỗi sang một kiểu khác. Ở đây, chúng ta sử dụng nó để chuyển đổi từ một chuỗi sang một số. Chúng ta cần nói với Rust kiểu số chính xác mà chúng ta muốn bằng cách sử dụng `let guess: u32`. Dấu hai chấm (`:`) sau `guess` nói với Rust chúng ta sẽ chú thích kiểu của biến. Rust có một vài kiểu số tích hợp; `u32` được thấy ở đây là một số nguyên không dấu, 32-bit. Đó là một lựa chọn mặc định tốt cho một số dương nhỏ. Bạn sẽ học về các kiểu số khác trong [Chương 3][integers]<!-- ignore -->.

Ngoài ra, chú thích `u32` trong chương trình ví dụ này và việc so sánh với `secret_number` có nghĩa là Rust sẽ suy luận rằng `secret_number` cũng nên là `u32`. Vì vậy, bây giờ việc so sánh sẽ giữa hai giá trị cùng kiểu!

Phương thức `parse` sẽ chỉ hoạt động trên các ký tự có thể được chuyển đổi logic thành số và do đó có thể dễ dàng gây ra lỗi. Nếu, ví dụ, chuỗi chứa `A👍%`, sẽ không có cách nào để chuyển đổi nó thành một số. Bởi vì nó có thể thất bại, phương thức `parse` trả về một kiểu `Result`, giống như phương thức `read_line` (đã thảo luận trước đó trong ["Xử lý Lỗi Tiềm ẩn với `Result`"](#handling-potential-failure-with-result)<!-- ignore -->). Chúng ta sẽ xử lý `Result` này theo cùng một cách bằng cách sử dụng phương thức `expect` một lần nữa. Nếu `parse` trả về một variant `Result` `Err` vì nó không thể tạo một số từ chuỗi, lời gọi `expect` sẽ crash trò chơi và in thông báo chúng ta đưa cho nó. Nếu `parse` có thể chuyển đổi thành công chuỗi thành một số, nó sẽ trả về variant `Ok` của `Result`, và `expect` sẽ trả về số mà chúng ta muốn từ giá trị `Ok`.

Hãy chạy chương trình bây giờ:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/
touch src/main.rs
cargo run
  76
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.26s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 58
Please input your guess.
  76
You guessed: 76
Too big!
```

Tuyệt! Mặc dù khoảng trắng đã được thêm trước dự đoán, chương trình vẫn tìm ra rằng người dùng đã đoán 76. Chạy chương trình một vài lần để xác minh hành vi khác nhau với các loại đầu vào khác nhau: Đoán số chính xác, đoán một số quá cao, và đoán một số quá thấp.

Chúng ta có hầu hết trò chơi hoạt động bây giờ, nhưng người dùng chỉ có thể thực hiện một dự đoán. Hãy thay đổi điều đó bằng cách thêm một vòng lặp!

## Cho phép Nhiều Dự đoán với Vòng lặp

Từ khóa `loop` tạo một vòng lặp vô hạn. Chúng ta sẽ thêm một vòng lặp để cho người dùng nhiều cơ hội hơn để đoán số:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-04-looping/src/main.rs:here}}
```

Như bạn có thể thấy, chúng ta đã di chuyển mọi thứ từ lời nhắc nhập dự đoán trở đi vào một vòng lặp. Hãy chắc chắn thụt lề các dòng bên trong vòng lặp thêm bốn khoảng trắng mỗi dòng và chạy chương trình lại. Chương trình bây giờ sẽ yêu cầu một dự đoán khác mãi mãi, điều này thực sự giới thiệu một vấn đề mới. Có vẻ như người dùng không thể thoát!

Người dùng luôn có thể ngắt chương trình bằng cách sử dụng phím tắt bàn phím <kbd>ctrl</kbd>-<kbd>C</kbd>. Nhưng có một cách khác để thoát khỏi con quái vật không thể thỏa mãn này, như đã đề cập trong cuộc thảo luận `parse` trong ["So sánh Dự đoán với Số Bí mật"](#comparing-the-guess-to-the-secret-number)<!-- ignore -->: Nếu người dùng nhập một câu trả lời không phải số, chương trình sẽ crash. Chúng ta có thể tận dụng điều đó để cho phép người dùng thoát, như được hiển thị ở đây:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-04-looping/
touch src/main.rs
cargo run
(too small guess)
(too big guess)
(correct guess)
quit
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.23s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 59
Please input your guess.
45
You guessed: 45
Too small!
Please input your guess.
60
You guessed: 60
Too big!
Please input your guess.
59
You guessed: 59
You win!
Please input your guess.
quit

thread 'main' panicked at src/main.rs:28:47:
Please type a number!: ParseIntError { kind: InvalidDigit }
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Gõ `quit` sẽ thoát trò chơi, nhưng như bạn sẽ nhận thấy, việc nhập bất kỳ đầu vào không phải số nào khác cũng vậy. Điều này không tối ưu, ít nhất là; chúng ta muốn trò chơi cũng dừng khi số chính xác được đoán.

### Thoát Sau một Dự đoán Đúng

Hãy lập trình trò chơi để thoát khi người dùng thắng bằng cách thêm một câu lệnh `break`:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-05-quitting/src/main.rs:here}}
```

Thêm dòng `break` sau `You win!` làm cho chương trình thoát khỏi vòng lặp khi người dùng đoán đúng số bí mật. Thoát khỏi vòng lặp cũng có nghĩa là thoát khỏi chương trình, bởi vì vòng lặp là phần cuối cùng của `main`.

### Xử lý Đầu vào Không hợp lệ

Để tinh chỉnh thêm hành vi của trò chơi, thay vì crash chương trình khi người dùng nhập một không phải số, hãy làm cho trò chơi bỏ qua một không phải số để người dùng có thể tiếp tục đoán. Chúng ta có thể làm điều đó bằng cách thay đổi dòng mà `guess` được chuyển đổi từ `String` sang `u32`, như được hiển thị trong Listing 2-5.

<Listing number="2-5" file-name="src/main.rs" caption="Bỏ qua một dự đoán không phải số và yêu cầu một dự đoán khác thay vì crash chương trình">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-05/src/main.rs:here}}
```

</Listing>

Chúng ta chuyển từ một lời gọi `expect` sang một biểu thức `match` để chuyển từ crash khi có lỗi sang xử lý lỗi. Nhớ rằng `parse` trả về một kiểu `Result` và `Result` là một enum có các variant `Ok` và `Err`. Chúng ta đang sử dụng một biểu thức `match` ở đây, như chúng ta đã làm với kết quả `Ordering` của phương thức `cmp`.

Nếu `parse` có thể chuyển đổi thành công chuỗi thành một số, nó sẽ trả về một giá trị `Ok` chứa số kết quả. Giá trị `Ok` đó sẽ khớp với pattern của arm đầu tiên, và biểu thức `match` sẽ chỉ trả về giá trị `num` mà `parse` đã tạo ra và đặt bên trong giá trị `Ok`. Số đó sẽ kết thúc ngay nơi chúng ta muốn nó trong biến `guess` mới mà chúng ta đang tạo.

Nếu `parse` _không_ thể chuyển đổi chuỗi thành một số, nó sẽ trả về một giá trị `Err` chứa nhiều thông tin hơn về lỗi. Giá trị `Err` không khớp với pattern `Ok(num)` trong arm `match` đầu tiên, nhưng nó khớp với pattern `Err(_)` trong arm thứ hai. Dấu gạch dưới, `_`, là một giá trị bắt tất cả; trong ví dụ này, chúng ta đang nói rằng chúng ta muốn khớp với tất cả các giá trị `Err`, bất kể thông tin nào chúng có bên trong. Vì vậy, chương trình sẽ thực thi code của arm thứ hai, `continue`, nói với chương trình đi đến lần lặp tiếp theo của `loop` và yêu cầu một dự đoán khác. Vì vậy, một cách hiệu quả, chương trình bỏ qua tất cả các lỗi mà `parse` có thể gặp phải!

Bây giờ mọi thứ trong chương trình nên hoạt động như mong đợi. Hãy thử nó:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-05/
cargo run
(too small guess)
(too big guess)
foo
(correct guess)
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.13s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 61
Please input your guess.
10
You guessed: 10
Too small!
Please input your guess.
99
You guessed: 99
Too big!
Please input your guess.
foo
Please input your guess.
61
You guessed: 61
You win!
```

Tuyệt vời! Với một điều chỉnh nhỏ cuối cùng, chúng ta sẽ hoàn thành trò chơi đoán số. Nhớ lại rằng chương trình vẫn đang in số bí mật. Điều đó hoạt động tốt cho việc kiểm tra, nhưng nó làm hỏng trò chơi. Hãy xóa `println!` xuất ra số bí mật. Listing 2-6 hiển thị code cuối cùng.

<Listing number="2-6" file-name="src/main.rs" caption="Code trò chơi đoán số hoàn chỉnh">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-06/src/main.rs}}
```

</Listing>

Tại thời điểm này, bạn đã xây dựng thành công trò chơi đoán số. Chúc mừng!

## Tóm tắt

Dự án này là một cách thực hành để giới thiệu cho bạn nhiều khái niệm Rust mới: `let`, `match`, hàm, sử dụng các crate bên ngoài, và nhiều hơn nữa. Trong vài chương tiếp theo, bạn sẽ học về các khái niệm này chi tiết hơn. Chương 3 đề cập đến các khái niệm mà hầu hết các ngôn ngữ lập trình có, chẳng hạn như biến, kiểu dữ liệu, và hàm, và cho thấy cách sử dụng chúng trong Rust. Chương 4 khám phá ownership, một tính năng làm cho Rust khác biệt với các ngôn ngữ khác. Chương 5 thảo luận về struct và cú pháp phương thức, và Chương 6 giải thích cách enum hoạt động.

[prelude]: ../std/prelude/index.html
[variables-and-mutability]: ch03-01-variables-and-mutability.html#variables-and-mutability
[comments]: ch03-04-comments.html
[string]: ../std/string/struct.String.html
[iostdin]: ../std/io/struct.Stdin.html
[read_line]: ../std/io/struct.Stdin.html#method.read_line
[result]: ../std/result/enum.Result.html
[enums]: ch06-00-enums.html
[expect]: ../std/result/enum.Result.html#method.expect
[recover]: ch09-02-recoverable-errors-with-result.html
[randcrate]: https://crates.io/crates/rand
[semver]: http://semver.org
[cratesio]: https://crates.io/
[doccargo]: https://doc.rust-lang.org/cargo/
[doccratesio]: https://doc.rust-lang.org/cargo/reference/publishing.html
[match]: ch06-02-match.html
[shadowing]: ch03-01-variables-and-mutability.html#shadowing
[parse]: ../std/primitive.str.html#method.parse
[integers]: ch03-02-data-types.html#integer-types
