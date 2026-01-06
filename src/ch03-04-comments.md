## Comments

Tất cả các lập trình viên đều cố gắng làm cho code của họ dễ hiểu, nhưng đôi khi cần giải thích thêm. Trong những trường hợp này, các lập trình viên để lại _comments_ trong code nguồn của họ mà compiler sẽ bỏ qua nhưng những người đọc code nguồn có thể thấy hữu ích.

Đây là một comment đơn giản:

```rust
// hello, world
```

Trong Rust, phong cách comment theo idiom bắt đầu một comment với hai dấu gạch chéo, và comment tiếp tục cho đến cuối dòng. Đối với các comment mở rộng vượt quá một dòng đơn, bạn sẽ cần bao gồm `//` trên mỗi dòng, như thế này:

```rust
// So we're doing something complicated here, long enough that we need
// multiple lines of comments to do it! Whew! Hopefully, this comment will
// explain what's going on.
```

Comments cũng có thể được đặt ở cuối dòng chứa code:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-24-comments-end-of-line/src/main.rs}}
```

Nhưng bạn sẽ thường thấy chúng được sử dụng ở định dạng này, với comment trên một dòng riêng biệt phía trên code mà nó đang chú thích:

<span class="filename">Tên file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-25-comments-above-line/src/main.rs}}
```

Rust cũng có một loại comment khác, documentation comments (comment tài liệu), mà chúng ta sẽ thảo luận trong phần ["Xuất bản một Crate lên Crates.io"][publishing]<!-- ignore --> của Chương 14.

[publishing]: ch14-02-publishing-to-crates-io.html

<div style="text-align: right">
  <em>Người dịch Arriety</em>
</div>