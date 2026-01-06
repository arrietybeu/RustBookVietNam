## Xin chào, Cargo!

Cargo là hệ thống build và trình quản lý package của Rust. Hầu hết các Rustacean sử dụng công cụ này để quản lý các dự án Rust của họ bởi vì Cargo xử lý rất nhiều tác vụ cho bạn, chẳng hạn như build code, tải xuống các thư viện mà code của bạn phụ thuộc vào, và build các thư viện đó. (Chúng ta gọi các thư viện mà code của bạn cần là _dependencies_.)

Các chương trình Rust đơn giản nhất, như chương trình chúng ta vừa viết, không có bất kỳ dependency nào. Nếu chúng ta đã build dự án "Hello, world!" với Cargo, nó sẽ chỉ sử dụng phần của Cargo xử lý việc build code của bạn. Khi bạn viết các chương trình Rust phức tạp hơn, bạn sẽ thêm các dependency, và nếu bạn bắt đầu một dự án bằng Cargo, việc thêm dependency sẽ dễ dàng hơn nhiều.

Bởi vì phần lớn các dự án Rust sử dụng Cargo, phần còn lại của cuốn sách này giả định rằng bạn cũng đang sử dụng Cargo. Cargo được cài đặt cùng với Rust nếu bạn sử dụng các trình cài đặt chính thức được thảo luận trong phần ["Cài đặt"][installation]<!-- ignore -->. Nếu bạn cài đặt Rust thông qua cách khác, hãy kiểm tra xem Cargo đã được cài đặt chưa bằng cách nhập lệnh sau vào terminal của bạn:

```console
$ cargo --version
```

Nếu bạn thấy số phiên bản, bạn đã có nó! Nếu bạn thấy lỗi, chẳng hạn như `command not found`, hãy xem tài liệu cho phương pháp cài đặt của bạn để xác định cách cài đặt Cargo riêng biệt.

### Tạo một Dự án với Cargo

Hãy tạo một dự án mới bằng Cargo và xem nó khác với dự án "Hello, world!" ban đầu của chúng ta như thế nào. Quay trở lại thư mục _projects_ của bạn (hoặc bất cứ nơi nào bạn quyết định lưu trữ code của mình). Sau đó, trên bất kỳ hệ điều hành nào, chạy lệnh sau:

```console
$ cargo new hello_cargo
$ cd hello_cargo
```

Lệnh đầu tiên tạo một thư mục và dự án mới có tên _hello_cargo_. Chúng ta đã đặt tên dự án của mình là _hello_cargo_, và Cargo tạo các file của nó trong một thư mục cùng tên.

Vào thư mục _hello_cargo_ và liệt kê các file. Bạn sẽ thấy rằng Cargo đã tạo hai file và một thư mục cho chúng ta: một file _Cargo.toml_ và một thư mục _src_ với file _main.rs_ bên trong.

Nó cũng đã khởi tạo một Git repository mới cùng với file _.gitignore_. Các file Git sẽ không được tạo nếu bạn chạy `cargo new` trong một Git repository đã tồn tại; bạn có thể ghi đè hành vi này bằng cách sử dụng `cargo new --vcs=git`.

> Lưu ý: Git là một hệ thống quản lý phiên bản phổ biến. Bạn có thể thay đổi `cargo new` để sử dụng một hệ thống quản lý phiên bản khác hoặc không có hệ thống quản lý phiên bản bằng cách sử dụng cờ `--vcs`. Chạy `cargo new --help` để xem các tùy chọn có sẵn.

Mở _Cargo.toml_ trong trình soạn thảo văn bản mà bạn chọn. Nó sẽ trông tương tự như code trong Listing 1-2.

<Listing number="1-2" file-name="Cargo.toml" caption="Nội dung của *Cargo.toml* được tạo bởi `cargo new`">

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2024"

