## Câu lệnh làm việc với tập tin, thư mục

Trong Linux, khi làm việc với các tập tin, thư mục trong môi trường Command Line, ta có các lệnh cơ bản sau:

- Lệnh `pwd` (path working directory)

In ra đường dẫn đến vị trí hiện tại bạn đang đứng.

- Lệnh `ls` (list) - xem danh sách tập tin thư mục

`ls -[tùy chọn] [đường dẫn thư mục muốn xem]`

Các tuỳ chọn phổ biến của lệnh `ls`:

| Các tùy chọn | Ý nghĩa |
| --- | --- |
| -L | Hiển thị danh sách tập tin, thư mục (chỉ hiện thị tên)
| -l | Hiển thị danh sách tập tin, thư mục (gồm nhiều cột: filename, size, date,… |
| -a | Liệt kê tất cả các tập tin, thư mục, bao gồm những tập tin ẩn |
| -R | Liệt kê tất cả các tập tin, thư mục kể cả các tập tin, thư mục bên trong thư mục cha |

Ngoài ra chúng ta có thể sử dụng `man` để xem các tuỳ chọn của lệnh `ls`

`man ls`

- Lệnh `grep` - lọc lại tên tập tin thư mục muốn xem

Lệnh `ls -l` của "/" cho kết quả nhiều thông tin, nếu muốn lọc lại tên tập tin thư mục muốn xem chỉ cần thêm `grep`.

Ví dụ: Muốn xem trong "/" có tập tin, thư mục nào có ký tự là "pro" thì thực hiện như sau:

`ls -l | grep pro`

Lệnh `grep` còn được dùng tìm kiếm chuỗi trong file:

`grep "chuỗi" [tên file]`

- Lệnh `cd` (change directory)

Thay đổi vị trí thư mục hiện tại – di chuyển đến vị trí thư mục khác. Một số cách khác nhau khi sử dụng lệnh cd là:

	- cd . : đứng nguyên ở thư mục hiện tại
    - cd .. : di chuyển đến thư mục cha của thư mục hiện tại
    - cd – : di chuyển đến thư mục trước khi di chuyển đến thư mục hiện tại
    - cd hoặc cd ~: di chuyển đến thư mục /home/username. Đây là vị trí thư mục mặc định mỗi khi bạn mở Terminal. Và bạn có toàn quyền đối với thư mục này.
    - cd / : di chuyển đến thư mục root – thư mục gốc chứa mọi thư mục, trong đó có /home/username
    - cd [tên thư mục con]: di chuyển đến thư mục con bên trong thư mục hiện tại
    - cd [đường dẫn đến thư mục] : di chuyển đến thư mục với đường dẫn là đường dẫn cứng. Đường dẫn cứng có thể ví dụ như: /home/usr/Documents, ~/Documents/abc, …

- Lệnh `cat` - hiển thị nội dung toàn bộ file

Cách sử dụng của lệnh này về cơ bản cũng rất dễ, chỉ cần `cat [filename]`, và sau đó ta có thể thấy được toàn bộ nội dung của file.

Tuy nhiên, một hạn chế của cat là khi in ra nội dung của file thì nếu file quá dài ta không thể xem hết được, mà buộc phải kết hợp với các câu lệnh khác.

- Phân trang với less

Lệnh `less` là một bổ sung cần thiết cho `cat` khi xem nội dung của file. Với tính năng phân trang dữ liệu, less có thể giúp chúng ta xem toàn bộ nội dung của một file dài. Cú pháp sử dụng cũng chỉ cần `less [filename]`, khá tương đồng với `cat`.

- Lệnh `touch` - tạo file

Mặc dù có rất nhiều câu lệnh có thể dùng để tạo file, nhưng lệnh cơ bản nhất vẫn là `touch`, câu lệnh có tác dụng tạo ra một file với tên và đường dẫn chỉ định. Cú pháp cơ bản là `touch [filename_with_path]`. Nếu chỉ có filename thì mặc định là file sẽ được tạo ra ở thư mục hiện tại. Ta có thể tạo nhiều file cùng lúc với `touch`.

- Tạo thư mục với `mkdir`

Tương tự với `touch`, `mkdir` cũng có tác dụng tạo ra 1 file, nhưng file ở đây là dạng file thư mục. Đặc biệt, có thể dùng tùy chọn `-p` để tạo cả 1 cây thư mục.

- Lệnh `cp` (copy)

Dùng để sao chép tập tin hay thư mục đến một thư mục khác.

	- `cp [tên tập tin] [tên thư mục]`: dùng để copy một tập tin vào một thư mục
	- `cp -r [tên thư mục nguồn] [tên thư mục đích]`: dùng để copy thư mục nguồn vào thư mục đích

- Lệnh `mv` (move)

Dùng để di chuyển tập tin đến một thư mục mới đồng thời đổi tên tập tin đó.

	- `mv [tên tập tin cũ] [tên thư mục đích / tên tập tin mới]`: di chuyển một tập tin đến thư mục mới đồng thời đổi tên tập tin.
	- `mv [tên tập tin cũ] [tên thư mục đích]`: di chuyển tập tin đến thư mục đích và không đổi tên.

- Xóa file hoặc thư mục

Để xóa file, ta dùng lệnh `rm`, còn để xóa một thư mục, ta dùng lệnh `rmdir`. Tuy nhiên, `rmdir` có một hạn chế là chỉ xóa được thư mục trống. Để xóa cả một cây thư mục, ta cần sử dụng `rm` với tùy chọn `-r`.

Nếu như bạn đã quen với việc sử dụng Linux, thì có một lệnh được liệt kê vào danh sách lệnh nguy hiểm tuyệt đối không nên thao tác, đó là `rm -rf /`. Khi thực thi lệnh này, tất cả cây thư mục tính từ root sẽ bị xóa (-r), và không hỏi lại (-f). Nếu bạn không chắc chắn, thì tốt nhất không nên sử dụng tùy chọn `-r`, hoặc có thể sử dụng `-i` (sẽ hỏi trước khi xóa để chắc chắn).

- Dùng trình soạn thảo `vi`

Linux có nhiều chương trình cho phép soạn thảo văn bản như: vi, emacs, joe, pico,… chương trình soạn thảo văn bản thông dụng nhất đó là vi.

Khi `vi` khởi động sẽ ở chế độ dòng lệnh. Để chuyển đổi từ chế độ dòng lệnh sang chế độ soạn thảo thì nhấn phím insert. Để trở lại chế độ dòng lệnh thì chọn phím ESC

`vi [đường dẫn file]`

Ví dụ: Tạo tập tin 123.txt và đặt trong thư mục /usr/bin với nội dung là "dung trinh soan thao vi"

Bước 1: Dùng lệnh `vi` để tạo tập tin 123.txt. Nếu tập tin này đã có thì cũng dùng `vi` để mở và cũng theo cú pháp ở trên.

`vi 123.txt`

Bước 2: Nhấn phím "i" để nhập nội dung "dung trinh soan thao vi".

Bước 3: Nhấn phím ESC để nhập một trong các yêu cầu sau:

	- `:q!`: thoát mà không lưu văn bản.
	- `:wq`: Lưu và thoát khỏi tập tin.