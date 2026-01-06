## Kiểu dữ liệu

Mỗi giá trị trong Rust thuộc một _kiểu dữ liệu_ nhất định, cho Rust biết loại dữ liệu nào đang được chỉ định để nó biết cách làm việc với dữ liệu đó. Chúng ta sẽ xem xét hai tập con của kiểu dữ liệu: scalar và compound.

Hãy nhớ rằng Rust là một ngôn ngữ _statically typed_ (kiểu tĩnh), có nghĩa là nó phải biết các kiểu của tất cả biến tại compile time. Compiler thường có thể suy luận kiểu mà chúng ta muốn sử dụng dựa trên giá trị và cách chúng ta sử dụng nó. Trong các trường hợp khi nhiều kiểu có thể xảy ra, chẳng hạn như khi chúng ta chuyển đổi một `String` sang kiểu số bằng `parse` trong phần ["So sánh Dự đoán với Số Bí mật"][comparing-the-guess-to-the-secret-number]<!-- ignore --> ở Chương 2, chúng ta phải thêm chú thích kiểu, như thế này:

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

Nếu chúng ta không thêm chú thích kiểu `: u32` được hiển thị trong code trước đó, Rust sẽ hiển thị lỗi sau, có nghĩa là compiler cần thêm thông tin từ chúng ta để biết kiểu nào chúng ta muốn sử dụng:

```console
{{#include ../listings/ch03-common-programming-concepts/output-only-01-no-type-annotations/output.txt}}
```

Bạn sẽ thấy các chú thích kiểu khác nhau cho các kiểu dữ liệu khác.

### Scalar Types

Một kiểu _scalar_ đại diện cho một giá trị đơn lẻ. Rust có bốn kiểu scalar chính: số nguyên (integers), số dấu phẩy động (floating-point numbers), Boolean, và ký tự (characters). Bạn có thể nhận ra chúng từ các ngôn ngữ lập trình khác. Hãy tìm hiểu cách chúng hoạt động trong Rust.

#### Kiểu Số nguyên

Một _số nguyên_ (integer) là một số không có phần thập phân. Chúng ta đã sử dụng một kiểu số nguyên trong Chương 2, kiểu `u32`. Khai báo kiểu này cho biết rằng giá trị được liên kết với nó nên là một số nguyên không dấu (các kiểu số nguyên có dấu bắt đầu bằng `i` thay vì `u`) chiếm 32 bit không gian. Bảng 3-1 cho thấy các kiểu số nguyên tích hợp trong Rust. Chúng ta có thể sử dụng bất kỳ variant nào trong số này để khai báo kiểu của một giá trị số nguyên.

<span class="caption">Bảng 3-1: Các Kiểu Số nguyên trong Rust</span>

| Length  | Signed  | Unsigned |
| ------- | ------- | -------- |
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| Architecture-dependent | `isize` | `usize`  |

