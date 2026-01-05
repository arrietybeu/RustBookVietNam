# Lời Mở Đầu

> Lưu ý: Phiên bản sách này giống với [The Rust Programming Language][nsprust]
> có sẵn dưới dạng in ấn và định dạng ebook từ [No Starch Press][nsp].

[nsprust]: https://nostarch.com/rust-programming-language-3rd-edition
[nsp]: https://nostarch.com/

Chào mừng bạn đến với _The Rust Programming Language_, một cuốn sách giới thiệu về Rust.
Ngôn ngữ lập trình Rust giúp bạn viết phần mềm nhanh hơn và đáng tin cậy hơn.
Trong thiết kế ngôn ngữ lập trình, ergonomics cấp cao và kiểm soát cấp thấp thường xung đột với nhau;
Rust thách thức sự xung đột này. Bằng cách cân bằng khả năng kỹ thuật mạnh mẽ và trải nghiệm nhà phát triển tuyệt vời,
Rust cung cấp cho bạn tùy chọn để kiểm soát các chi tiết cấp thấp (chẳng hạn như cách sử dụng bộ nhớ)
mà không phải chịu đựng những rắc rối thường gặp phải với kiểm soát như vậy.

## Rust Được Thiết Kế Cho Ai?

Rust là lý tưởng cho nhiều người vì nhiều lý do khác nhau. Hãy xem xét một số nhóm quan trọng nhất.

### Các Đội Nhóm Nhà Phát Triển

Rust đang chứng minh rằng nó là một công cụ năng suất để cộng tác giữa các đội nhóm nhà phát triển lớn
với mức độ kiến thức lập trình hệ thống khác nhau. Mã cấp thấp dễ bị các lỗi vi tính,
những lỗi này chỉ có thể được phát hiện thông qua kiểm tra rộng rãi và xem xét code cẩn thận bởi các nhà phát triển có kinh nghiệm
trong hầu hết các ngôn ngữ khác. Trong Rust, trình biên dịch đóng vai trò như một gatekeeper
bằng cách từ chối biên dịch mã có những lỗi khó nắm bắt này, bao gồm các lỗi về concurrency.
Bằng cách làm việc cùng với trình biên dịch, đội nhóm có thể dành thời gian tập trung vào logic của chương trình
thay vì theo đuổi các lỗi.

Rust cũng mang các công cụ nhà phát triển hiện đại vào thế giới lập trình hệ thống:

- Cargo, công cụ quản lý phụ thuộc và xây dựng tích hợp, làm cho việc thêm,
  biên dịch và quản lý phụ thuộc trở nên dễ dàng và nhất quán trên toàn bộ hệ sinh thái Rust.
- Công cụ định dạng `rustfmt` đảm bảo phong cách mã hóa nhất quán giữa các nhà phát triển.
- Rust Language Server cung cấp tích hợp môi trường phát triển tích hợp (IDE)
  để hoàn thành code và hiển thị thông báo lỗi nội tuyến.

Bằng cách sử dụng các công cụ này và những công cụ khác trong hệ sinh thái Rust,
các nhà phát triển có thể năng suất cao khi viết mã cấp hệ thống.

### Sinh Viên

Rust dành cho sinh viên và những người quan tâm đến việc tìm hiểu về các khái niệm hệ thống.
Sử dụng Rust, nhiều người đã học được các chủ đề như phát triển hệ điều hành.
Cộng đồng rất hoan nghênh và sẵn sàng trả lời các câu hỏi của sinh viên.
Thông qua các nỗ lực như cuốn sách này, các đội Rust muốn làm cho các khái niệm hệ thống
dễ tiếp cận hơn cho nhiều người, đặc biệt là những người mới bắt đầu lập trình.

### Các Công Ty

Hàng trăm công ty, cả lớn và nhỏ, sử dụng Rust trong môi trường sản xuất cho nhiều tác vụ khác nhau,
bao gồm công cụ dòng lệnh, dịch vụ web, công cụ DevOps, thiết bị nhúng, phân tích và chuyển mã hóa âm thanh và video,
tiền điện tử, sinh học thông tin, động cơ tìm kiếm, ứng dụng Internet of Things, machine learning,
và thậm chí là các phần chính của trình duyệt web Firefox.

### Những Nhà Phát Triển Phần Mềm Mã Mở

Rust là dành cho những người muốn xây dựng ngôn ngữ lập trình Rust, cộng đồng,
công cụ nhà phát triển và thư viện. Chúng tôi rất muốn bạn đóng góp cho ngôn ngữ Rust.

### Những Người Đánh Giá Cao Tốc Độ và Sự Ổn Định

