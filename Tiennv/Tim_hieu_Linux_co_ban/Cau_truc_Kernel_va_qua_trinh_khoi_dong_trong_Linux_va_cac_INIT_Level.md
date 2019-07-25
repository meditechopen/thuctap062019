## Cấu trúc Kernel và quá trình khởi động trong Linux và các INIT Level

#### Cấu trúc kernel Linux

#### Quá trình khởi dộng trong Linux

Quá trình khởi động của một máy Linux, từ lúc nhấn nút nguồn để bật máy tính lên cho tới khi bạn có thể sử dụng máy tính để thực hiện các công việc của mình.

- Power-on

BIOS (một phần mềm được nhúng (embedded) vào các chip PROM, EPROM hay các bộ nhớ flash nằm trên các bo mạch chủ) là chương trình được chạy đầu tiên khi bạn nhấn nút nguồn hoặc nút reset trên máy tính của mình. BIOS thực hiện một công việc gọi là POST (Power-on Self-test) nhằm kiểm tra các thông số và trạng thái của các phần cứng máy tính khác nhau như là bộ nhớ, CPU, thiết bị lưu trữ, card mạng, ...
Đồng thời, BIOS cũng cho phép bạn thay đổi các thiết lập, cấu hình của nó.
Nếu quá trình POST thành công, thì sau đó BIOS sẽ cố gắng tìm kiếm và khởi chạy (boot) một hệ điều hành được chứa trong các thiết bị lưu trữ như ổ cứng, CD/DVD, USB, ... Thứ tự tìm kiếm có thể được thay đổi bởi người dùng.

- Master Boot Record (MBR)

Sector đầu tiên (được đánh số 0) của một thiết bị lưu trữ dữ liệu được gọi là MBR, thường sector 0 này có kích thước là 512 byte. Sau khi BIOS xác định được thiết bị lưu trữ nào sẽ được ư tiên để tìm kiếm đầu tiên thì thực chất BIOS sẽ đọc trong MBR của thiết bị này để nạp vào bộ nhớ một chương trình rất nhỏ (dưới 512 byte). Chương trình nhỏ này sẽ định vị và khởi động boot loader - đây là chương trình chịu trách nhiệm cho việc tìm và nạp nhân (kernel) của hệ điều hành.

- Boot loader

Có 2 loại bootloader phổ biến trên linux là GRUB và LILO(tiền thân của Grub). Cả 2 chương trình này đều có chung mục đích: cho phép bạn lựa chọn một trong các hệ điều hành có trên máy tính để khởi động, sau đó chúng sẽ nạp kernel của hệ điều hành đó vao bộ nhớ và chuyển quyền điều khiển máy tính cho kernel này.
Grub hay LILO đều có thể khởi động cho cả Linux và Windows, nhưng ngược lại các bootloader trên Windows (như NTLDR, BOOTMGR) thì không hỗ trợ khởi động cho các hệ điều hành Linux. Trong thế giới Linux, các boot loader cũng có thể nạp thêm các ramdisk hoặc các INITRD.

- Linux kernel được nạp và khởi chạy
Bootloader nạp một phiên bản dạng nén của Linux kernel, và ngay lập tức nó tự giải nén và tự cài đặt mình lên đỉnh bộ nhớ hệ thống - nơi mà nó sẽ nằm ở đó cho đến khi bạn tắt máy.

> updating ...