Mỗi variant có thể là signed (có dấu) hoặc unsigned (không dấu) và có kích thước rõ ràng. _Signed_ và _unsigned_ đề cập đến việc liệu số có thể âm hay không—nói cách khác, liệu số cần có dấu (signed) hay liệu nó sẽ chỉ dương và do đó có thể được biểu diễn mà không có dấu (unsigned). Nó giống như viết số trên giấy: Khi dấu quan trọng, một số được hiển thị với dấu cộng hoặc dấu trừ; tuy nhiên, khi an toàn để giả định số là dương, nó được hiển thị mà không có dấu. Số signed được lưu trữ bằng cách sử dụng biểu diễn [two's complement][twos-complement]<!-- ignore -->.

Mỗi variant signed có thể lưu trữ các số từ −(2<sup>n − 1</sup>) đến 2<sup>n − 1</sup> − 1 bao gồm, trong đó _n_ là số bit mà variant sử dụng. Vì vậy, một `i8` có thể lưu trữ các số từ −(2<sup>7</sup>) đến 2<sup>7</sup> − 1, bằng −128 đến 127. Các variant unsigned có thể lưu trữ các số từ 0 đến 2<sup>n</sup> − 1, vì vậy một `u8` có thể lưu trữ các số từ 0 đến 2<sup>8</sup> − 1, bằng 0 đến 255.

Ngoài ra, các kiểu `isize` và `usize` phụ thuộc vào kiến trúc của máy tính mà chương trình của bạn đang chạy: 64 bit nếu bạn đang ở trên kiến trúc 64-bit và 32 bit nếu bạn đang ở trên kiến trúc 32-bit.

Bạn có thể viết integer literals theo bất kỳ dạng nào được hiển thị trong Bảng 3-2. Lưu ý rằng number literals có thể là nhiều kiểu số cho phép một type suffix, chẳng hạn như `57u8`, để chỉ định kiểu. Number literals cũng có thể sử dụng `_` làm dấu phân cách trực quan để làm cho số dễ đọc hơn, chẳng hạn như `1_000`, sẽ có cùng giá trị như nếu bạn đã chỉ định `1000`.

<span class="caption">Bảng 3-2: Integer Literals trong Rust</span>

| Number literals  | Example       |
| ---------------- | ------------- |
| Decimal          | `98_222`      |
| Hex              | `0xff`        |
| Octal            | `0o77`        |
| Binary           | `0b1111_0000` |
| Byte (`u8` only) | `b'A'`        |

Vậy làm thế nào để bạn biết loại số nguyên nào để sử dụng? Nếu bạn không chắc chắn, các giá trị mặc định của Rust thường là nơi tốt để bắt đầu: Các kiểu số nguyên mặc định là `i32`. Tình huống chính mà bạn sẽ sử dụng `isize` hoặc `usize` là khi index một loại collection.

> ##### Integer Overflow
>
> Giả sử bạn có một biến kiểu `u8` có thể giữ các giá trị từ 0 đến 255. Nếu bạn cố gắng thay đổi biến thành một giá trị ngoài phạm vi đó, chẳng hạn như 256, _integer overflow_ (tràn số nguyên) sẽ xảy ra, có thể dẫn đến một trong hai hành vi. Khi bạn đang biên dịch ở chế độ debug, Rust bao gồm các kiểm tra cho integer overflow khiến chương trình của bạn _panic_ tại runtime nếu hành vi này xảy ra. Rust sử dụng thuật ngữ _panicking_ khi một chương trình thoát với lỗi; chúng ta sẽ thảo luận về panic chi tiết hơn trong phần ["Lỗi Không thể Phục hồi với `panic!`"][unrecoverable-errors-with-panic]<!-- ignore --> ở Chương 9.
>
> Khi bạn đang biên dịch ở chế độ release với cờ `--release`, Rust _không_ bao gồm các kiểm tra cho integer overflow gây panic. Thay vào đó, nếu overflow xảy ra, Rust thực hiện _two's complement wrapping_. Tóm lại, các giá trị lớn hơn giá trị tối đa mà kiểu có thể giữ "wrap around" (quấn vòng) đến giá trị tối thiểu của các giá trị mà kiểu có thể giữ. Trong trường hợp của `u8`, giá trị 256 trở thành 0, giá trị 257 trở thành 1, và cứ thế. Chương trình sẽ không panic, nhưng biến sẽ có một giá trị có lẽ không phải là những gì bạn đã mong đợi. Dựa vào hành vi wrapping của integer overflow được coi là một lỗi.
>
> Để xử lý rõ ràng khả năng overflow, bạn có thể sử dụng các họ phương thức này được cung cấp bởi thư viện chuẩn cho các kiểu số nguyên nguyên thủy:
>
> - Wrap ở tất cả các chế độ với các phương thức `wrapping_*`, chẳng hạn như `wrapping_add`.
> - Trả về giá trị `None` nếu có overflow với các phương thức `checked_*`.
> - Trả về giá trị và một Boolean cho biết liệu có overflow với các phương thức `overflowing_*`.
> - Bão hòa ở giá trị tối thiểu hoặc tối đa của giá trị với các phương thức `saturating_*`.

#### Kiểu Số dấu phẩy động

Rust cũng có hai kiểu nguyên thủy cho _số dấu phẩy động_ (floating-point numbers), là các số có dấu thập phân. Các kiểu số dấu phẩy động của Rust là `f32` và `f64`, lần lượt có kích thước 32 bit và 64 bit. Kiểu mặc định là `f64` vì trên CPU hiện đại, nó có tốc độ gần như tương đương với `f32` nhưng có khả năng chính xác hơn. Tất cả các kiểu số dấu phẩy động đều có dấu.

Đây là một ví dụ cho thấy số dấu phẩy động trong hành động:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-06-floating-point/src/main.rs}}
```

Số dấu phẩy động được biểu diễn theo tiêu chuẩn IEEE-754.

#### Các Phép toán Số

Rust hỗ trợ các phép toán cơ bản mà bạn mong đợi cho tất cả các kiểu số: cộng, trừ, nhân, chia, và phần dư. Phép chia số nguyên cắt về phía không đến số nguyên gần nhất. Code sau đây cho thấy cách bạn sẽ sử dụng mỗi phép toán số trong câu lệnh `let`:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-07-numeric-operations/src/main.rs}}
```

