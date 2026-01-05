## Cài Đặt

Bước đầu tiên là cài đặt Rust. Chúng tôi sẽ tải xuống Rust thông qua `rustup`,
một công cụ dòng lệnh để quản lý các phiên bản Rust và các công cụ liên kết.
Bạn sẽ cần một kết nối internet để tải xuống.

> Lưu ý: Nếu vì lý do nào đó bạn không muốn sử dụng `rustup`,
> vui lòng xem [trang Phương Pháp Cài Đặt Rust Khác][otherinstall] để biết thêm tùy chọn.

Các bước sau cài đặt phiên bản ổn định mới nhất của trình biên dịch Rust.
Các bảo đảm ổn định của Rust đảm bảo rằng tất cả các ví dụ trong sách
biên dịch được sẽ tiếp tục biên dịch được với các phiên bản Rust mới hơn.
Đầu ra có thể khác nhau một chút giữa các phiên bản vì Rust thường cải thiện
các thông báo lỗi và cảnh báo. Nói cách khác, bất kỳ phiên bản Rust ổn định mới hơn
nào bạn cài đặt bằng các bước này sẽ hoạt động như mong đợi với nội dung của cuốn sách này.

> ### Ký Hiệu Dòng Lệnh
>
> Trong chương này và xuyên suốt cuốn sách, chúng tôi sẽ hiển thị một số lệnh được sử dụng trong terminal.
> Các dòng mà bạn nên nhập vào terminal đều bắt đầu với `$`. Bạn không cần nhập ký tự `$`;
> đó là dấu nhắc dòng lệnh được hiển thị để chỉ ra sự bắt đầu của mỗi lệnh.
> Các dòng không bắt đầu với `$` thường hiển thị kết quả của lệnh trước đó.
> Ngoài ra, các ví dụ dành riêng cho PowerShell sẽ sử dụng `>` thay vì `$`.

### Cài Đặt `rustup` trên Linux hoặc macOS

Nếu bạn đang sử dụng Linux hoặc macOS, hãy mở terminal và nhập lệnh sau:

