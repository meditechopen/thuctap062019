## File and directory size

Thật đơn giản. Sử dụng lệnh "ls" cho các tập tin và lệnh "du" cho các thư mục.

- Kiểm tra kích thước tập tin

| Command | Ý nghĩa |
| --- | --- |
| ls -l filename | Kích thước tệp tin |
| ls -l | Kích thước tất cả tệp tin trong thư mục hiện tại |
| ls -al | Kích thước tất cả tệp tin, kể cả những tệp tin ẩn trong thư mục hiện tại |
| ls -al dir | Kích thước tất cả tệp tin, kể cả những tệp tin ẩn trong thư mục "dir" |

Nhưng lệnh "ls" sẽ không liệt kê kích thước thực tế của các thư mục. Vì vậy, ta sử dụng "du" cho mục đích này.

- Kiểm tra kích thước thư mục

| Command | Ý nghĩa |
| --- | --- |
| du -sh directory_name | Cung cấp cho bạn kích thước tóm tắt (-s) của thư mục ở định dạng có thể đọc được của con người (-h) | 
| du -bsh | Cung cấp cho bạn kích thước (-s) rõ ràng (-b) của tất cả các tệp và thư mục trong thư mục hiện tại ở định dạng có thể đọc được của con người (-h) |

Để lý giải cho việc này, trên output của lệnh "ls -l" là kích thước của không gian trên đĩa được sử dụng để lưu trữ thông tin meta cho thư mục (tức là bảng các tệp thuộc thư mục này). Nếu nó có nghĩa là 1024 thì điều này có nghĩa là 1024 byte trên đĩa được sử dụng (nó luôn phân bổ các khối đầy đủ) cho mục đích này.

Để hiểu rõ hơn điều này, ta hãy cùng xem lại hệ thống tập tin Unix / Linux hoạt động thế nào

Hệ thống tập tin trên Unix/ Linux có 1 số khái niệm riêng biệt để xử lý dữ liệu trên đĩa

- khối dữ liệu: 1 nhóm các khối trên đĩa có nội dung của tệp

- inodes: các khối đặc biệt trên 1 hệ thống tệp, với 1 đại chỉ số duy nhất trong hệ thống tệp đó, chứa siêu dữ liệu về 1 tệp như:
	
	- quyền
	
	- thời gian truy cập / sửa đổi
	
	- kích thước
	
	- con trỏ tới các khối dữ liệu (có thể là danh sách các khối, phạm vi, ...)
	
- tên tệp: là các vị trí phân cấp trên thư mục gốc của hệ thống tệp được ánh xạ tới inodes

Nói cách khác, 1 "tệp tin" thực sự bao gồm 3 thứ khác nhau

1. 1 đường dẫn trong hệ thống tập tin

2. inodes với siêu dữ liệu

3. khối dữ liệu  được trỏ tới bởi inodes

Bạn có thể nghĩ rằng thư mục là 1 tệp chứa 1 loạt các tệp khác. Nhưng điều đó chỉ đúng một nửa. 1 thư mục là 1 tập tin ánh xạ tên tệp thành số inode. Nó không "chứa" các tệp, nhưng trỏ đến tên tệp. Hãy nghĩ về nó như 1 văn bản chứa các mục thế này:

	- . - inode 1234
	
	- .. - inode 200
	
	- document - inode 2008
	
	- README.txt - inode 2009

Các mục trên được gọi là directory entries. Về cơ bản chúng là ánh xạ từ tên tệp tới số inode. 1 thư mục là 1 tệp tin đặc biệt có chứa các directory entries.

Khi ta chạy lệnh "ls -l" trên tập và thư mục sẽ thấy các kích thước khác nhau.

Đầu tiên, khi nói về "kích thước" chúng ta có thể đề cập đến 2 điều

	- filesize - là 1 số được lưu trong inode
	
	- kích thước được phân bổ - là số khối được liên kết với inode nhân với kích thước của mỗi khối

Nói chung, đây không phải cùng 1 số. Hẫy thử chạy "stat" trên 1 tệp "thông thường" và bạn sẽ thấy sự khác biệt này

Bây giờ, chúng ta đi đến sự khác biệt giũa các tệp và thư mục thông thường: ví dụ kích thước 4096 được báo cáo của thư mục là số "filesize" được lưu trong inode thư mục, không phải số lượng mục trong thư mục. Đó không phải là 1 số cố định - đó là các byte tối đa sẽ phù hợp với số khối được phân bổ cho thư mục. Thông thường đây là 512 byte / block x 8 lần khối lượng được phân bổ cho 1 tệp có bất kỳ nội dung nào. Khi thư mục được hiệu chỉnh, nhiều khối dữ liệu được gán cho nó và nó cũng sẽ tối đa hóa các khối đó bằng cách điều chỉnh kích thước tệp cho phù hợp.

Và như vậy, "ls" và "stat" sẽ hiển thị trường kích thước tệp cảu inode của thư mục, được đặt thành kích thước của các khối dữ liệu được gán cho nó