Mỗi biểu thức trong các câu lệnh này sử dụng một toán tử toán học và đánh giá thành một giá trị đơn lẻ, sau đó được gắn với một biến. [Phụ lục B][appendix_b]<!-- ignore --> chứa danh sách tất cả các toán tử mà Rust cung cấp.

#### Kiểu Boolean

Như trong hầu hết các ngôn ngữ lập trình khác, một kiểu Boolean trong Rust có hai giá trị có thể: `true` và `false`. Boolean có kích thước một byte. Kiểu Boolean trong Rust được chỉ định bằng `bool`. Ví dụ:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-08-boolean/src/main.rs}}
```

Cách chính để sử dụng giá trị Boolean là thông qua các điều kiện, chẳng hạn như biểu thức `if`. Chúng ta sẽ đề cập đến cách biểu thức `if` hoạt động trong Rust trong phần ["Luồng điều khiển"][control-flow]<!-- ignore -->.

#### Kiểu Ký tự

Kiểu `char` của Rust là kiểu chữ cái nguyên thủy nhất của ngôn ngữ. Đây là một số ví dụ về khai báo giá trị `char`:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-09-char/src/main.rs}}
```

Lưu ý rằng chúng ta chỉ định `char` literals với dấu ngoặc đơn, trái ngược với string literals, sử dụng dấu ngoặc kép. Kiểu `char` của Rust có kích thước 4 byte và đại diện cho một Unicode scalar value, có nghĩa là nó có thể đại diện cho nhiều hơn chỉ ASCII. Các chữ cái có dấu; các ký tự Trung Quốc, Nhật Bản và Hàn Quốc; emoji; và khoảng trắng không chiều rộng đều là các giá trị `char` hợp lệ trong Rust. Unicode scalar values nằm trong khoảng từ `U+0000` đến `U+D7FF` và `U+E000` đến `U+10FFFF` bao gồm. Tuy nhiên, "ký tự" không thực sự là một khái niệm trong Unicode, vì vậy trực giác của con người về "ký tự" là gì có thể không khớp với `char` trong Rust. Chúng ta sẽ thảo luận chủ đề này chi tiết trong ["Lưu trữ Văn bản Mã hóa UTF-8 với Strings"][strings]<!-- ignore --> trong Chương 8.

### Compound Types

_Compound types_ (kiểu hợp) có thể nhóm nhiều giá trị thành một kiểu. Rust có hai kiểu compound nguyên thủy: tuple và array.

#### Kiểu Tuple

Một _tuple_ là một cách chung để nhóm một số giá trị với nhiều kiểu khác nhau thành một kiểu compound. Tuple có độ dài cố định: Một khi được khai báo, chúng không thể tăng hoặc giảm kích thước.

