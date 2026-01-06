## Functions

Functions (hàm) phổ biến trong code Rust. Bạn đã thấy một trong những hàm quan trọng nhất trong ngôn ngữ: hàm `main`, là điểm vào của nhiều chương trình. Bạn cũng đã thấy từ khóa `fn`, cho phép bạn khai báo các hàm mới.

Code Rust sử dụng _snake case_ như phong cách quy ước cho tên hàm và biến, trong đó tất cả chữ cái đều viết thường và dấu gạch dưới phân tách các từ. Đây là một chương trình chứa một ví dụ định nghĩa hàm:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-16-functions/src/main.rs}}
```

Chúng ta định nghĩa một hàm trong Rust bằng cách nhập `fn` theo sau là tên hàm và một bộ dấu ngoặc đơn. Các dấu ngoặc nhọn cho compiler biết nơi thân hàm bắt đầu và kết thúc.

Chúng ta có thể gọi bất kỳ hàm nào chúng ta đã định nghĩa bằng cách nhập tên của nó theo sau là một bộ dấu ngoặc đơn. Bởi vì `another_function` được định nghĩa trong chương trình, nó có thể được gọi từ bên trong hàm `main`. Lưu ý rằng chúng ta định nghĩa `another_function` _sau_ hàm `main` trong code nguồn; chúng ta cũng có thể định nghĩa nó trước. Rust không quan tâm nơi bạn định nghĩa các hàm của mình, chỉ cần chúng được định nghĩa ở đâu đó trong một scope có thể được thấy bởi người gọi.

Hãy bắt đầu một dự án binary mới có tên _functions_ để khám phá hàm sâu hơn. Đặt ví dụ `another_function` vào _src/main.rs_ và chạy nó. Bạn sẽ thấy đầu ra sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-16-functions/output.txt}}
```

Các dòng thực thi theo thứ tự chúng xuất hiện trong hàm `main`. Đầu tiên thông báo "Hello, world!" được in, và sau đó `another_function` được gọi và thông báo của nó được in.

### Parameters

Chúng ta có thể định nghĩa các hàm để có _parameters_ (tham số), là các biến đặc biệt là một phần của chữ ký hàm. Khi một hàm có parameters, bạn có thể cung cấp cho nó các giá trị cụ thể cho các parameters đó. Về mặt kỹ thuật, các giá trị cụ thể được gọi là _arguments_ (đối số), nhưng trong cuộc trò chuyện thông thường, mọi người có xu hướng sử dụng các từ _parameter_ và _argument_ thay thế cho nhau cho các biến trong định nghĩa hàm hoặc các giá trị cụ thể được truyền vào khi bạn gọi một hàm.

Trong phiên bản này của `another_function`, chúng ta thêm một parameter:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/src/main.rs}}
```

Hãy thử chạy chương trình này; bạn sẽ nhận được đầu ra sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/output.txt}}
```

Khai báo của `another_function` có một parameter có tên `x`. Kiểu của `x` được chỉ định là `i32`. Khi chúng ta truyền `5` vào `another_function`, macro `println!` đặt `5` nơi cặp dấu ngoặc nhọn chứa `x` trong chuỗi định dạng.

Trong chữ ký hàm, bạn _phải_ khai báo kiểu của mỗi parameter. Đây là một quyết định có chủ ý trong thiết kế của Rust: Yêu cầu chú thích kiểu trong định nghĩa hàm có nghĩa là compiler gần như không bao giờ cần bạn sử dụng chúng ở nơi khác trong code để tìm ra kiểu bạn muốn. Compiler cũng có thể đưa ra thông báo lỗi hữu ích hơn nếu nó biết các kiểu mà hàm mong đợi.

Khi định nghĩa nhiều parameters, hãy phân tách các khai báo parameter bằng dấu phẩy, như thế này:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/src/main.rs}}
```

Ví dụ này tạo một hàm có tên `print_labeled_measurement` với hai parameters. Parameter đầu tiên có tên `value` và là `i32`. Thứ hai có tên `unit_label` và là kiểu `char`. Hàm sau đó in văn bản chứa cả `value` và `unit_label`.

Hãy thử chạy code này. Thay thế chương trình hiện tại trong file _src/main.rs_ của dự án _functions_ của bạn bằng ví dụ trước đó và chạy nó bằng `cargo run`:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/output.txt}}
```

Bởi vì chúng ta gọi hàm với `5` làm giá trị cho `value` và `'h'` làm giá trị cho `unit_label`, đầu ra chương trình chứa các giá trị đó.

### Statements and Expressions

Thân hàm được tạo thành từ một chuỗi các statements (câu lệnh) tùy chọn kết thúc bằng một expression (biểu thức). Cho đến nay, các hàm chúng ta đã đề cập không bao gồm một expression kết thúc, nhưng bạn đã thấy một expression như một phần của statement. Bởi vì Rust là một ngôn ngữ dựa trên expression, đây là một sự phân biệt quan trọng cần hiểu. Các ngôn ngữ khác không có sự phân biệt tương tự, vì vậy hãy xem statements và expressions là gì và cách sự khác biệt của chúng ảnh hưởng đến thân của các hàm.

- _Statements_ (Câu lệnh) là các hướng dẫn thực hiện một số hành động và không trả về một giá trị.
- _Expressions_ (Biểu thức) đánh giá thành một giá trị kết quả.

Hãy xem một số ví dụ.

