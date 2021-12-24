---
section: getting-started
layout: getting-started
title: 2. Các kiểu cơ bản
---

Trong chương này chúng ta sẽ học thêm về các kiểu dữ liệu cơ bản của Elixir: integer (số nguyên), float (số thực), boolean (luận lí), atom (nguyên tử), string (chuỗi kí tự), list (danh sách), và tuple (bộ). Sau đây là ví dụ một số giá trị của các kiểu cơ bản:

```elixir
iex> 1          # integer
iex> 0x1F       # integer
iex> 1.0        # float
iex> true       # boolean
iex> :atom      # atom / symbol
iex> "elixir"   # string
iex> [1, 2, 3]  # list
iex> {1, 2, 3}  # tuple
```

## Số học cơ bản

Hãy mở IEx trong giao diện dòng lệnh (gõ `iex`) rồi nhập vào các biểu thức sau:

```elixir
iex> 1 + 2
3
iex> 5 * 5
25
iex> 10 / 2
5.0
```

Lưu ý rằng `10 / 2` trả về số thực `5.0` chứ không phải số nguyên `5`. Điều này đúng như mong đợi. Trong Elixir, toán tử (phép toán) chia `/` luôn trả về một số thực. Nếu bạn muốn thực hiện phép chia số nguyên hoặc lấy phần dư bạn có thể dùng hàm `div` hoặc `rem`:

```elixir
iex> div(10, 2)
5
iex> div 10, 2
5
iex> rem 10, 3
1
```

Lưu ý rằng Elixir cho phép bạn lược bỏ cặp dấu ngoặc tròn khi gọi và truyền ít nhất một đối số cho một hàm *có tên*. Đặc điểm này đem đến một cú pháp gọn gàng hơn khi viết các khai báo hoặc các cấu trúc luồng điều khiển (control-flow construct). Tuy nhiên các lập trình viên nhìn chung thích viết kèm dấu ngoặc tròn hơn.

> Ghi chú của người dịch: khái niệm hàm *có tên* và hàm *khuyết danh* sẽ được trình bày cụ thể hơn ở phần sau. Trong ví dụ trên, `div` và `rem` chính là tên của các hàm tương ứng.

Elixir cũng hỗ trợ cách viết tắt các số ở hệ nhị phân, bát phân, và thập lục phân:

```elixir
iex> 0b1010 # số nhị phân
10
iex> 0o777  # số bát phân
511
iex> 0x1F   # số bát phân
31
iex> 0x1f === 0x1F
true
```

Cách viết số thực phải gồm một dấu chấm và theo sau là ít nhất một chữ số. Bạn cũng có thể dùng cách viết khoa học với kí hiệu `e` (lũy thừa cơ số 10):

```elixir
iex> 1.0
1.0
iex> 1.0e2
100.0
iex> 1.0e-2
0.01
iex> 1.0e-10
1.0e-10
```

Trong Elixir, các số thực có độ chính xác kép (64-bit double precision).

Bạn có thể gọi hàm `round` để tìm số nguyên gần nhất của một số thực cho trước, hoặc hàm `trunc` để lấy phần nguyên của một số thực.

```elixir
iex> round(3.58)
4
iex> trunc(3.58)
3
```

## Nhận dạng các hàm và tra cứu tài liệu

Các hàm trong Elixir được nhận dạng dựa trên đồng thời hai yếu tố: tên gọi và số lượng đối số (arity). Kể từ giờ, xuyên suốt tài liệu hướng dẫn này, chúng ta sẽ dùng cả hai yếu tố trên khi đề cập đến các hàm. `trunc/1` ám chỉ hàm có tên là `trunc` và nhận `1` đối số, trong khi `trunc/2` ám chỉ một hàm khác (là ví dụ, chứ không có thật) có cùng tên nhưng nhận `2` đối số.

Chúng ta dùng cú pháp trên khi xem tài liệu mô tả các hàm. Elixir shell định nghĩa sẵn hàm `h` dùng để truy cập tài liệu của bất kỳ hàm nào. Ví dụ, gõ `h trunc/1` sẽ in ra tài liệu mô tả hàm `trunc/1`:

```elixir
iex> h trunc/1
                             def trunc()

Returns the integer part of number.
```