Chúng ta tạo một tuple bằng cách viết một danh sách các giá trị được phân tách bằng dấu phẩy bên trong dấu ngoặc đơn. Mỗi vị trí trong tuple có một kiểu, và các kiểu của các giá trị khác nhau trong tuple không cần phải giống nhau. Chúng ta đã thêm chú thích kiểu tùy chọn trong ví dụ này:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-10-tuples/src/main.rs}}
```

Biến `tup` được gắn với toàn bộ tuple vì một tuple được coi là một phần tử compound đơn lẻ. Để lấy các giá trị riêng lẻ ra khỏi tuple, chúng ta có thể sử dụng pattern matching để destructure một giá trị tuple, như thế này:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-11-destructuring-tuples/src/main.rs}}
```

Chương trình này đầu tiên tạo một tuple và gắn nó với biến `tup`. Sau đó, nó sử dụng một pattern với `let` để lấy `tup` và biến nó thành ba biến riêng biệt, `x`, `y`, và `z`. Điều này được gọi là _destructuring_ vì nó chia tuple đơn lẻ thành ba phần. Cuối cùng, chương trình in giá trị của `y`, là `6.4`.

Chúng ta cũng có thể truy cập một phần tử tuple trực tiếp bằng cách sử dụng dấu chấm (`.`) theo sau là index của giá trị chúng ta muốn truy cập. Ví dụ:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-12-tuple-indexing/src/main.rs}}
```

Chương trình này tạo tuple `x` và sau đó truy cập từng phần tử của tuple bằng các index tương ứng của chúng. Như với hầu hết các ngôn ngữ lập trình, index đầu tiên trong tuple là 0.

Tuple không có bất kỳ giá trị nào có tên đặc biệt, _unit_. Giá trị này và kiểu tương ứng của nó đều được viết `()` và đại diện cho một giá trị rỗng hoặc một kiểu trả về rỗng. Các biểu thức ngầm định trả về giá trị unit nếu chúng không trả về bất kỳ giá trị nào khác.

#### Kiểu Array

Một cách khác để có một collection của nhiều giá trị là với một _array_. Không giống như tuple, mỗi phần tử của array phải có cùng kiểu. Không giống như array trong một số ngôn ngữ khác, array trong Rust có độ dài cố định.

Chúng ta viết các giá trị trong array như một danh sách được phân tách bằng dấu phẩy bên trong dấu ngoặc vuông:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-13-arrays/src/main.rs}}
```

Array hữu ích khi bạn muốn dữ liệu của mình được cấp phát trên stack, giống như các kiểu khác mà chúng ta đã thấy cho đến nay, thay vì heap (chúng ta sẽ thảo luận về stack và heap nhiều hơn trong [Chương 4][stack-and-heap]<!-- ignore -->) hoặc khi bạn muốn đảm bảo rằng bạn luôn có một số phần tử cố định. Tuy nhiên, array không linh hoạt như kiểu vector. Vector là một kiểu collection tương tự được cung cấp bởi thư viện chuẩn _được phép_ tăng hoặc giảm kích thước vì nội dung của nó nằm trên heap. Nếu bạn không chắc chắn có nên sử dụng array hay vector, rất có thể bạn nên sử dụng vector. [Chương 8][vectors]<!-- ignore --> thảo luận về vector chi tiết hơn.

Tuy nhiên, array hữu ích hơn khi bạn biết số phần tử sẽ không cần thay đổi. Ví dụ, nếu bạn đang sử dụng tên của các tháng trong một chương trình, bạn có thể sẽ sử dụng array thay vì vector vì bạn biết nó sẽ luôn chứa 12 phần tử:

```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
```

Bạn viết kiểu của array bằng cách sử dụng dấu ngoặc vuông với kiểu của mỗi phần tử, dấu chấm phẩy, và sau đó số phần tử trong array, như thế này:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Ở đây, `i32` là kiểu của mỗi phần tử. Sau dấu chấm phẩy, số `5` cho biết array chứa năm phần tử.