Chúng ta thực sự đã sử dụng statements và expressions. Tạo một biến và gán giá trị cho nó với từ khóa `let` là một statement. Trong Listing 3-1, `let y = 6;` là một statement.

<Listing number="3-1" file-name="src/main.rs" caption="Khai báo hàm `main` chứa một statement">

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-01/src/main.rs}}
```

</Listing>

Định nghĩa hàm cũng là statements; toàn bộ ví dụ trước đó là một statement trong chính nó. (Như chúng ta sẽ thấy ngay sau đó, gọi một hàm không phải là statement, mặc dù.)

Statements không trả về giá trị. Do đó, bạn không thể gán một statement `let` cho một biến khác, như code sau cố gắng làm; bạn sẽ nhận được lỗi:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/src/main.rs}}
```

Khi bạn chạy chương trình này, lỗi bạn sẽ nhận được trông như thế này:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/output.txt}}
```

Statement `let y = 6` không trả về giá trị, vì vậy không có gì để `x` gắn vào. Điều này khác với những gì xảy ra trong các ngôn ngữ khác, chẳng hạn như C và Ruby, nơi phép gán trả về giá trị của phép gán. Trong các ngôn ngữ đó, bạn có thể viết `x = y = 6` và có cả `x` và `y` có giá trị `6`; đó không phải trường hợp trong Rust.

Expressions đánh giá thành một giá trị và tạo nên phần lớn phần còn lại của code mà bạn sẽ viết trong Rust. Hãy xem xét một phép toán toán học, chẳng hạn như `5 + 6`, là một expression đánh giá thành giá trị `11`. Expressions có thể là một phần của statements: Trong Listing 3-1, `6` trong statement `let y = 6;` là một expression đánh giá thành giá trị `6`. Gọi một hàm là một expression. Gọi một macro là một expression. Một block scope mới được tạo với dấu ngoặc nhọn là một expression, ví dụ:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-20-blocks-are-expressions/src/main.rs}}
```

Expression này:

```rust,ignore
{
    let x = 3;
    x + 1
}
```

là một block, trong trường hợp này, đánh giá thành `4`. Giá trị đó được gắn với `y` như một phần của statement `let`. Lưu ý dòng `x + 1` không có dấu chấm phẩy ở cuối, không giống như hầu hết các dòng bạn đã thấy cho đến nay. Expressions không bao gồm dấu chấm phẩy kết thúc. Nếu bạn thêm dấu chấm phẩy vào cuối một expression, bạn biến nó thành một statement, và nó sau đó sẽ không trả về giá trị. Hãy ghi nhớ điều này khi bạn khám phá giá trị trả về hàm và expressions tiếp theo.

### Functions with Return Values

Hàm có thể trả về giá trị cho code gọi chúng. Chúng ta không đặt tên cho giá trị trả về, nhưng chúng ta phải khai báo kiểu của chúng sau một mũi tên (`->`). Trong Rust, giá trị trả về của hàm đồng nghĩa với giá trị của expression cuối cùng trong block của thân hàm. Bạn có thể trả về sớm từ một hàm bằng cách sử dụng từ khóa `return` và chỉ định một giá trị, nhưng hầu hết các hàm trả về expression cuối cùng một cách ngầm định. Đây là một ví dụ về một hàm trả về một giá trị:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/src/main.rs}}
```

Không có lời gọi hàm, macro, hoặc thậm chí statements `let` trong hàm `five`—chỉ có số `5` một mình. Đó là một hàm hoàn toàn hợp lệ trong Rust. Lưu ý rằng kiểu trả về của hàm cũng được chỉ định, như `-> i32`. Hãy thử chạy code này; đầu ra sẽ trông như thế này:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/output.txt}}
```

`5` trong `five` là giá trị trả về của hàm, đó là lý do tại sao kiểu trả về là `i32`. Hãy kiểm tra điều này chi tiết hơn. Có hai điểm quan trọng: Đầu tiên, dòng `let x = five();` cho thấy chúng ta đang sử dụng giá trị trả về của một hàm để khởi tạo một biến. Bởi vì hàm `five` trả về `5`, dòng đó giống như sau:

```rust
let x = 5;
```

Thứ hai, hàm `five` không có parameters và định nghĩa kiểu của giá trị trả về, nhưng thân của hàm là một `5` cô đơn không có dấu chấm phẩy vì nó là một expression mà giá trị của nó chúng ta muốn trả về.

Hãy xem một ví dụ khác:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-22-function-parameter-and-return/src/main.rs}}
```

Chạy code này sẽ in `The value of x is: 6`. Nhưng điều gì xảy ra nếu chúng ta đặt dấu chấm phẩy ở cuối dòng chứa `x + 1`, thay đổi nó từ một expression thành một statement?

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/src/main.rs}}
```

Biên dịch code này sẽ tạo ra lỗi, như sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/output.txt}}
```

Thông báo lỗi chính, `mismatched types`, tiết lộ vấn đề cốt lõi với code này. Định nghĩa của hàm `plus_one` nói rằng nó sẽ trả về một `i32`, nhưng statements không đánh giá thành giá trị, được biểu thị bởi `()`, kiểu unit. Do đó, không có gì được trả về, điều này mâu thuẫn với định nghĩa hàm và dẫn đến lỗi. Trong đầu ra này, Rust cung cấp thông báo để có thể giúp khắc phục vấn đề này: Nó đề xuất loại bỏ dấu chấm phẩy, điều này sẽ sửa lỗi.

<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>