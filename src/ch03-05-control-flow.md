## Luồng điều khiển

Khả năng chạy một số code tùy thuộc vào việc một điều kiện là `true` và khả năng chạy một số code lặp lại trong khi một điều kiện là `true` là các khối xây dựng cơ bản trong hầu hết các ngôn ngữ lập trình. Các cấu trúc phổ biến nhất cho phép bạn điều khiển luồng thực thi của code Rust là các biểu thức `if` và loops.

### Biểu thức `if`

Một biểu thức `if` cho phép bạn phân nhánh code của mình tùy thuộc vào các điều kiện. Bạn cung cấp một điều kiện và sau đó nói, "Nếu điều kiện này được đáp ứng, chạy khối code này. Nếu điều kiện không được đáp ứng, không chạy khối code này."

Tạo một dự án mới có tên _branches_ trong thư mục _projects_ của bạn để khám phá biểu thức `if`. Trong file _src/main.rs_, nhập như sau:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/src/main.rs}}
```

Tất cả các biểu thức `if` bắt đầu bằng từ khóa `if`, theo sau là một điều kiện. Trong trường hợp này, điều kiện kiểm tra xem biến `number` có giá trị nhỏ hơn 5 hay không. Chúng ta đặt khối code để thực thi nếu điều kiện là `true` ngay sau điều kiện bên trong dấu ngoặc nhọn. Các khối code liên quan đến các điều kiện trong biểu thức `if` đôi khi được gọi là _arms_ (nhánh), giống như các arms trong biểu thức `match` mà chúng ta đã thảo luận trong phần ["So sánh Dự đoán với Số Bí mật"][comparing-the-guess-to-the-secret-number]<!-- ignore --> của Chương 2.

Tùy chọn, chúng ta cũng có thể bao gồm một biểu thức `else`, mà chúng ta đã chọn làm ở đây, để cung cấp cho chương trình một khối code thay thế để thực thi nếu điều kiện đánh giá thành `false`. Nếu bạn không cung cấp biểu thức `else` và điều kiện là `false`, chương trình sẽ chỉ bỏ qua khối `if` và chuyển sang phần code tiếp theo.

Hãy thử chạy code này; bạn sẽ thấy đầu ra sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/output.txt}}
```

Hãy thử thay đổi giá trị của `number` thành một giá trị làm cho điều kiện `false` để xem điều gì xảy ra:

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/src/main.rs:here}}
```

Chạy chương trình lại, và xem đầu ra:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/output.txt}}
```

Cũng đáng lưu ý rằng điều kiện trong code này _phải_ là một `bool`. Nếu điều kiện không phải là `bool`, chúng ta sẽ nhận được lỗi. Ví dụ, hãy thử chạy code sau:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/src/main.rs}}
```

Điều kiện `if` đánh giá thành giá trị `3` lần này, và Rust ném một lỗi:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/output.txt}}
```

Lỗi cho biết rằng Rust mong đợi một `bool` nhưng nhận được một số nguyên. Không giống như các ngôn ngữ như Ruby và JavaScript, Rust sẽ không tự động cố gắng chuyển đổi các kiểu không phải Boolean sang Boolean. Bạn phải rõ ràng và luôn cung cấp `if` với một Boolean làm điều kiện của nó. Nếu chúng ta muốn khối code `if` chạy chỉ khi một số không bằng `0`, ví dụ, chúng ta có thể thay đổi biểu thức `if` thành như sau:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-29-if-not-equal-0/src/main.rs}}
```

Chạy code này sẽ in `number was something other than zero`.

#### Xử lý Nhiều Điều kiện với `else if`

Bạn có thể sử dụng nhiều điều kiện bằng cách kết hợp `if` và `else` trong biểu thức `else if`. Ví dụ:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/src/main.rs}}
```

Chương trình này có bốn đường dẫn có thể thực hiện. Sau khi chạy nó, bạn sẽ thấy đầu ra sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/output.txt}}
```

Khi chương trình này thực thi, nó kiểm tra từng biểu thức `if` lần lượt và thực thi phần thân đầu tiên mà điều kiện đánh giá thành `true`. Lưu ý rằng mặc dù 6 chia hết cho 2, chúng ta không thấy đầu ra `number is divisible by 2`, cũng như chúng ta không thấy văn bản `number is not divisible by 4, 3, or 2` từ khối `else`. Đó là vì Rust chỉ thực thi khối cho điều kiện `true` đầu tiên, và một khi nó tìm thấy một, nó thậm chí không kiểm tra phần còn lại.

Sử dụng quá nhiều biểu thức `else if` có thể làm lộn xộn code của bạn, vì vậy nếu bạn có nhiều hơn một, bạn có thể muốn refactor code của mình. Chương 6 mô tả một cấu trúc phân nhánh Rust mạnh mẽ gọi là `match` cho các trường hợp này.

#### Sử dụng `if` trong Câu lệnh `let`

Bởi vì `if` là một biểu thức, chúng ta có thể sử dụng nó ở bên phải của câu lệnh `let` để gán kết quả cho một biến, như trong Listing 3-2.

<Listing number="3-2" file-name="src/main.rs" caption="Gán kết quả của biểu thức `if` cho một biến">

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-02/src/main.rs}}
```

