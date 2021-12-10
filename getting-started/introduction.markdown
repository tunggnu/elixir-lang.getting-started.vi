---
section: getting-started
layout: getting-started
title: 1. Giới thiệu
---
{% assign stable = site.data.elixir-versions[site.data.elixir-versions.stable] %}

Xin chào!

Trong tài liệu hướng dẫn này, bạn sẽ được học các thành phần căn bản của Elixir - cú pháp ngôn ngữ, cách định nghĩa mô-đun, cách thao tác trên các cấu trúc dữ liệu phổ biến v.v. Chương này tập trung vào việc cài đặt Elixir và cách tương tác với Elixir bằng giao diện IEx (Elixir's Interactive Shell, một chương trình chạy ở chế độ dòng lệnh).

Yêu cầu của tài liệu là bạn phải cài thành công:

* Elixir phiên bản 1.5.0 trở lên
* Erlang/OTP phiên bản 19 trở lên

Hãy bắt đầu!

> If you find any errors in the tutorial or on the website, [please report a bug or send a pull request to our issue tracker](https://github.com/elixir-lang/elixir-lang.github.com).

> The Elixir guides are also available in EPUB format:
>
>   * [Getting started guide](https://elixir-lang.org/downloads/books/elixir-getting-started-guide.epub)
>   * [Mix and OTP guide](https://elixir-lang.org/downloads/books/mix-and-otp.epub)
>   * [Meta-programming guide](https://elixir-lang.org/downloads/books/meta-programming-in-elixir.epub)

## Cài đặt

Nếu bạn chưa cài Elixir, hãy xem [trang cài đặt](/install.html) của chúng tôi. Khi cài xong, bạn có thể chạy lệnh `elixir --version` để xác nhận phiên bản của Elixir và Erlang có thỏa mãn yêu cầu hay không.

## Chế độ tương tác

Sau khi cài Elixir bạn sẽ có ba chương trình sau: `iex`, `elixir` và `elixirc`. Nếu bạn biên dịch Elixir từ mã nguồn chứ không dùng bộ cài, các chương trình đó sẽ nằm trong thư mục `bin`.

Bây giờ hãy bắt đầu bằng cách gõ lệnh `iex` (hoặc `iex.bat` nếu bạn dùng Windows PowerShell) để mở chế độ tương tác của Elixir. Trong chế độ này chúng ta có thể gõ bất kỳ biểu thức nào và nhận về kết quả của nó. Hãy khởi động với một số biểu thức cơ bản sau:

```elixir
Erlang/OTP {{ stable.minimum_otp }} [64-bit] [smp:2:2] [...]

Interactive Elixir ({{ stable.version }}) - press Ctrl+C to exit
iex(1)> 40 + 2
42
iex(2)> "hello" <> " world"
"hello world"
```

Lưu ý rằng một số chi tiết như số hiệu phiên bản có thể khác một chút trên máy tính của bạn, cái đó không quan trọng. Từ giờ, các phiên làm việc với `iex` sẽ được lược bớt các thông tin phụ (như số hiệu phiên bản trong ví dụ trên) để chỉ tập trung vào phần mã lệnh. Nếu muốn thoát `iex` hãy bấm tổ hợp phím `Ctrl+C` hai lần.

Có vẻ như chúng ta đã sẵn sàng để khởi hành! Trong các chương sau chúng ta sẽ dùng chế độ tương tác rất nhiều để làm quen thêm một chút các cấu trúc ngôn ngữ và kiểu dữ liệu cơ bản.

> Lưu ý: nếu bạn dùng Windows, bạn cũng có thể gõ `iex --werl` (hoặc `iex.bat --werl` trong PowerShell) để có được trải nghiệm tốt hơn tùy vào giao diện dòng lệnh bạn đang dùng.

## Chạy các tập lệnh

Khi đã quen với các thành phần căn bản của ngôn ngữ, có thể bạn sẽ muốn thử viết các chương trình đơn giản. Nếu vậy bạn chỉ cần đặt các mã Elixir vào trong một tệp, ví dụ như mã sau:

```elixir
IO.puts("Hello world from Elixir")
```

Hãy lưu nó vào tệp `simple.exs` và thực thi nó bằng `elixir` như sau:

```console
$ elixir simple.exs
Hello world from Elixir
```

Sau này chúng ta sẽ học cách biên dịch mã Elixir (trong [Chương 8](/getting-started/modules-and-functions.html)) và cách dùng công cụ hỗ trợ biên dịch Mix (trong mục [hướng dẫn Mix và OTP](/getting-started/mix-otp/introduction-to-mix.html)). Còn bây giờ hãy chuyển sang [Chương 2](/getting-started/basic-types.html).

## Cách đặt câu hỏi

Trong khi đọc tài liệu hướng dẫn này, thường bạn sẽ có các thắc mắc; suy cho cùng đó là một phần của quá trình học! Có nhiều nơi cho bạn đưa ra câu hỏi, sau đây là một trong số đó:

* [Official #elixir on irc.libera.chat](irc://irc.libera.chat/elixir)
* [Elixir Forum](http://elixirforum.com)
* [Elixir on Slack](https://elixir-slackin.herokuapp.com/)
* [Elixir on Discord](https://discord.gg/elixir)
* [elixir tag on StackOverflow](https://stackoverflow.com/questions/tagged/elixir)

Khi đặt câu hỏi hãy nhớ hai mẹo sau:

* Thay vì hỏi "thực hiện việc X như thế nào trong Elixir", hãy hỏi "giải quyết bài toán Y thế nào trong Elixir". Nói cách khác, đừng hỏi cách thực hiện một giải pháp cụ thể thế nào, mà hãy môt tả vấn đề đang gặp phải. Phát biểu vấn đề mang đến nhiều ngữ cảnh hơn và giúp tìm ra câu trả lời hợp lý hơn.
* Trong tình huống có gì đó hoạt động không như mong muốn, hãy kèm theo báo cáo của bạn nhiều thông tin nhất có thể, ví dụ: số hiệu phiên bản Elixir, đoạn mã, thông báo lỗi cùng với dấu vết lỗi (stacktrace). Hãy dùng các trang web như [Gist](https://gist.github.com/) để đăng các thông tin đó.
