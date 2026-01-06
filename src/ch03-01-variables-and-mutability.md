## Biến và Tính khả biến

Như đã đề cập trong phần ["Lưu trữ Giá trị với Biến"][storing-values-with-variables]<!-- ignore -->, theo mặc định, các biến là bất biến (immutable). Đây là một trong nhiều gợi ý mà Rust đưa ra để bạn viết code theo cách tận dụng tính an toàn và khả năng đồng thời dễ dàng mà Rust cung cấp. Tuy nhiên, bạn vẫn có tùy chọn để làm cho các biến của mình có thể thay đổi (mutable). Hãy khám phá cách và lý do Rust khuyến khích bạn ưu tiên tính bất biến và tại sao đôi khi bạn có thể muốn không sử dụng nó.

Khi một biến là bất biến, một khi một giá trị được gắn với một tên, bạn không thể thay đổi giá trị đó. Để minh họa điều này, hãy tạo một dự án mới có tên _variables_ trong thư mục _projects_ của bạn bằng cách sử dụng `cargo new variables`.

Sau đó, trong thư mục _variables_ mới của bạn, mở _src/main.rs_ và thay thế code của nó bằng code sau, code này sẽ chưa biên dịch được:

<span class="filename">Tên file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/src/main.rs}}
```

Lưu và chạy chương trình bằng `cargo run`. Bạn sẽ nhận được thông báo lỗi về lỗi bất biến, như được hiển thị trong đầu ra này:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/output.txt}}
```

Ví dụ này cho thấy cách compiler giúp bạn tìm lỗi trong các chương trình của mình. Lỗi compiler có thể gây bực bội, nhưng thực sự chúng chỉ có nghĩa là chương trình của bạn chưa an toàn thực hiện những gì bạn muốn nó làm; chúng _không_ có nghĩa là bạn không phải là một lập trình viên tốt! Các Rustacean có kinh nghiệm vẫn gặp lỗi compiler.

Bạn đã nhận được thông báo lỗi `` cannot assign twice to immutable variable `x` `` vì bạn đã cố gắng gán một giá trị thứ hai cho biến bất biến `x`.

Điều quan trọng là chúng ta nhận được lỗi compile-time khi chúng ta cố gắng thay đổi một giá trị được chỉ định là bất biến, bởi vì tình huống này có thể dẫn đến lỗi. Nếu một phần code của chúng ta hoạt động dựa trên giả định rằng một giá trị sẽ không bao giờ thay đổi và một phần khác của code thay đổi giá trị đó, có khả năng phần đầu tiên của code sẽ không làm những gì nó được thiết kế để làm. Nguyên nhân của loại lỗi này có thể khó theo dõi sau khi sự việc xảy ra, đặc biệt khi phần code thứ hai chỉ thay đổi giá trị _đôi khi_. Compiler Rust đảm bảo rằng khi bạn nói rằng một giá trị sẽ không thay đổi, nó thực sự sẽ không thay đổi, vì vậy bạn không phải tự mình theo dõi nó. Do đó, code của bạn dễ suy luận hơn.

Nhưng tính khả biến có thể rất hữu ích và có thể làm cho code dễ viết hơn. Mặc dù các biến là bất biến theo mặc định, bạn có thể làm cho chúng có thể thay đổi bằng cách thêm `mut` ở phía trước tên biến như bạn đã làm trong [Chương 2][storing-values-with-variables]<!-- ignore -->. Thêm `mut` cũng truyền đạt ý định cho những người đọc code trong tương lai bằng cách cho biết rằng các phần khác của code sẽ thay đổi giá trị của biến này.

Ví dụ, hãy thay đổi _src/main.rs_ thành như sau:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/src/main.rs}}
```

Khi chúng ta chạy chương trình bây giờ, chúng ta nhận được:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/output.txt}}
```

Chúng ta được phép thay đổi giá trị được gắn với `x` từ `5` thành `6` khi `mut` được sử dụng. Cuối cùng, quyết định có sử dụng tính khả biến hay không là tùy thuộc vào bạn và phụ thuộc vào những gì bạn nghĩ là rõ ràng nhất trong tình huống cụ thể đó.

<!-- Old headings. Do not remove or links may break. -->
<a id="constants"></a>

### Khai báo Hằng số

Giống như các biến bất biến, _hằng số_ (constants) là các giá trị được gắn với một tên và không được phép thay đổi, nhưng có một vài khác biệt giữa hằng số và biến.

Đầu tiên, bạn không được phép sử dụng `mut` với hằng số. Hằng số không chỉ bất biến theo mặc định—chúng luôn luôn bất biến. Bạn khai báo hằng số bằng cách sử dụng từ khóa `const` thay vì từ khóa `let`, và kiểu của giá trị _phải_ được chú thích. Chúng ta sẽ đề cập đến kiểu và chú thích kiểu trong phần tiếp theo, ["Kiểu dữ liệu"][data-types]<!-- ignore -->, vì vậy đừng lo lắng về chi tiết ngay bây giờ. Chỉ cần biết rằng bạn phải luôn chú thích kiểu.

Hằng số có thể được khai báo trong bất kỳ scope nào, bao gồm global scope, điều này làm cho chúng hữu ích cho các giá trị mà nhiều phần code cần biết.

Sự khác biệt cuối cùng là hằng số chỉ có thể được đặt thành một biểu thức hằng số, không phải kết quả của một giá trị chỉ có thể được tính toán tại runtime.