Gõ `h trunc/1` có kết quả như trên vì hàm `trunc/1` được định nghĩa sẵn trong mô đun `Kernel`. Tất cả các hàm của `Kernel` được tự động nạp vào danh sách tên gọi hiện có (namespace) của chúng ta. Thông thường khi tìm tài liệu của một hàm cho trước bạn cũng ghi cả tên mô đun của nó:

```elixir
iex> h Kernel.trunc/1
                             def trunc()

Returns the integer part of number.
```

Bạn có thể kết hợp tên mô-đun và hàm để tìm kiếm bất kỳ hàm nào, bao gồm cả toán tử (hãy thử gõ `h Kernel.+/2` xem sao). Gọi `h` mà không kèm đối số nào sẽ hiển thị tài liệu của mô-đun `IEx.Helpers`, là nơi chứa định nghĩa của hàm `h` và các hàm chức năng khác.

## Kiểu boolean

Elixir hỗ trợ các giá trị boolean là `true` và `false` là, lần lượt có nghĩa là *đúng* và *sai*:

```elixir
iex> true
true
iex> true == false
false
```

Elixir còn cung cấp một số hàm bổ nghĩa (predicate function) để kiểm tra kiểu của một giá trị cho trước. Ví dụ, bạn có thể dùng hàm `is_boolean/1` để kiểm tra một giá trị có phải thuộc kiểu boolean hay không:

```elixir
iex> is_boolean(true)
true
iex> is_boolean(1)
false
```

Bạn cũng có thể dùng `is_integer/1`, `is_float/1`, hoặc `is_number/1` để lần lượt kiểm tra một giá trị có phải là số nguyên, số thực, hay là số nói chung.

## Kiểu atom

Một atom (nguyên tử) là một hằng số mà giá trị của nó chính là tên gọi của nó. Trong một số ngôn ngữ lập trình, nó còn được gọi là symbol (kí hiệu). Các atom thường có ích khi dùng để liệt kê các giá trị riêng biệt, ví dụ như:

```elixir
iex> :apple
:apple
iex> :orange
:orange
iex> :watermelon
:watermelon
```

> Ghi chú của người dịch:
>
> * Cách định nghĩa atom ở trên có vẻ khó hiểu. Theo người dịch, một atom là một giá trị cụ thể (hằng số), biểu diễn cho một ý nghĩa nào đó mà lập trình viên tự quy định. Ví dụ để biểu diễn một quả táo, một lập trình viên có thể dùng atom với kí hiệu là `:apple`, nhưng một lập trình viên khác lại có thể dùng atom với kí hiệu khác, như là `:an_apple`, hoặc thậm chí là `:qua_tao`. Điều thú vị là, cách định nghĩa atom của người dịch có vẻ cũng... khó hiểu 😅
> * Kí hiệu của atom luôn bắt đầu bằng dấu hai chấm `:`, sau đó là một chữ cái a-z/A-Z, và sau đó có thể có thêm các chữ số hoặc chữ cái khác nữa.

Hai atom được coi như tương đương nhau nếu tên gọi (kí hiệu) của chúng giống nhau.

```elixir
iex> :apple == :apple
true
iex> :apple == :orange
false
```

Thông thường chúng được dùng để biểu diễn kết quả của một phép toán, ví dụ như `:ok` và `:error`.

Các giá trị `true` and `false` thực ra cũng là các atom:

```elixir
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```

Elixir cho phép bạn lược bỏ dấu `:` khi viết các atom `false`, `true` và `nil` (ý nghĩa của `nil` cũng giống như `null` trong các ngôn ngữ lập trình khác). Nhưng tất cả các atom khác phải bắt đầu bằng `:`.

Cuối cùng Elixir có một cấu trúc gọi là alias (bí danh) mà chúng ta sẽ khám phá sau. Alias thực ra là atom nhưng được kí hiệu bắt đầu bằng một chữ cái in hoa chứ không phải dấu `:`.

```elixir
iex> is_atom(Hello)
true
```

## Kiểu string

Trong Elixir, kí hiệu của string (chuỗi kí tự) được bao bởi cặp kí tự nháy kép `"`, và nó được mã hóa theo cơ chế mã hóa UTF-8. Do đó string có thể biểu diễn cho chuỗi kí tự Unicode bất kì:

```elixir
iex> "hellö"
"hellö"
```

