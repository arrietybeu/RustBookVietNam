## Hello, World!

Bây giờ bạn đã cài đặt Rust, đã đến lúc viết chương trình Rust đầu tiên của bạn.
Là truyền thống khi học một ngôn ngữ mới là viết một chương trình nhỏ
in văn bản `Hello, world!` lên màn hình, vì vậy chúng tôi sẽ làm điều tương tự ở đây!

> Lưu ý: Cuốn sách này giả định bạn có sự quen thuộc cơ bản với dòng lệnh.
> Rust không đặt ra bất kỳ yêu cầu cụ thể nào về trình soạn thảo hoặc công cụ của bạn
> hoặc nơi mã của bạn sống, vì vậy nếu bạn thích sử dụng IDE thay vì dòng lệnh,
> hãy thoải mái sử dụng IDE yêu thích của bạn. Nhiều IDE bây giờ có một mức độ hỗ trợ Rust;
> kiểm tra tài liệu IDE để biết chi tiết. Đội Rust đã tập trung vào việc cho phép hỗ trợ IDE tuyệt vời
> thông qua `rust-analyzer`. Xem [Phụ lục D][devtools] để biết thêm chi tiết.

<!-- Các tiêu đề cũ. Đừng xóa hoặc các liên kết có thể bị hỏng. -->
<a id="creating-a-project-directory"></a>

### Thiết Lập Thư Mục Dự Án

Bạn sẽ bắt đầu bằng cách tạo một thư mục để lưu trữ mã Rust của bạn.
Không quan trọng với Rust nơi mã của bạn sống, nhưng đối với các bài tập
và dự án trong cuốn sách này, chúng tôi đề nghị tạo một thư mục _projects_ trong thư mục home của bạn
và giữ tất cả các dự án của bạn ở đó.

Mở terminal và nhập các lệnh sau để tạo thư mục _projects_
và thư mục cho dự án "Hello, world!" trong thư mục _projects_.

Đối với Linux, macOS và PowerShell trên Windows, nhập:

```console
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

Đối với Windows CMD, nhập:

```cmd
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

<!-- Các tiêu đề cũ. Đừng xóa hoặc các liên kết có thể bị hỏng. -->
<a id="writing-and-running-a-rust-program"></a>

### Cơ Bản Về Chương Trình Rust

Tiếp theo, hãy tạo một tệp nguồn mới và gọi nó là _main.rs_. Các tệp Rust luôn kết thúc bằng
phần mở rộng _.rs_. Nếu bạn đang sử dụng nhiều hơn một từ trong tên tệp của mình, quy ước là sử dụng
một dấu gạch dưới để tách chúng. Ví dụ, sử dụng _hello_world.rs_ thay vì _helloworld.rs_.

Bây giờ mở tệp _main.rs_ mà bạn vừa tạo và nhập mã trong Danh sách 1-1.

<Danh sách số="1-1" tên-tệp="main.rs" chú thích="Một chương trình in `Hello, world!`">

```rust
fn main() {
    println!("Hello, world!");
}
```

</Danh sách>

Lưu tệp và quay lại cửa sổ terminal của bạn trong
thư mục _~/projects/hello_world_. Trên Linux hoặc macOS, nhập các lệnh sau để biên dịch và chạy tệp:

```console
$ rustc main.rs
$ ./main
Hello, world!
```

Trên Windows, nhập lệnh `.\main` thay vì `./main`:

```powershell
> rustc main.rs
> .\main
Hello, world!
```

Bất kể hệ điều hành của bạn là gì, chuỗi `Hello, world!` nên được in ra màn hình
terminal. Nếu bạn không thấy đầu ra này, hãy tham khảo lại phần
["Khắc phục sự cố"][troubleshooting] trong phần Cài đặt
để biết các cách nhận trợ giúp.

Nếu `Hello, world!` đã được in ra, chúc mừng! Bạn đã chính thức viết một chương trình Rust.
Điều đó khiến bạn trở thành một lập trình viên Rust—chào mừng!

<!-- Các tiêu đề cũ. Đừng xóa hoặc các liên kết có thể bị hỏng. -->

<a id="anatomy-of-a-rust-program"></a>

### Giải Thích Cấu Trúc Của Một Chương Trình Rust

Hãy cùng xem xét chương trình "Hello, world!" này một cách chi tiết. Đây là phần đầu tiên của
câu đố:

```rust
fn main() {

}
```

Các dòng này định nghĩa một hàm có tên là `main`. Hàm `main` là đặc biệt: Nó
luôn là mã đầu tiên được thực thi trong mọi chương trình Rust có thể thực thi. Ở đây, dòng đầu tiên khai báo một hàm có tên là `main` không có tham số và không trả về
gì cả. Nếu có tham số, chúng sẽ được đặt bên trong dấu ngoặc đơn (`()`)

Thân hàm được bao quanh bởi `{}`. Rust yêu cầu dấu ngoặc nhọn quanh tất cả
các thân hàm. Thật tốt khi đặt dấu ngoặc nhọn mở trên cùng một dòng với khai báo hàm,
thêm một khoảng trắng ở giữa.