Đây là một ví dụ về khai báo hằng số:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Tên của hằng số là `THREE_HOURS_IN_SECONDS`, và giá trị của nó được đặt thành kết quả của việc nhân 60 (số giây trong một phút) với 60 (số phút trong một giờ) với 3 (số giờ chúng ta muốn đếm trong chương trình này). Quy ước đặt tên của Rust cho hằng số là sử dụng tất cả chữ hoa với dấu gạch dưới giữa các từ. Compiler có thể đánh giá một tập hợp hạn chế các thao tác tại compile time, điều này cho phép chúng ta chọn viết ra giá trị này theo cách dễ hiểu và xác minh hơn, thay vì đặt hằng số này thành giá trị 10,800. Xem [phần về đánh giá hằng số của Rust Reference][const-eval] để biết thêm thông tin về các thao tác có thể được sử dụng khi khai báo hằng số.

Hằng số có hiệu lực trong toàn bộ thời gian một chương trình chạy, trong scope mà chúng được khai báo. Thuộc tính này làm cho hằng số hữu ích cho các giá trị trong miền ứng dụng của bạn mà nhiều phần của chương trình có thể cần biết, chẳng hạn như số điểm tối đa mà bất kỳ người chơi nào của một trò chơi được phép kiếm được, hoặc tốc độ ánh sáng.

Đặt tên các giá trị hardcoded được sử dụng trong suốt chương trình của bạn như hằng số rất hữu ích trong việc truyền đạt ý nghĩa của giá trị đó cho những người bảo trì code trong tương lai. Nó cũng giúp chỉ có một nơi trong code của bạn mà bạn sẽ cần thay đổi nếu giá trị hardcoded cần được cập nhật trong tương lai.

### Shadowing

Như bạn đã thấy trong hướng dẫn trò chơi đoán số trong [Chương 2][comparing-the-guess-to-the-secret-number]<!-- ignore -->, bạn có thể khai báo một biến mới với cùng tên như một biến trước đó. Rustacean nói rằng biến đầu tiên bị _shadowed_ (che) bởi biến thứ hai, có nghĩa là biến thứ hai là những gì compiler sẽ thấy khi bạn sử dụng tên của biến. Thực tế, biến thứ hai che khuất biến đầu tiên, lấy bất kỳ việc sử dụng tên biến nào cho chính nó cho đến khi chính nó bị shadow hoặc scope kết thúc. Chúng ta có thể shadow một biến bằng cách sử dụng cùng tên biến và lặp lại việc sử dụng từ khóa `let` như sau:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/src/main.rs}}
```

Chương trình này đầu tiên gắn `x` với giá trị `5`. Sau đó, nó tạo một biến mới `x` bằng cách lặp lại `let x =`, lấy giá trị ban đầu và thêm `1` để giá trị của `x` là `6`. Sau đó, trong một scope bên trong được tạo với dấu ngoặc nhọn, câu lệnh `let` thứ ba cũng shadow `x` và tạo một biến mới, nhân giá trị trước đó với `2` để cho `x` một giá trị `12`. Khi scope đó kết thúc, shadow bên trong kết thúc và `x` trở lại thành `6`. Khi chúng ta chạy chương trình này, nó sẽ xuất ra như sau:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/output.txt}}
```

Shadowing khác với việc đánh dấu một biến là `mut` vì chúng ta sẽ nhận được lỗi compile-time nếu chúng ta vô tình cố gắng gán lại cho biến này mà không sử dụng từ khóa `let`. Bằng cách sử dụng `let`, chúng ta có thể thực hiện một vài phép biến đổi trên một giá trị nhưng biến vẫn bất biến sau khi các phép biến đổi đó hoàn thành.

Sự khác biệt khác giữa `mut` và shadowing là vì chúng ta đang tạo một biến mới một cách hiệu quả khi chúng ta sử dụng từ khóa `let` lại, chúng ta có thể thay đổi kiểu của giá trị nhưng tái sử dụng cùng một tên. Ví dụ, giả sử chương trình của chúng ta yêu cầu người dùng cho thấy họ muốn bao nhiêu khoảng trắng giữa một số văn bản bằng cách nhập các ký tự khoảng trắng, và sau đó chúng ta muốn lưu trữ đầu vào đó dưới dạng một số:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-04-shadowing-can-change-types/src/main.rs:here}}
```

Biến `spaces` đầu tiên là kiểu chuỗi (string), và biến `spaces` thứ hai là kiểu số. Shadowing do đó giúp chúng ta không phải nghĩ ra các tên khác nhau, chẳng hạn như `spaces_str` và `spaces_num`; thay vào đó, chúng ta có thể tái sử dụng tên đơn giản hơn `spaces`. Tuy nhiên, nếu chúng ta cố gắng sử dụng `mut` cho điều này, như được hiển thị ở đây, chúng ta sẽ nhận được lỗi compile-time:

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/src/main.rs:here}}
```

Lỗi nói rằng chúng ta không được phép thay đổi kiểu của một biến:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/output.txt}}
```

Bây giờ chúng ta đã khám phá cách các biến hoạt động, hãy xem xét các kiểu dữ liệu khác mà chúng có thể có.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[data-types]: ch03-02-data-types.html#data-types
[storing-values-with-variables]: ch02-00-guessing-game-tutorial.html#storing-values-with-variables
[const-eval]: ../reference/const_eval.html


<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>