> Ghi chú: nếu bạn đang dùng Windows, thì có khả năng terminal (giao diện dòng lệnh) của bạn mặc định không hỗ trợ UTF-8. Bạn có thể đổi sang chế độ mã hóa UTF-8 trước khi mở IEx bằng cách gõ `chcp 65001`.

Elixir còn hỗ trợ tính năng *string interpolation* (nội suy chuỗi), nghĩa là chèn giá trị dạng string của một biến đã cho vào trong phần kí hiệu mô tả một string khác. Ví dụ:

```elixir
iex> string = :world
iex> "hellö #{string}"
"hellö world"
```

> Ghi chú của người dịch: trong Elixir, giá trị dạng string của một atom là dãy kí tự phía sau dấu `:` trong kí hiệu của atom đó. Do vậy giá trị dạng string của atom `:world` là `world`, nên `"hellö #{string}"` tương đương với `"hellö world"`.

String có thể chứa các dấu ngắt dòng (line break). Khi viết một string, bạn có thể trực tiếp bấm phím ⏎ tại các vị trí muốn xuống dòng, hoặc dùng escape sequence (chuỗi thoát) `\n` thay cho bấm phím ⏎:

```elixir
iex> "hello
...> world" # bấm ⏎ ngay sau hello ở trên để xuống dòng, rồi gõ tiếp world
"hello\nworld"
iex> "hello\nworld" # không bấm ⏎ ngay sau hello mà gõ \n
"hello\nworld"
```

Bạn có thể in ra một string bằng cách gọi hàm `IO.puts/1` của mô-đun`IO`:

```elixir
iex> IO.puts("hello\nworld")
hello
world
:ok
```

Lưu ý rằng hàm `IO.puts/1` trả lại atom `:ok` sau khi in.

Trong Elixir, string thực chất được biểu diễn bởi một dãy byte liên tục, còn gọi là binary:

```elixir
iex> is_binary("hellö")
true
```

Chúng ta cũng có thể tính số lượng byte biểu diễn một string:

```elixir
iex> byte_size("hellö")
6
```

Lưu ý rằng số byte để biểu diễn string trên là 6, mặc dù string chỉ có 5 grapheme (chữ cái). Đó là vì chữ cái "ö" tốn 2 byte để lưu trữ theo chuẩn UTF-8. Chúng ta có thể tính độ dài thực tế của string, là số lượng chữ cái của nó, bằng cách dùng hàm `String.length/1`:

```elixir
iex> String.length("hellö")
5
```

