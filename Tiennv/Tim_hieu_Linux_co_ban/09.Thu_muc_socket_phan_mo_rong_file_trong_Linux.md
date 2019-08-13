## Thư mục, socket, phần mở rộng file trong Linux

#### Thư mục

Một thư mục là một vị trí để lưu trữ các tập tin trên máy tính của bạn. Các thư mục được tìm thấy trong một hệ thống tệp phân cấp, chẳng hạn như Linux , MS-DOS , OS/2 và Unix.

Một thư mục được sử dụng để lưu trữ, sắp xếp và tách các tệp và thư mục trên máy tính. Ví dụ: bạn có thể có một thư mục để lưu trữ hình ảnh và một thư mục khác để lưu trữ tất cả các tài liệu của bạn. Bằng cách lưu trữ các loại tệp cụ thể trong một thư mục, bạn có thể nhanh chóng chuyển sang loại tệp bạn muốn xem. Nói cách khác, nếu bạn muốn tìm một hình ảnh, bạn có thể mở thư mục hình ảnh và tìm thấy nó nhanh hơn rất nhiều nếu bạn có thể lưu trữ tất cả các tệp trong cùng một thư mục.

Thư mục cũng được sử dụng như 1 nơi dùng để lưu trữ các chương trình. Ví dụ khi bạn cài đặt 1 chương trình trên máy tính, tất cả các tệp cảu nó được lưu trữ trong 1 thư mục liên quan đến chương trình đó. Bằng cách lưu trữ 1 chương trình trong thư mục riêng của mình, nó giúp ngăn các tệp có cùng tên bị ghi đè, sửa đổi hoặc bị xóa bởi các chương trình khác.

Mọi thứ trong Linux/UNIX đều dựa trên hệ thống tệp. Hệ thống tệp bao gồm nhiều thư mục khác nhau (Windows gọi chúng là "thư mục".) Thư mục gốc ("/") nằm ở cơ sở của hệ thống tệp. Một số thư mục có thể nằm trên các phân vùng hoặc ổ đĩa khác nhau, nhưng chúng vẫn là một phần của hệ thống tệp.

#### Socket

Socket là điểm cuối của liên kết giao tiếp hai chiều giữa hai chương trình đang chạy trên mạng. Bạn cũng có thể giao tiếp giữa hai tiến trình thông qua socket trên cùng một máy nhưng chủ yếu nó được sử dụng để giao tiếp qua mạng. Socket được hỗ trợ bởi các hệ điều hành khác nhau như window, MAC, Linux, Unix, v.v.

Để chính xác hơn nữa, một socket là một sự kết hợp của địa chỉ IP và một port trên một hệ thống. Trên mỗi hệ thống, một socket tồn tại để một process tương tác với socket của một process thuộc hệ thống khác trên mạng.

Socket thường được giao tiếp bởi giao diện lập trình ứng dụng (API) được cung cấp bởi hệ điều hành. API cho phép các chương trình sử dụng socket mạng và kết nối với một máy khác qua mạng.

Socket được sử dụng trong ứng dụng mô hình client - server. Nó được tạo ra ở cả hai phía của máy khách và máy chủ để liên lạc với nhau. Socket giao tiếp qua mạng bằng địa chỉ IP và số cổng. Địa chỉ IP là giá trị số được gán cho từng máy tính và thiết bị sử dụng giao thức internet để liên lạc. Cổng là cách để xác định quy trình cụ thể mà internet hoặc tin nhắn mạng khác được chuyển tiếp khi đến máy chủ.

Có 2 loại socket được sử dụng rộng rãi là: stream sockets và datagram sockets.

- Stream sockets: Dựa trên giao thức TCP (Tranmission Control Protocol), là giao thức hướng luồng (stream oriented). Việc truyền dữ liệu chỉ thực hiện giữa 2 tiến trình đã thiết lập kết nối. Giao thức này đảm bảo dữ liệu được truyền đến nơi nhận một cách đáng tin cậy, đúng thứ tự nhờ vào cơ chế quản lý luồng lưu thông trên mạng và cơ chế chống tắc nghẽn.

- Datagram sockets: Dựa trên giao thức UDP (User Datagram Protocol), là giao thức hướng thông điệp (message oriented). Việc truyền dữ liệu không yêu cầu có sự thiết lập kết nối giữa tiến quá trình. Ngược lại với giao thức TCP thì dữ liệu được truyền theo giao thức UDP không được tin cậy, có thế không đúng trình tự và lặp lại. Tuy nhiên vì nó không yêu cầu thiết lập kết nối không phải có những cơ chế phức tạp nên tốc độ nhanh…ứng dụng cho các ứng dụng truyền dữ liệu nhanh như chat, game…..

#### Phần mở rộng file

Một phần mở rộng tên tệp, thường được gọi là phần mở rộng, thường được định nghĩa là một chuỗi ngắn (nghĩa là chuỗi ký tự ) được thêm vào cuối tên cơ sở (nghĩa là phần chính của tên) của tệp sau  một dấu chấm để chỉ ra loại tệp.

Một số hệ điều hành , chẳng hạn như MS-DOS và các hệ thống Microsoft Windows, yêu cầu sử dụng các phần mở rộng để hệ thống hoạt động và hầu như mọi tệp đều có phần mở rộng. Tuy nhiên, điều này có thể không phải lúc nào cũng rõ ràng vì hệ thống có thể được cấu hình để các phần mở rộng bị ẩn khỏi chế độ xem.

Bản thân Linux và các hệ điều hành tương tự Unix khác thường không yêu cầu sử dụng các phần mở rộng, mặc dù một số chương trình ứng dụng chạy trên chúng. Tuy nhiên, ngay cả khi các tiện ích mở rộng không thực sự cần thiết, chúng vẫn được sử dụng thường xuyên vì chúng có thể giúp người dùng dễ dàng biết nhanh hơn về loại tệp.

Một số tiện ích mở rộng phổ biến được sử dụng trên các hệ điều hành giống Unix / Linux là:

- .c - C language source code

- .conf and cfg - configuration file

- .deb - Debian software package

- .py - Python script

- .rpm - an rpm package

- .sh - a shell script

- .src - một tệp mã nguồn. Được viết bằng văn bản thuần túy, một tệp nguồn phải được biên dịch để sử dụng

- .tar - tệp tin nén được tạo bằng tiện ích tar

- .txt : tệp văn bản ASCII đơn giản