[dependencies]
```

</Listing>

File này ở định dạng [_TOML_][toml]<!-- ignore --> (_Tom's Obvious, Minimal Language_), đây là định dạng cấu hình của Cargo.

Dòng đầu tiên, `[package]`, là một tiêu đề phần cho biết rằng các câu lệnh sau đang cấu hình một package. Khi chúng ta thêm nhiều thông tin hơn vào file này, chúng ta sẽ thêm các phần khác.

Ba dòng tiếp theo thiết lập thông tin cấu hình mà Cargo cần để biên dịch chương trình của bạn: tên, phiên bản, và edition của Rust để sử dụng. Chúng ta sẽ nói về khóa `edition` trong [Phụ lục E][appendix-e]<!-- ignore -->.

Dòng cuối cùng, `[dependencies]`, là phần bắt đầu của một phần để bạn liệt kê bất kỳ dependency nào của dự án. Trong Rust, các package code được gọi là _crate_. Chúng ta sẽ không cần bất kỳ crate nào khác cho dự án này, nhưng chúng ta sẽ cần trong dự án đầu tiên ở Chương 2, vì vậy chúng ta sẽ sử dụng phần dependencies này sau.

Bây giờ hãy mở _src/main.rs_ và xem:

<span class="filename">Tên file: src/main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

Cargo đã tạo một chương trình "Hello, world!" cho bạn, giống như chương trình chúng ta đã viết trong Listing 1-1! Cho đến nay, sự khác biệt giữa dự án của chúng ta và dự án mà Cargo tạo ra là Cargo đặt code trong thư mục _src_, và chúng ta có một file cấu hình _Cargo.toml_ trong thư mục cấp cao nhất.

Cargo mong đợi các file nguồn của bạn nằm trong thư mục _src_. Thư mục dự án cấp cao nhất chỉ dành cho các file README, thông tin giấy phép, file cấu hình, và bất cứ thứ gì khác không liên quan đến code của bạn. Sử dụng Cargo giúp bạn tổ chức các dự án của mình. Có một nơi cho mọi thứ, và mọi thứ đều ở đúng chỗ của nó.

Nếu bạn bắt đầu một dự án không sử dụng Cargo, như chúng ta đã làm với dự án "Hello, world!", bạn có thể chuyển đổi nó thành một dự án sử dụng Cargo. Di chuyển code dự án vào thư mục _src_ và tạo một file _Cargo.toml_ phù hợp. Một cách dễ dàng để có được file _Cargo.toml_ đó là chạy `cargo init`, lệnh này sẽ tạo nó cho bạn tự động.

### Build và Chạy một Dự án Cargo

Bây giờ hãy xem điều gì khác biệt khi chúng ta build và chạy chương trình "Hello, world!" với Cargo! Từ thư mục _hello_cargo_ của bạn, build dự án của bạn bằng cách nhập lệnh sau:

```console
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

Lệnh này tạo một file thực thi trong _target/debug/hello_cargo_ (hoặc _target\debug\hello_cargo.exe_ trên Windows) thay vì trong thư mục hiện tại của bạn. Bởi vì bản build mặc định là bản build debug, Cargo đặt file nhị phân trong một thư mục có tên _debug_. Bạn có thể chạy file thực thi bằng lệnh này:

```console
$ ./target/debug/hello_cargo # hoặc .\target\debug\hello_cargo.exe trên Windows
Hello, world!
```

Nếu mọi thứ suôn sẻ, `Hello, world!` sẽ được in ra terminal. Chạy `cargo build` lần đầu tiên cũng khiến Cargo tạo một file mới ở cấp cao nhất: _Cargo.lock_. File này theo dõi các phiên bản chính xác của các dependency trong dự án của bạn. Dự án này không có dependency, vì vậy file này hơi thưa thớt. Bạn sẽ không bao giờ cần thay đổi file này thủ công; Cargo quản lý nội dung của nó cho bạn.

Chúng ta vừa build một dự án với `cargo build` và chạy nó với `./target/debug/hello_cargo`, nhưng chúng ta cũng có thể sử dụng `cargo run` để biên dịch code và sau đó chạy file thực thi kết quả tất cả trong một lệnh:

```console
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

Sử dụng `cargo run` thuận tiện hơn việc phải nhớ chạy `cargo build` và sau đó sử dụng toàn bộ đường dẫn đến file nhị phân, vì vậy hầu hết các developer sử dụng `cargo run`.

Lưu ý rằng lần này chúng ta không thấy đầu ra cho biết Cargo đang biên dịch `hello_cargo`. Cargo đã nhận ra rằng các file không thay đổi, vì vậy nó không rebuild mà chỉ chạy file nhị phân. Nếu bạn đã sửa đổi code nguồn của mình, Cargo sẽ rebuild dự án trước khi chạy nó, và bạn sẽ thấy đầu ra này:

```console
$ cargo run
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

Cargo cũng cung cấp một lệnh gọi là `cargo check`. Lệnh này nhanh chóng kiểm tra code của bạn để đảm bảo nó biên dịch được nhưng không tạo ra file thực thi:

```console
$ cargo check
   Checking hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

Tại sao bạn lại không muốn một file thực thi? Thông thường, `cargo check` nhanh hơn nhiều so với `cargo build` bởi vì nó bỏ qua bước tạo file thực thi. Nếu bạn liên tục kiểm tra công việc của mình trong khi viết code, sử dụng `cargo check` sẽ tăng tốc quá trình cho bạn biết liệu dự án của bạn vẫn biên dịch được hay không! Do đó, nhiều Rustacean chạy `cargo check` định kỳ khi họ viết chương trình của mình để đảm bảo nó biên dịch được. Sau đó, họ chạy `cargo build` khi họ sẵn sàng sử dụng file thực thi.

Hãy tóm tắt lại những gì chúng ta đã học cho đến nay về Cargo:

- Chúng ta có thể tạo một dự án bằng `cargo new`.
- Chúng ta có thể build một dự án bằng `cargo build`.
- Chúng ta có thể build và chạy một dự án trong một bước bằng `cargo run`.
- Chúng ta có thể build một dự án mà không tạo ra file nhị phân để kiểm tra lỗi bằng `cargo check`.
- Thay vì lưu kết quả của bản build trong cùng thư mục với code của chúng ta, Cargo lưu trữ nó trong thư mục _target/debug_.

Một lợi thế bổ sung của việc sử dụng Cargo là các lệnh đều giống nhau bất kể bạn đang làm việc trên hệ điều hành nào. Vì vậy, tại thời điểm này, chúng ta sẽ không còn cung cấp hướng dẫn cụ thể cho Linux và macOS so với Windows nữa.

### Build cho Bản phát hành

Khi dự án của bạn cuối cùng đã sẵn sàng để phát hành, bạn có thể sử dụng `cargo build --release` để biên dịch nó với các tối ưu hóa. Lệnh này sẽ tạo một file thực thi trong _target/release_ thay vì _target/debug_. Các tối ưu hóa làm cho code Rust của bạn chạy nhanh hơn, nhưng bật chúng lên sẽ kéo dài thời gian cần thiết để chương trình của bạn biên dịch. Đây là lý do tại sao có hai profile khác nhau: một cho phát triển, khi bạn muốn rebuild nhanh chóng và thường xuyên, và một cái khác để build chương trình cuối cùng mà bạn sẽ đưa cho người dùng mà sẽ không được rebuild lặp đi lặp lại và sẽ chạy nhanh nhất có thể. Nếu bạn đang đo thời gian chạy của code, hãy chắc chắn chạy `cargo build --release` và đo với file thực thi trong _target/release_.

<!-- Old headings. Do not remove or links may break. -->
<a id="cargo-as-convention"></a>

### Tận dụng các Quy ước của Cargo

Với các dự án đơn giản, Cargo không cung cấp nhiều giá trị hơn việc chỉ sử dụng `rustc`, nhưng nó sẽ chứng tỏ giá trị của nó khi các chương trình của bạn trở nên phức tạp hơn. Khi các chương trình phát triển thành nhiều file hoặc cần một dependency, việc để Cargo điều phối bản build sẽ dễ dàng hơn nhiều.

Mặc dù dự án `hello_cargo` đơn giản, giờ đây nó sử dụng phần lớn các công cụ thực sự mà bạn sẽ sử dụng trong phần còn lại của sự nghiệp Rust của bạn. Trên thực tế, để làm việc trên bất kỳ dự án hiện có nào, bạn có thể sử dụng các lệnh sau để checkout code bằng Git, chuyển đến thư mục của dự án đó, và build:

```console
$ git clone example.org/someproject
$ cd someproject
$ cargo build
```

Để biết thêm thông tin về Cargo, hãy xem [tài liệu của nó][cargo].

## Tóm tắt

Bạn đã có một khởi đầu tuyệt vời trong hành trình Rust của mình! Trong chương này, bạn đã học cách:

- Cài đặt phiên bản ổn định mới nhất của Rust bằng `rustup`.
- Cập nhật lên phiên bản Rust mới hơn.
- Mở tài liệu được cài đặt cục bộ.
- Viết và chạy chương trình "Hello, world!" bằng `rustc` trực tiếp.
- Tạo và chạy một dự án mới bằng các quy ước của Cargo.

Đây là thời điểm tuyệt vời để build một chương trình đáng kể hơn để làm quen với việc đọc và viết code Rust. Vì vậy, trong Chương 2, chúng ta sẽ build một chương trình trò chơi đoán số. Nếu bạn muốn bắt đầu bằng cách học cách các khái niệm lập trình phổ biến hoạt động trong Rust, hãy xem Chương 3 và sau đó quay lại Chương 2.

[installation]: ch01-01-installation.html#installation
[toml]: https://toml.io
[appendix-e]: appendix-05-editions.html
[cargo]: https://doc.rust-lang.org/cargo/


<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>