> Lưu ý: Nếu bạn muốn tuân thủ một kiểu chuẩn trong tất cả các dự án Rust,
> bạn có thể sử dụng một công cụ định dạng tự động có tên là `rustfmt` để định dạng mã của bạn theo
> một kiểu nhất định (thêm về `rustfmt` trong
> [Phụ lục D][devtools]). Nhóm Rust đã bao gồm công cụ này
> với bản phân phối Rust chuẩn, như `rustc` là, vì vậy nó nên đã được cài đặt trên máy tính của bạn!

Thân hàm `main` chứa mã sau:

```rust
println!("Hello, world!");
```

Dòng này thực hiện tất cả công việc trong chương trình nhỏ này: Nó in văn bản ra màn hình.
Có ba chi tiết quan trọng cần lưu ý ở đây.

Đầu tiên, `println!` gọi một macro Rust. Nếu nó gọi một hàm thay vào đó, nó
sẽ được nhập là `println` (không có `!`). Các macro Rust là một cách để viết
mã tạo mã để mở rộng cú pháp Rust, và chúng tôi sẽ thảo luận về chúng chi tiết hơn trong
[Chương 20][ch20-macros]. Hiện tại, bạn chỉ cần biết rằng việc sử dụng `!` có nghĩa là bạn đang gọi một macro thay vì một hàm bình thường và rằng các macro không phải lúc nào cũng tuân theo cùng một quy tắc như các hàm.

Thứ hai, bạn thấy chuỗi `"Hello, world!"`. Chúng tôi truyền chuỗi này làm đối số
cho `println!`, và chuỗi này được in ra màn hình.

Thứ ba, chúng tôi kết thúc dòng bằng một dấu chấm phẩy (`;`), điều này cho thấy biểu thức này đã kết thúc và biểu thức tiếp theo đã sẵn sàng bắt đầu. Hầu hết các dòng mã Rust đều kết thúc bằng một dấu chấm phẩy.

<!-- Các tiêu đề cũ. Đừng xóa hoặc các liên kết có thể bị hỏng. -->
<a id="compiling-and-running-are-separate-steps"></a>

### Biên Dịch Và Thực Thi Là Hai Bước Riêng Biệt

Bạn vừa mới chạy một chương trình mới được tạo, vì vậy hãy xem xét từng bước trong
quá trình này.

Trước khi chạy một chương trình Rust, bạn phải biên dịch nó bằng cách sử dụng trình biên dịch Rust bằng cách
nhập lệnh `rustc` và truyền cho nó tên tệp nguồn của bạn, như thế này:

```console
$ rustc main.rs
```

Nếu bạn có nền tảng C hoặc C++, bạn sẽ nhận thấy rằng điều này tương tự như `gcc`
hay `clang`. Sau khi biên dịch thành công, Rust xuất ra một tệp thực thi nhị phân.

Trên Linux, macOS và PowerShell trên Windows, bạn có thể thấy tệp thực thi bằng cách
nhập lệnh `ls` trong shell của bạn:

```console
$ ls
main  main.rs
```

Trên Linux và macOS, bạn sẽ thấy hai tệp. Với PowerShell trên Windows, bạn sẽ
thấy cùng ba tệp mà bạn sẽ thấy khi sử dụng CMD. Với CMD trên Windows, bạn sẽ nhập lệnh sau:

```cmd
> dir /B %= tùy chọn /B nói chỉ hiển thị tên tệp =%
main.exe
main.pdb
main.rs
```

Điều này hiển thị tệp mã nguồn với phần mở rộng _.rs_, tệp thực thi
(_main.exe_ trên Windows, nhưng _main_ trên tất cả các nền tảng khác), và, khi sử dụng
Windows, một tệp chứa thông tin gỡ lỗi với phần mở rộng _.pdb_. Từ đây, bạn chạy tệp _main_ hoặc _main.exe_, như thế này:

```console
$ ./main # hoặc .\main trên Windows
```

Nếu _main.rs_ của bạn là chương trình "Hello, world!" của bạn, dòng lệnh này sẽ in `Hello,
world!` ra terminal của bạn.

Nếu bạn quen thuộc hơn với một ngôn ngữ động, chẳng hạn như Ruby, Python, hoặc
JavaScript, bạn có thể không quen với việc biên dịch và chạy một chương trình như
các bước riêng biệt. Rust là một ngôn ngữ _biên dịch trước_, có nghĩa là bạn có thể
biên dịch một chương trình và đưa tệp thực thi cho người khác, và họ có thể chạy nó
ngay cả khi không có Rust được cài đặt. Nếu bạn đưa cho ai đó một tệp _.rb_, _.py_, hoặc
_.js_ , họ cần phải có một cài đặt Ruby, Python, hoặc JavaScript được cài đặt (tương ứng). Nhưng trong những ngôn ngữ đó, bạn chỉ cần một lệnh để
biên dịch và chạy chương trình của bạn. Mọi thứ đều có sự đánh đổi trong thiết kế ngôn ngữ.

Chỉ biên dịch với `rustc` là đủ cho các chương trình đơn giản, nhưng khi dự án của bạn
phát triển, bạn sẽ muốn quản lý tất cả các tùy chọn và dễ dàng chia sẻ mã của mình.
Tiếp theo, chúng tôi sẽ giới thiệu cho bạn công cụ Cargo, sẽ giúp bạn viết
các chương trình Rust thực tế.

[troubleshooting]: ch01-01-installation.html#troubleshooting
[devtools]: appendix-04-useful-development-tools.html
[ch20-macros]: ch20-05-macros.html