Mô-đun [String](https://hexdocs.pm/elixir/String.html) chứa một loạt các hàm dùng để thao tác trên các string theo chuẩn Unicode:

```elixir
iex> String.upcase("hellö")
"HELLÖ"
```

## Hàm khuyết danh (anonymous function)

Ngoài các hàm có tên như `String.length`, `String.upcase`, `byte_size` được đề cập bên trên, Elixir còn cung cấp các hàm khuyết danh (không có tên gọi). Nhờ hàm khuyết danh chúng ta có thể lưu trữ và truyền các mã thực thi cứ như thể chúng là các giá trị số hoặc string thông thường. Hàm khuyết danh được bao bởi cặp từ khóa `fn` và `end`:

```elixir
iex> add = fn a, b -> a + b end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> add.(1, 2)
3
iex> is_function(add)
true
```

Trong ví dụ trên chúng ta định nghĩa một hàm khuyết danh nhận hai đối số, `a` và `b`, và trả về kết quả của biểu thức `a + b`. Các đối số luôn nằm bên trái cặp kí tự `->` và mã thực thi thì nằm bên phải. Hàm này được lưu vào biến `add`.

Chúng ta có thể gọi hàm khuyết danh bằng cách truyền các đối số cho nó. Lưu ý rằng bắt buộc phải có một dấu chấm (`.`) giữa tên biến và cặp ngoặc tròn bao quanh các đối số. Dấu chấm giúp đảm bảo không có sự nhập nhằng giữa việc gọi một hàm khuyết danh đã gán cho biến `add` trước đó và một hàm có tên là `add/2`. Chúng ta sẽ làm việc với các hàm có tên nhiều hơn khi học đến mục [Mô-đun và Hàm](/getting-started/modules-and-functions.html). Hiện giờ chỉ cần nhớ rằng Elixir có sự phân biệt rõ ràng giữa hàm khuyết danh và hàm có tên.

Hàm khuyết danh trong Elixir cũng được nhận dạng bởi số lượng đối số của nó. Chúng ta có thể kiểm tra xem một hàm khuyết danh có nhận một lượng đối số nào đó hay không bằng cách dùng hàm `is_function/2`:

```elixir
# check if add is a function that expects exactly 2 arguments
iex> is_function(add, 2)
true
# check if add is a function that expects exactly 1 argument
iex> is_function(add, 1)
false
```

Cuối cùng, hàm khuyết danh cũng có thể truy cập các biến ở trong cùng phạm vi với nó tại thời điểm nó được định nghĩa. Điều này thường được gọi là closure. Hãy định nghĩa một hàm khuyết danh mới dùng hàm khuyết danh `add` mà chúng ta đã định nghĩa ở trên:

```elixir
iex> double = fn a -> add.(a, a) end
#Function<6.71889879/1 in :erl_eval.expr/5>
iex> double.(2)
4
```

> Ghi chú của người dịch: khái niệm closure không được trình bày chi tiết ở đây nên nếu bạn không hiểu nó thì cũng là bình thường. Hãy chờ xem các phần sau của tài liệu hướng dẫn này có làm rõ được khái niệm closure không.

Gán giá trị mới cho một biến bên trong một hàm không làm ảnh hưởng đến biến cùng tên thuộc phạm vi xung quanh hàm:

```elixir
iex> x = 42
42
iex> (fn -> x = 0 end).()
0
iex> x
42
```

## Kiểu list

Elixir dùng cặp ngoặc vuông `[]` để biểu thị một danh sách (list) các giá trị. Các giá trị của danh sách có thể thuộc bất kì kiểu dữ liệu nào:

```elixir
iex> [1, 2, true, 3]
[1, 2, true, 3]
iex> length [1, 2, 3]
3
```

Hai danh sách có thể được ghép nối hoặc loại trừ nhau bằng cách dùng toán tử `++/2` hoặc `--/2`:

```elixir
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, true, 2, false, 3, true] -- [true, false]
[1, 2, 3, true]
```

Các toán tử xử lý danh sách (như `++/2` và `--/2`) không bao giờ làm biến đổi danh sách đã cho. Ghép nối hoặc loại trừ các phần tử khỏi một danh sách luôn sinh ra kết quả là một danh sách mới. Chúng ta nói rằng các cấu trúc dữ liệu trong Elixir là *immutable* (bất biến). Một ưu thế của tính bất biến là nó giúp mã trở nên rõ ràng hơn. Bạn có thể tự do truyền dữ liệu đi khắp nơi nhưng vẫn đảm bảo được không đoạn mã nào thay đổi được nó - chỉ có thể dùng nó để sinh dữ liệu mới.

Xuyên suốt tài liệu hướng dẫn này chúng ta sẽ nói nhiều đến đầu (head) và đuôi (tail) của danh sách. Phần tử đầu tiên của danh sách được gọi là đầu và danh sách các phần tử còn lại của danh sách được gọi là đuôi. Như vậy đuôi là danh sách con của danh sách đã cho. Bạn có thể tính ra chúng lần lượt bằng các hàm `hd/1` và `tl/1`. Bây giờ hãy gán một danh sách cho một biến và lấy ra đầu và đuôi của nó:

```elixir
iex> list = [1, 2, 3]
iex> hd(list)
1
iex> tl(list)
[2, 3]
```

Lấy đầu hoặc đuôi của một danh sách rỗng sẽ sinh ra một lỗi:

```elixir
iex> hd([])
** (ArgumentError) argument error
```

Đôi khi bạn muốn tạo một danh sách nhưng Elixir lại trả về cho bạn một chuỗi các kí tự bên trong cặp nháy kép `''`. Ví dụ:

```elixir
iex> [11, 12, 13]
'\v\f\r'
iex> [104, 101, 108, 108, 111]
'hello'
```

Đó là vì khi Elixir gặp một danh sách các con số tương ứng với mã ASCII của [các kí tự có thể nhìn thấy](https://en.wikipedia.org/wiki/ASCII#Printable_characters) được, thì Elixir sẽ in ra danh sách các kí tự đó (charlist) thay vì in ra danh sách các con số ban đầu. Danh sách kí tự thường hay gặp khi giao tiếp với các mã Erlang có sẵn. Bất cứ khi nào bạn nhìn thấy một giá trị được in ra trong IEx nhưng lại cảm thấy nghi ngờ nó, bạn có thể dùng hàm `i/1` để lấy thêm thông tin về nó:

```elixir
iex> i 'hello'
Term
  'hello'
Data type
  List
Description
  ...
Raw representation
  [104, 101, 108, 108, 111]
Reference modules
  List
Implemented protocols
  ...
```

Hãy nhớ rằng kí hiệu gồm các kí tự được bao quanh bởi cặp ngoặc đơn và kí hiệu gồm các kí tự được bao quanh bởi cặp ngoặc kép là không tương đương nhau, vì chúng đại diện cho các giá trị thuộc các kiểu dữ liệu khác nhau:

```elixir
iex> 'hello' == "hello"
false
```

Kí hiệu gồm cặp ngoặc đơn bao quanh các kí tự là đại diện cho một charlist, còn kí hiệu gồm cặp ngoặc kép bao quanh các kí tự là đại diện cho một string. Chúng ta sẽ thảo luận thêm về chúng trong chương ["Binary, string và charlist"](/getting-started/binaries-strings-and-char-lists.html).

## Kiểu tuple

Elixir sử dụng căp ngoặc nhọn `{}` để định nghĩa tuple (bộ). Giống như danh sách, bộ có thể chứa bất kỳ giá trị nào:

```elixir
iex> {:ok, "hello"}
{:ok, "hello"}
iex> tuple_size {:ok, "hello"}
2
```

Bộ lưu các phần tử của nó liên tục trong bộ nhớ. Điều này có nghĩa truy cập một phần tử của bộ thông qua chỉ số hoặc tính kích thước của bộ sẽ rất nhanh. Chỉ số của các phần tử bắt đầu từ `0`:

```elixir
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> elem(tuple, 1)
"hello"
iex> tuple_size(tuple)
2
```

Có thể dùng hàm `put_elem/3` để gán một giá trị mới cho một phần tử hiện có của bộ thông qua chỉ số của phần tử đó:

```elixir
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> put_elem(tuple, 1, "world")
{:ok, "world"}
iex> tuple
{:ok, "hello"}
```

Lưu ý rằng hàm `put_elem/3` trả về một bộ mới còn bộ ban đầu ứng với biến  `tuple` thì không hề bị biến đổi. Mọi thao tác trên một bộ luôn trả về một bộ mới, nó không bao giờ thay đổi bộ ban đầu.

> Ghi chú của người dịch: hàm `put_elem/3` chỉ thay đổi giá trị của một phần tử hiện có của bộ, chứ nó không thêm một phần tử mới vào trong bộ, như ở ví dụ trên nếu bạn muốn thêm `"world"` vào bộ bằng cách gọi `put_elem(tuple, 2, "world")` thì sẽ bị lỗi.

## Dùng list hay tuple?

Sự khác biệt giữa danh sách và bộ là gì?

Elixir sử dụng cấu trúc dữ liệu danh sách liên kết đơn (linked list) để lưu danh sách trong bộ nhớ, nghĩa là mỗi phần tử của danh sách liên kết với giá trị của nó đồng thời trỏ đến phần tử tiếp theo, cứ như thế cho đến cuối danh sách. Điều này dẫn đến việc tính độ dài của một danh sách là một thao tác tuyến tính (linear operation): chúng ta cần phải lần lượt di chuyển từ đầu đến cuối của danh sách mới có thể xác định được độ dài của nó.

Tương tự, hiệu suất của việc nối danh sách phụ thuộc vào độ dài của danh sách nằm bên trái toán tử nối `++`:

```elixir
iex> list = [1, 2, 3]
[1, 2, 3]

# Thao tác nối bên dưới sẽ nhanh vì ta chỉ cần truy cập phần tử đầu tiên
# của danh sách `[0]` là đã có thể nối nó với danh sách `list`
iex> [0] ++ list
[0, 1, 2, 3]

# Thao tác nối bên dưới sẽ chậm vì ta phải truy cập tuần tự từ phần tử
# đầu tiên của `list` đến phần tử cuối cùng mới có thể nối nó với `[4]`
iex> list ++ [4]
[1, 2, 3, 4]
```

Ngược lại các phần tử của bộ được lưu liên tục trong bộ nhớ, dẫn đến việc tính kích cỡ của bộ hoặc truy cập một phần tử thông qua chỉ số của nó sẽ nhanh. Tuy nhiên cập nhật hoặc bổ sung phần tử vào bộ sẽ tốn thời gian vì nó đòi hỏi phải tạo một bộ mới trong bộ nhớ:

```elixir
iex> tuple = {:a, :b, :c, :d}
{:a, :b, :c, :d}
iex> put_elem(tuple, 2, :e)
{:a, :b, :e, :d}
```

Lưu ý rằng đặc điểm này chỉ áp dụng với bản thân các phần tử của bộ, chứ không áp dụng cho các giá trị mà các phần tử đang liên kết tới. Ví dụ, khi bạn cập nhật một bộ, tất cả các giá trị trước đó, ngoại trừ giá trị bị cập nhật, sẽ được dùng chung bởi cả bộ mới và bộ cũ. Nói cách khác, bộ và danh sách trong Elixir có khả năng chia sẻ nội dung. Điều này giúp giảm bộ nhớ cần cấp phát cho các bộ và chuỗi mới, và đó là nhờ vào tính bất biến trong Elixir.

Các đặc điểm hiệu suất kể trên đã quyết định cách dùng các cấu trúc dữ liệu đó.Một cách dùng bộ rất phổ biến là kết hợp các thông tin phụ với thông tin chính làm kết quả trả trả về sau khi gọi một hàm . Ví dụ hàm `File.read/1` dùng để đọc nội dung của tệp. Nó trả về một bộ:

```elixir
iex> File.read("path/to/existing/file") # Đường dẫn đầy đủ đến tệp thông thường
{:ok, "... contents ..."}
iex> File.read("path/to/unknown/file") # Đường dẫn đến tệp không tồn tại
{:error, :enoent}
```

Nếu đường dẫn đưa cho `File.read/1` thực sự ứng với một tệp tồn tại và có thể đọc được, `File.read/1` sẽ trả về một bộ với `:ok` là phần tử đầu tiên và nội dung tệp (kiểu binary) là phần tử thứ hai. Ngược lại nó trả về một bộ với phần tử đầu tiên là `:error` và phần tử thứ hai là một atom mô tả lỗi.

Trong hầu hết các tình huống, Elixir sẽ hướng dẫn bạn làm điều đúng đắn. Ví dụ Elixir có hàm `elem/2` để truy cập đến một phần tử bất kỳ của bộ nhưng lại không có hàm tương tự dành cho danh sách {vì truy cập đến phần tử bất kỳ của danh sách là việc không nên làm}:

```elixir
iex> tuple = {:ok, "hello"}
{:ok, "hello"}
iex> elem(tuple, 1)
"hello"
```

Khi cần lấy ra số phần tử của một cấu trúc dữ liệu, Elixir tuân theo một quy tắc đơn giản: tên hàm có chứa từ `size` nếu việc đếm phần tử tốn khoảng thời gian không đổi (constant time) (ví như số phần tử đã được tính trước), còn nếu việc đếm cần thời gian tuyến tính (linear) (ví như thời gian đếm càng lâu khi cấu trúc dữ liệu càng lớn) thì tên hàm có chứa từ `length`. Một mẹo để nhớ điều này là cả "length" và "linear" đều bắt đầu bằng chữ cái "l".

Ví dụ cho đến giờ chúng ta đã dùng 4 hàm lấy số phần tử: `byte_size/1` (lấy số byte của một string), `tuple_size/1` (lấy số phần tử của bộ), `length/1` (lấy số phần tử của danh sách) và `String.length/1` (lấy số chữ cái của một string). Dùng `byte_size`  không tốn thời gian nên bạn có thể dùng thoải mái,nhưng dùng `String.length` lại tốn thời gian vì phải duyệt toàn bộ string mới có thể tính ra số chữ cái của nó, do đó nên hạn chế dùng.

Elixir cũng cung cấp các kiểu dữ liệu `Port`, `Reference`, và `PID` (thường dùng trong giao tiếp giữa các tiến trình / process communication), và chúng ta sẽ xem sơ qua chúng khi bàn về các tiến trình (process). Còn bây giờ chúng ta hãy xem xét một số toán tử cơ bản thường dùng với các dữ liệu cơ bản đã học trong chương này.