Bạn cũng có thể khởi tạo array để chứa cùng một giá trị cho mỗi phần tử bằng cách chỉ định giá trị ban đầu, theo sau là dấu chấm phẩy, và sau đó độ dài của array trong dấu ngoặc vuông, như được hiển thị ở đây:

```rust
let a = [3; 5];
```

Array có tên `a` sẽ chứa `5` phần tử mà tất cả sẽ được đặt thành giá trị `3` ban đầu. Điều này giống như viết `let a = [3, 3, 3, 3, 3];` nhưng theo cách ngắn gọn hơn.

<!-- Old headings. Do not remove or links may break. -->
<a id="accessing-array-elements"></a>

#### Truy cập Phần tử Array

Một array là một khối bộ nhớ đơn lẻ có kích thước cố định, đã biết có thể được cấp phát trên stack. Bạn có thể truy cập các phần tử của array bằng cách sử dụng indexing, như thế này:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-14-array-indexing/src/main.rs}}
```

Trong ví dụ này, biến có tên `first` sẽ nhận giá trị `1` vì đó là giá trị tại index `[0]` trong array. Biến có tên `second` sẽ nhận giá trị `2` từ index `[1]` trong array.

#### Truy cập Phần tử Array Không hợp lệ

Hãy xem điều gì xảy ra nếu bạn cố gắng truy cập một phần tử của array nằm ngoài cuối array. Giả sử bạn chạy code này, tương tự như trò chơi đoán số trong Chương 2, để lấy index của array từ người dùng:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,panics
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access/src/main.rs}}
```

Code này biên dịch thành công. Nếu bạn chạy code này bằng `cargo run` và nhập `0`, `1`, `2`, `3`, hoặc `4`, chương trình sẽ in ra giá trị tương ứng tại index đó trong array. Nếu thay vào đó bạn nhập một số ngoài cuối array, chẳng hạn như `10`, bạn sẽ thấy đầu ra như thế này:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access
cargo run
10
-->

```console
thread 'main' panicked at src/main.rs:19:19:
index out of bounds: the len is 5 but the index is 10
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Chương trình dẫn đến lỗi runtime tại điểm sử dụng giá trị không hợp lệ trong thao tác indexing. Chương trình thoát với thông báo lỗi và không thực thi câu lệnh `println!` cuối cùng. Khi bạn cố gắng truy cập một phần tử bằng cách sử dụng indexing, Rust sẽ kiểm tra rằng index mà bạn đã chỉ định nhỏ hơn độ dài array. Nếu index lớn hơn hoặc bằng độ dài, Rust sẽ panic. Kiểm tra này phải xảy ra tại runtime, đặc biệt trong trường hợp này, vì compiler không thể biết giá trị nào người dùng sẽ nhập khi họ chạy code sau đó.

Đây là một ví dụ về các nguyên tắc memory safety của Rust trong hành động. Trong nhiều ngôn ngữ cấp thấp, loại kiểm tra này không được thực hiện, và khi bạn cung cấp một index không chính xác, bộ nhớ không hợp lệ có thể được truy cập. Rust bảo vệ bạn chống lại loại lỗi này bằng cách thoát ngay lập tức thay vì cho phép truy cập bộ nhớ và tiếp tục. Chương 9 thảo luận thêm về xử lý lỗi của Rust và cách bạn có thể viết code dễ đọc, an toàn không panic cũng không cho phép truy cập bộ nhớ không hợp lệ.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[twos-complement]: https://en.wikipedia.org/wiki/Two%27s_complement
[control-flow]: ch03-05-control-flow.html#control-flow
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[stack-and-heap]: ch04-01-what-is-ownership.html#the-stack-and-the-heap
[vectors]: ch08-01-vectors.html
[unrecoverable-errors-with-panic]: ch09-01-unrecoverable-errors-with-panic.html
[appendix_b]: appendix-02-operators.md

<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>