</Listing>

Biến `number` sẽ được gắn với một giá trị dựa trên kết quả của biểu thức `if`. Chạy code này để xem điều gì xảy ra:

```console
{{#include ../listings/ch03-common-programming-concepts/listing-03-02/output.txt}}
```

Hãy nhớ rằng các khối code đánh giá thành biểu thức cuối cùng trong chúng, và các số tự chúng cũng là biểu thức. Trong trường hợp này, giá trị của toàn bộ biểu thức `if` phụ thuộc vào khối code nào thực thi. Điều này có nghĩa là các giá trị có khả năng là kết quả từ mỗi arm của `if` phải có cùng kiểu; trong Listing 3-2, kết quả của cả arm `if` và arm `else` đều là số nguyên `i32`. Nếu các kiểu không khớp, như trong ví dụ sau, chúng ta sẽ nhận được lỗi:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/src/main.rs}}
```

Khi chúng ta cố gắng biên dịch code này, chúng ta sẽ nhận được lỗi. Các arms `if` và `else` có các kiểu giá trị không tương thích, và Rust chỉ ra chính xác nơi tìm vấn đề trong chương trình:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/output.txt}}
```

Biểu thức trong khối `if` đánh giá thành một số nguyên, và biểu thức trong khối `else` đánh giá thành một chuỗi. Điều này sẽ không hoạt động, bởi vì các biến phải có một kiểu duy nhất, và Rust cần biết chắc chắn tại compile time kiểu của biến `number` là gì. Biết kiểu của `number` cho phép compiler xác minh kiểu hợp lệ ở mọi nơi chúng ta sử dụng `number`. Rust sẽ không thể làm điều đó nếu kiểu của `number` chỉ được xác định tại runtime; compiler sẽ phức tạp hơn và sẽ đưa ra ít đảm bảo hơn về code nếu nó phải theo dõi nhiều kiểu giả định cho bất kỳ biến nào.

### Lặp lại với Loops

Thường hữu ích để thực thi một khối code nhiều lần. Để thực hiện tác vụ này, Rust cung cấp một số _loops_ (vòng lặp), sẽ chạy qua code bên trong thân vòng lặp đến cuối và sau đó bắt đầu ngay lập tức từ đầu. Để thử nghiệm với loops, hãy tạo một dự án mới có tên _loops_.

Rust có ba loại loops: `loop`, `while`, và `for`. Hãy thử từng loại một.

#### Lặp lại Code với `loop`

Từ khóa `loop` nói với Rust thực thi một khối code lặp đi lặp lại mãi mãi hoặc cho đến khi bạn nói rõ ràng nó dừng lại.

Ví dụ, thay đổi file _src/main.rs_ trong thư mục _loops_ của bạn để trông như thế này:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-loop/src/main.rs}}
```

Khi chúng ta chạy chương trình này, chúng ta sẽ thấy `again!` được in lặp đi lặp lại liên tục cho đến khi chúng ta dừng chương trình thủ công. Hầu hết các terminal hỗ trợ phím tắt bàn phím <kbd>ctrl</kbd>-<kbd>C</kbd> để ngắt một chương trình bị kẹt trong một vòng lặp liên tục. Hãy thử nó:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-32-loop
cargo run
CTRL-C
-->

```console
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.08s
     Running `target/debug/loops`