Rust là dành cho những người khao khát tốc độ và sự ổn định trong một ngôn ngữ lập trình.
Khi nói đến tốc độ, chúng tôi có nghĩa là cả cách mã Rust có thể chạy nhanh
và tốc độ mà Rust cho phép bạn viết các chương trình. Kiểm tra của trình biên dịch Rust
đảm bảo sự ổn định thông qua bổ sung tính năng và tái cấu trúc.
Điều này trái ngược với mã legacy dễ vỡ trong các ngôn ngữ không có các kiểm tra này,
những mã mà các nhà phát triển thường sợ sửa đổi. Bằng cách phấn đấu cho các trừu tượng chi phí không
—những tính năng cấp cao hơn được biên dịch thành mã cấp thấp nhanh như mã được viết thủ công—
Rust nỗ lực để làm cho mã an toàn cũng là mã nhanh.

Ngôn ngữ Rust hy vọng hỗ trợ nhiều người dùng khác; những người được đề cập ở đây
chỉ là một số bên liên quan lớn nhất. Nhìn chung, tham vọng lớn nhất của Rust
là loại bỏ những sự đánh đổi mà các lập trình viên đã chấp nhận trong hàng thập kỷ
bằng cách cung cấp an toàn _và_ năng suất, tốc độ _và_ ergonomics.
Hãy thử Rust và xem liệu những lựa chọn của nó có phù hợp với bạn không.

## Cuốn Sách Này Dành Cho Ai?

Cuốn sách này giả định rằng bạn đã viết mã trong một ngôn ngữ lập trình khác,
nhưng nó không đưa ra bất kỳ giả định nào về ngôn ngữ nào. Chúng tôi đã cố gắng làm cho tài liệu
dễ tiếp cận đối với những người từ nhiều nền tảng lập trình khác nhau.
Chúng tôi không dành nhiều thời gian để nói về lập trình _là gì_ hoặc cách suy nghĩ về nó.
Nếu bạn hoàn toàn mới bắt đầu với lập trình, bạn sẽ được phục vụ tốt hơn
bằng cách đọc một cuốn sách cung cấp cụ thể một phần giới thiệu về lập trình.

## Cách Sử Dụng Cuốn Sách Này

Nói chung, cuốn sách này giả định rằng bạn đang đọc nó theo thứ tự từ đầu đến cuối.
Các chương sau xây dựng dựa trên các khái niệm trong các chương trước,
và các chương trước có thể không đi sâu vào chi tiết về một chủ đề cụ thể
nhưng sẽ xem xét lại chủ đề đó trong một chương sau.

Bạn sẽ tìm thấy hai loại chương trong cuốn sách này: các chương khái niệm và các chương dự án.
Trong các chương khái niệm, bạn sẽ học về một khía cạnh của Rust.
Trong các chương dự án, chúng tôi sẽ xây dựng các chương trình nhỏ cùng nhau,
áp dụng những gì bạn đã học cho đến nay. Chương 2, Chương 12 và Chương 21 là các chương dự án;
phần còn lại là các chương khái niệm.

**Chương 1** giải thích cách cài đặt Rust, cách viết chương trình "Hello, world!" và cách sử dụng Cargo,
công cụ quản lý gói và xây dựng của Rust. **Chương 2** là một giới thiệu thực tế
về viết chương trình trong Rust, giúp bạn xây dựng một trò chơi đoán số.
Ở đây, chúng tôi bao gồm các khái niệm ở mức cao, và các chương sau sẽ cung cấp chi tiết bổ sung.
Nếu bạn muốn bắt tay vào việc ngay lập tức, Chương 2 là nơi dành cho bạn.
Nếu bạn là một người học tập đặc biệt cẩn thận người thích học mọi chi tiết trước khi tiếp tục,
bạn có thể muốn bỏ qua Chương 2 và đi thẳng đến **Chương 3**, bao gồm các tính năng Rust
tương tự như tính năng của các ngôn ngữ lập trình khác;
sau đó, bạn có thể quay lại Chương 2 khi muốn làm việc trên một dự án
áp dụng các chi tiết bạn đã học.

Trong **Chương 4**, bạn sẽ tìm hiểu về hệ thống ownership của Rust. **Chương 5**
thảo luận về structs và methods. **Chương 6** bao gồm enums, các biểu thức `match`
và các cấu trúc kiểm soát luồng `if let` và `let...else`. Bạn sẽ sử dụng structs
và enums để tạo các kiểu tùy chỉnh.

Trong **Chương 7**, bạn sẽ tìm hiểu về hệ thống module của Rust
và các quy tắc privacy để tổ chức mã và ứng dụng lập trình (API) công khai của nó.
**Chương 8** thảo luận về một số cấu trúc dữ liệu collection phổ biến mà thư viện tiêu chuẩn cung cấp:
vectors, strings và hash maps. **Chương 9** khám phá triết lý và kỹ thuật xử lý lỗi của Rust.