```console
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Lệnh này sẽ tải xuống một tập lệnh và bắt đầu cài đặt công cụ `rustup`,
công cụ này sẽ cài đặt phiên bản ổn định mới nhất của Rust. Bạn có thể được yêu cầu
nhập mật khẩu của mình. Nếu cài đặt thành công, dòng sau sẽ xuất hiện:

```text
Rust is installed now. Great!
```

Bạn cũng sẽ cần một _liên kết_, đây là một chương trình mà Rust sử dụng để kết hợp các
đầu ra đã biên dịch của nó thành một tệp. Có thể bạn đã có một cái. Nếu bạn gặp lỗi
liên kết, bạn nên cài đặt một trình biên dịch C, thường thì nó sẽ bao gồm một
liên kết. Một trình biên dịch C cũng rất hữu ích vì một số gói Rust phổ biến phụ thuộc vào
mã C và sẽ cần một trình biên dịch C.

Trên macOS, bạn có thể có được trình biên dịch C bằng cách chạy:

```console
$ xcode-select --install
```

Người dùng Linux thường nên cài đặt GCC hoặc Clang, theo tài liệu của
phân phối của họ. Ví dụ, nếu bạn sử dụng Ubuntu, bạn có thể cài đặt
gói `build-essential`.

### Cài Đặt `rustup` trên Windows

Trên Windows, hãy truy cập [https://www.rust-lang.org/tools/install][install]<!-- ignore
--> và làm theo hướng dẫn để cài đặt Rust. Vào một thời điểm nào đó trong quá trình
cài đặt, bạn sẽ được nhắc cài đặt Visual Studio. Điều này cung cấp một
liên kết và các thư viện gốc cần thiết để biên dịch chương trình. Nếu bạn cần thêm
trợ giúp với bước này, hãy xem
[https://rust-lang.github.io/rustup/installation/windows-msvc.html][msvc]<!--
ignore -->.

Phần còn lại của cuốn sách này sử dụng các lệnh hoạt động trong cả _cmd.exe_ và PowerShell.
Nếu có sự khác biệt cụ thể, chúng tôi sẽ giải thích cách sử dụng.

### Khắc Phục Sự Cố

Để kiểm tra xem bạn đã cài đặt Rust đúng cách chưa, hãy mở một shell và nhập dòng lệnh này:

```console
$ rustc --version
```

Bạn sẽ thấy số phiên bản, băm cam kết và ngày cam kết của phiên bản ổn định mới nhất
đã được phát hành, theo định dạng sau:

```text
rustc x.y.z (abcabcabc yyyy-mm-dd)
```

Nếu bạn thấy thông tin này, bạn đã cài đặt Rust thành công! Nếu bạn không thấy
thông tin này, hãy kiểm tra xem Rust có trong biến hệ thống `%PATH%` của bạn không, như
sau.

Trong Windows CMD, sử dụng:

```console
> echo %PATH%
```

Trong PowerShell, sử dụng:

```powershell
> echo $env:Path
```

Trong Linux và macOS, sử dụng:

```console
$ echo $PATH
```

Nếu mọi thứ đều chính xác và Rust vẫn không hoạt động, có một số nơi bạn có thể nhận được trợ giúp.
Tìm hiểu cách liên lạc với các Rustaceans khác (một biệt danh ngớ ngẩn mà chúng tôi gọi
mình) trên [trang cộng đồng][community].

### Cập Nhật và Gỡ Cài Đặt

Khi Rust được cài đặt qua `rustup`, việc cập nhật lên phiên bản mới được phát hành là
rất dễ dàng. Từ shell của bạn, chạy tập lệnh cập nhật sau:

```console
$ rustup update
```

Để gỡ cài đặt Rust và `rustup`, hãy chạy tập lệnh gỡ cài đặt sau từ shell của bạn:

```console
$ rustup self uninstall
```

<!-- Old headings. Do not remove or links may break. -->
<a id="local-documentation"></a>

### Đọc Tài Liệu Cục Bộ

Việc cài đặt Rust cũng bao gồm một bản sao cục bộ của tài liệu để bạn có thể đọc
ngoại tuyến. Chạy `rustup doc` để mở tài liệu cục bộ trong trình duyệt của bạn.

Bất cứ khi nào một kiểu hoặc hàm được cung cấp bởi thư viện chuẩn và bạn không chắc
nó hoạt động như thế nào hoặc cách sử dụng nó, hãy sử dụng tài liệu lập trình ứng dụng
(API) để tìm hiểu!

<!-- Old headings. Do not remove or links may break. -->
<a id="text-editors-and-integrated-development-environments"></a>

### Sử Dụng Trình Soạn Thảo Văn Bản và IDE

Cuốn sách này không đưa ra giả định nào về công cụ bạn sử dụng để viết mã Rust.
Hầu hết mọi trình soạn thảo văn bản đều có thể hoàn thành công việc! Tuy nhiên, nhiều trình soạn thảo văn bản và
môi trường phát triển tích hợp (IDEs) có hỗ trợ tích hợp cho Rust. Bạn
luôn có thể tìm thấy danh sách khá đầy đủ về nhiều trình soạn thảo và IDE trên [trang công cụ
][tools] trên trang web của Rust.

### Làm Việc Ngoại Tuyến Với Cuốn Sách Này

Trong một số ví dụ, chúng tôi sẽ sử dụng các gói Rust ngoài thư viện chuẩn. Để
làm việc thông qua những ví dụ đó, bạn sẽ cần phải có kết nối internet
hoặc đã tải xuống các phụ thuộc đó trước. Để tải xuống các
phụ thuộc đó trước, bạn có thể chạy các lệnh sau. (Chúng tôi sẽ giải thích
`cargo` là gì và mỗi lệnh này làm gì chi tiết hơn sau.)

```console
$ cargo new get-dependencies
$ cd get-dependencies
$ cargo add rand@0.8.5 trpl@0.2.0
```

Điều này sẽ lưu vào bộ nhớ cache các tệp tải xuống cho các gói này vì vậy bạn sẽ không cần phải
tải xuống chúng sau này. Khi bạn đã chạy lệnh này, bạn không cần phải giữ lại thư mục
`get-dependencies`. Nếu bạn đã chạy lệnh này, bạn có thể sử dụng cờ `--offline` với tất cả các lệnh `cargo`
trong phần còn lại của cuốn sách để sử dụng các phiên bản đã được lưu vào bộ nhớ cache này thay vì cố gắng sử dụng mạng.

[otherinstall]: https://forge.rust-lang.org/infra/other-installation-methods.html
[install]: https://www.rust-lang.org/tools/install
[msvc]: https://rust-lang.github.io/rustup/installation/windows-msvc.html
[community]: https://www.rust-lang.org/community
[tools]: https://www.rust-lang.org/tools