again!
again!
again!
again!
^Cagain!
```

Ký hiệu `^C` đại diện cho nơi bạn nhấn <kbd>ctrl</kbd>-<kbd>C</kbd>.

Bạn có thể thấy hoặc không thấy từ `again!` được in sau `^C`, tùy thuộc vào nơi code đang ở trong vòng lặp khi nó nhận được tín hiệu ngắt.

May mắn thay, Rust cũng cung cấp một cách để thoát khỏi vòng lặp bằng code. Bạn có thể đặt từ khóa `break` trong vòng lặp để nói với chương trình khi nào dừng thực thi vòng lặp. Nhớ lại rằng chúng ta đã làm điều này trong trò chơi đoán số trong phần ["Thoát Sau một Dự đoán Đúng"][quitting-after-a-correct-guess]<!-- ignore --> của Chương 2 để thoát chương trình khi người dùng thắng trò chơi bằng cách đoán đúng số.

Chúng ta cũng đã sử dụng `continue` trong trò chơi đoán số, trong một vòng lặp nó nói với chương trình bỏ qua bất kỳ code còn lại nào trong lần lặp này của vòng lặp và chuyển sang lần lặp tiếp theo.

#### Trả về Giá trị từ Loops

Một trong những công dụng của `loop` là thử lại một thao tác mà bạn biết có thể thất bại, chẳng hạn như kiểm tra xem một thread đã hoàn thành công việc của nó chưa. Bạn cũng có thể cần truyền kết quả của thao tác đó ra khỏi vòng lặp đến phần còn lại của code của bạn. Để làm điều này, bạn có thể thêm giá trị mà bạn muốn trả về sau biểu thức `break` mà bạn sử dụng để dừng vòng lặp; giá trị đó sẽ được trả về ra khỏi vòng lặp để bạn có thể sử dụng nó, như được hiển thị ở đây:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-33-return-value-from-loop/src/main.rs}}
```

Trước vòng lặp, chúng ta khai báo một biến có tên `counter` và khởi tạo nó thành `0`. Sau đó, chúng ta khai báo một biến có tên `result` để giữ giá trị được trả về từ vòng lặp. Trên mỗi lần lặp của vòng lặp, chúng ta thêm `1` vào biến `counter`, và sau đó kiểm tra xem `counter` có bằng `10` hay không. Khi nó bằng, chúng ta sử dụng từ khóa `break` với giá trị `counter * 2`. Sau vòng lặp, chúng ta sử dụng dấu chấm phẩy để kết thúc câu lệnh gán giá trị cho `result`. Cuối cùng, chúng ta in giá trị trong `result`, trong trường hợp này là `20`.

Bạn cũng có thể `return` từ bên trong vòng lặp. Trong khi `break` chỉ thoát khỏi vòng lặp hiện tại, `return` luôn thoát khỏi hàm hiện tại.

<!-- Old headings. Do not remove or links may break. -->
<a id="loop-labels-to-disambiguate-between-multiple-loops"></a>

#### Phân biệt với Loop Labels

Nếu bạn có các vòng lặp bên trong vòng lặp, `break` và `continue` áp dụng cho vòng lặp trong cùng nhất tại điểm đó. Bạn có thể tùy chọn chỉ định một _loop label_ (nhãn vòng lặp) trên vòng lặp mà sau đó bạn có thể sử dụng với `break` hoặc `continue` để chỉ định rằng các từ khóa đó áp dụng cho vòng lặp được gắn nhãn thay vì vòng lặp trong cùng nhất. Loop labels phải bắt đầu bằng dấu nháy đơn. Đây là một ví dụ với hai vòng lặp lồng nhau:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/src/main.rs}}
```

Vòng lặp bên ngoài có nhãn `'counting_up`, và nó sẽ đếm lên từ 0 đến 2. Vòng lặp bên trong không có nhãn đếm ngược từ 10 đến 9. `break` đầu tiên không chỉ định nhãn sẽ chỉ thoát khỏi vòng lặp bên trong. Câu lệnh `break 'counting_up;` sẽ thoát khỏi vòng lặp bên ngoài. Code này in:

```console
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/output.txt}}
```

<!-- Old headings. Do not remove or links may break. -->
<a id="conditional-loops-with-while"></a>

#### Tối ưu hóa Vòng lặp Có điều kiện với while

Một chương trình thường cần đánh giá một điều kiện trong vòng lặp. Trong khi điều kiện là `true`, vòng lặp chạy. Khi điều kiện không còn là `true`, chương trình gọi `break`, dừng vòng lặp. Có thể triển khai hành vi như thế này bằng cách sử dụng kết hợp `loop`, `if`, `else`, và `break`; bạn có thể thử điều đó ngay bây giờ trong chương trình, nếu bạn muốn. Tuy nhiên, pattern này quá phổ biến đến nỗi Rust có một cấu trúc ngôn ngữ tích hợp cho nó, được gọi là vòng lặp `while`. Trong Listing 3-3, chúng ta sử dụng `while` để lặp chương trình ba lần, đếm ngược mỗi lần, và sau đó, sau vòng lặp, in một thông báo và thoát.

<Listing number="3-3" file-name="src/main.rs" caption="Sử dụng vòng lặp `while` để chạy code trong khi điều kiện đánh giá thành `true`">

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-03/src/main.rs}}
```

</Listing>

Cấu trúc này loại bỏ rất nhiều lồng nhau sẽ cần thiết nếu bạn sử dụng `loop`, `if`, `else`, và `break`, và nó rõ ràng hơn. Trong khi điều kiện đánh giá thành `true`, code chạy; nếu không, nó thoát khỏi vòng lặp.