**Chương 10** đi sâu vào generics, traits và lifetimes, cung cấp cho bạn sức mạnh
để định nghĩa mã áp dụng cho nhiều kiểu. **Chương 11** hoàn toàn về testing,
điều này thậm chí với các bảo đảm an toàn của Rust vẫn cần thiết để đảm bảo rằng logic chương trình của bạn là chính xác.
Trong **Chương 12**, chúng tôi sẽ xây dựng triển khai của chúng tôi cho một tập con tính năng từ công cụ dòng lệnh `grep`
tìm kiếm văn bản trong các tệp. Đối với điều này, chúng tôi sẽ sử dụng nhiều khái niệm
mà chúng tôi đã thảo luận trong các chương trước.

**Chương 13** khám phá closures và iterators: các tính năng của Rust
xuất phát từ các ngôn ngữ lập trình hàm. Trong **Chương 14**, chúng tôi sẽ xem xét Cargo chi tiết hơn
và nói về các best practices để chia sẻ thư viện của bạn với người khác.
**Chương 15** thảo luận về smart pointers mà thư viện tiêu chuẩn cung cấp
và các traits cho phép chức năng của chúng.

Trong **Chương 16**, chúng tôi sẽ thực hiện các mô hình lập trình đồng thời khác nhau
và nói về cách Rust giúp bạn lập trình với nhiều threads một cách không sợ hãi.
Trong **Chương 17**, chúng tôi xây dựng dựa trên đó bằng cách khám phá cú pháp async và await của Rust,
cùng với tasks, futures và streams, và mô hình concurrency nhẹ mà chúng cho phép.

**Chương 18** xem xét cách các idioms của Rust so sánh với các nguyên tắc lập trình hướng đối tượng
mà bạn có thể quen thuộc. **Chương 19** là một tham chiếu về patterns và pattern matching,
đây là những cách mạnh mẽ để diễn đạt ý tưởng trong toàn bộ các chương trình Rust.
**Chương 20** chứa một loạt các chủ đề nâng cao đáng quan tâm,
bao gồm unsafe Rust, macros và thêm về lifetimes, traits, types, functions và closures.

Trong **Chương 21**, chúng tôi sẽ hoàn thành một dự án trong đó chúng tôi sẽ triển khai
một web server multithreaded cấp thấp!

Cuối cùng, một số phụ lục chứa thông tin hữu ích về ngôn ngữ dưới dạng tham chiếu.
**Phụ lục A** bao gồm các keywords của Rust, **Phụ lục B** bao gồm các operators và ký hiệu của Rust,
**Phụ lục C** bao gồm các traits có thể dẫn xuất được cung cấp bởi thư viện tiêu chuẩn,
**Phụ lục D** bao gồm một số công cụ phát triển hữu ích, và **Phụ lục E** giải thích các Rust editions.
Trong **Phụ lục F**, bạn có thể tìm thấy các bản dịch của cuốn sách,
và trong **Phụ lục G** chúng tôi sẽ bao gồm cách Rust được tạo ra và Rust nightly là gì.

Không có cách sai để đọc cuốn sách này: Nếu bạn muốn bỏ qua trước, hãy làm!
Bạn có thể phải quay lại các chương trước nếu gặp bất kỳ nhầm lẫn nào.
Nhưng hãy làm bất cứ điều gì phù hợp với bạn.

<span id="ferris"></span>

Một phần quan trọng của quá trình học Rust là học cách đọc các thông báo lỗi mà trình biên dịch hiển thị:
Những thông báo này sẽ hướng dẫn bạn tới mã hoạt động.
Như vậy, chúng tôi sẽ cung cấp nhiều ví dụ không biên dịch được cùng với thông báo lỗi
mà trình biên dịch sẽ hiển thị cho bạn trong mỗi tình huống.
Hãy biết rằng nếu bạn nhập và chạy một ví dụ ngẫu nhiên, nó có thể không biên dịch được!
Hãy chắc chắn đọc văn bản xung quanh để xem liệu ví dụ bạn đang cố gắng chạy
có được dự định là lỗi hay không. Trong hầu hết các trường hợp, chúng tôi sẽ dẫn bạn
đến phiên bản đúng của bất kỳ mã nào không biên dịch được.
Ferris cũng sẽ giúp bạn phân biệt mã không dự định hoạt động:

| Ferris                                                                                                           | Ý Nghĩa                                          |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| <img src="img/ferris/does_not_compile.svg" class="ferris-explain" alt="Ferris with a question mark"/>            | Mã này không biên dịch được!                     |
| <img src="img/ferris/panics.svg" class="ferris-explain" alt="Ferris throwing up their hands"/>                   | Mã này bị panic!                                 |
| <img src="img/ferris/not_desired_behavior.svg" class="ferris-explain" alt="Ferris with one claw up, shrugging"/> | Mã này không tạo ra hành vi mong muốn.           |

Trong hầu hết các trường hợp, chúng tôi sẽ dẫn bạn đến phiên bản đúng
của bất kỳ mã nào không biên dịch được.

## Mã Nguồn

Các tệp nguồn từ đó cuốn sách này được tạo có thể được tìm thấy trên
[GitHub][book].

[book]: https://github.com/rust-lang/book/tree/main/src