#### Lặp qua Collection với `for`

Bạn có thể chọn sử dụng cấu trúc `while` để lặp qua các phần tử của collection, chẳng hạn như array. Ví dụ, vòng lặp trong Listing 3-4 in mỗi phần tử trong array `a`.

<Listing number="3-4" file-name="src/main.rs" caption="Lặp qua mỗi phần tử của collection bằng cách sử dụng vòng lặp `while`">

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-04/src/main.rs}}
```

</Listing>

Ở đây, code đếm lên qua các phần tử trong array. Nó bắt đầu tại index `0` và sau đó lặp cho đến khi nó đạt đến index cuối cùng trong array (tức là khi `index < 5` không còn là `true`). Chạy code này sẽ in mỗi phần tử trong array:

```console
{{#include ../listings/ch03-common-programming-concepts/listing-03-04/output.txt}}
```

Tất cả năm giá trị array xuất hiện trong terminal, như mong đợi. Mặc dù `index` sẽ đạt giá trị `5` tại một số điểm, vòng lặp dừng thực thi trước khi cố gắng lấy giá trị thứ sáu từ array.

Tuy nhiên, cách tiếp cận này dễ gây lỗi; chúng ta có thể khiến chương trình panic nếu giá trị index hoặc điều kiện kiểm tra không chính xác. Ví dụ, nếu bạn thay đổi định nghĩa của array `a` để có bốn phần tử nhưng quên cập nhật điều kiện thành `while index < 4`, code sẽ panic. Nó cũng chậm, bởi vì compiler thêm code runtime để thực hiện kiểm tra điều kiện xem index có nằm trong giới hạn của array hay không trên mỗi lần lặp qua vòng lặp.

Như một lựa chọn ngắn gọn hơn, bạn có thể sử dụng vòng lặp `for` và thực thi một số code cho mỗi item trong collection. Vòng lặp `for` trông giống như code trong Listing 3-5.

<Listing number="3-5" file-name="src/main.rs" caption="Lặp qua mỗi phần tử của collection bằng cách sử dụng vòng lặp `for`">

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-05/src/main.rs}}
```

</Listing>

Khi chúng ta chạy code này, chúng ta sẽ thấy đầu ra giống như trong Listing 3-4. Quan trọng hơn, chúng ta đã tăng tính an toàn của code và loại bỏ cơ hội lỗi có thể xảy ra do vượt quá cuối array hoặc không đi đủ xa và bỏ lỡ một số item. Machine code được tạo từ vòng lặp `for` cũng có thể hiệu quả hơn vì index không cần được so sánh với độ dài của array ở mỗi lần lặp.

Sử dụng vòng lặp `for`, bạn sẽ không cần nhớ thay đổi bất kỳ code nào khác nếu bạn thay đổi số lượng giá trị trong array, như bạn sẽ phải làm với phương pháp được sử dụng trong Listing 3-4.

Tính an toàn và ngắn gọn của vòng lặp `for` làm cho chúng trở thành cấu trúc vòng lặp được sử dụng phổ biến nhất trong Rust. Ngay cả trong các tình huống mà bạn muốn chạy một số code một số lần nhất định, như trong ví dụ đếm ngược sử dụng vòng lặp `while` trong Listing 3-3, hầu hết Rustacean sẽ sử dụng vòng lặp `for`. Cách làm đó sẽ là sử dụng `Range`, được cung cấp bởi thư viện chuẩn, tạo ra tất cả các số trong dãy bắt đầu từ một số và kết thúc trước một số khác.

Đây là cách đếm ngược sẽ trông như thế nào bằng cách sử dụng vòng lặp `for` và một phương thức khác mà chúng ta chưa đề cập, `rev`, để đảo ngược range:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-34-for-range/src/main.rs}}
```

Code này tốt hơn một chút, phải không?

## Tóm tắt

Bạn đã làm được! Đây là một chương khá lớn: Bạn đã học về biến, kiểu dữ liệu scalar và compound, hàm, comments, biểu thức `if`, và loops! Để thực hành với các khái niệm được thảo luận trong chương này, hãy thử xây dựng các chương trình để thực hiện những việc sau:

- Chuyển đổi nhiệt độ giữa Fahrenheit và Celsius.
- Tạo số Fibonacci thứ *n*.
- In lời bài hát của bài hát Giáng sinh "The Twelve Days of Christmas," tận dụng sự lặp lại trong bài hát.

Khi bạn sẵn sàng để tiếp tục, chúng ta sẽ nói về một khái niệm trong Rust _không_ thường tồn tại trong các ngôn ngữ lập trình khác: ownership.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[quitting-after-a-correct-guess]: ch02-00-guessing-game-tutorial.html#quitting-after-a-correct-guess

<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>