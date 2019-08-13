## Cấu trúc Kernel và quá trình khởi động trong Linux và các INIT Level

#### Cấu trúc kernel Linux

Về mặt kỹ thuật, không chính xác khi coi Linux là một hệ điều hành hoàn chỉnh. Linux thực sự chỉ đề cập cụ thể đến kernel, được đặt theo tên của người sáng lập Linus Torvalds. Mọi thứ bạn thấy trên màn hình đều đến từ các dự án và những nhà phát triển khác.

Torvalds đã tạo ra Linux kernel vào năm 1991. Ban đầu, ông đặt tên cho dự án là Freax (kết hợp giữa các từ “free”, “freak” và “UNIX”). Sau đó nó được đổi tên thành Linux cho đến ngày nay.

Đây là thành phần quan trọng của mọi hệ điều hành, và được ví như trái tim của HĐH, kernel sẽ chứa các module hay các thư viện để quản lý và giao tiếp giữa phần cứng máy tính và các ứng dụng.

Vì được phát hành với bản quyền GNU - General Public License. Do đó mà bất cứ ai cũng có thể tải và xem mã nguồn của Linux, thậm chí việc chỉnh sửa và phát triển một distro riêng cho mình. Mọi thông tin khác về kernel như phiên bản, thông tin cập nhật,... bạn có thể xem tại [đây](www.kernel.org).

Linux kernel gồm một số thành phần chính sau:

![Ảnh](https://developer.ibm.com/developer/articles/l-linux-kernel/images/figure3.jpg)

- Giao diện lời gọi hệ thống (System call interface – SCI)

SCI thực hiện các lời gọi hệ thống từ vùng ứng dụng vào nhân Linux. Giao diện này độc lập với kiến trúc bộ vi xử lý ngay cả trong cùng một họ vi xử lý. SCI có thể thực hiện các dịch vụ gọi hàm dồn kênh và tách kênh. Các gói liên quan được cài trong thư mục ẩn ./linux/kernel và phần độc lập với kiến trúc vi xử lý nằm trong `./linux/arch`.

- Quản lý các tiến trình (Process management)

Quản lý tiến trình đảm bảo việc thực hiện các tiến trình. Trong vùng nhân Linux, mỗi tiến trình được gọi là một mạch lệnh (thread) và được thể hiện thành một vi xử lý ảo (gồm mã lệnh, dữ liệu, các ngăn xếp và các thanh ghi của CPU). Trong vùng ứng dụng thì chỉ dùng từ tiến trình mặc dù Linux không phân biệt hai khái niệm này (threads và processes). Nhân cung cấp một giao diện lập trình ứng dụng (API) để: tạo tiến trình mới (fork, exec hoặc các hàm POSIX), ngừng tiến trình (kill, exit) và thông tin, đồng bộ giữa các tiến trình (signal hoặc các cơ cấu POSIX).

Quản lý tiến trình còn dùng để chia sẻ CPU giữa các mạch lệnh đang hoạt động. Nhân thực hiện một thuật toán lập lịch cố định bất kể đến các mạch lệnh đang tranh chấp quyền sử dụng CPU. Lịch này cũng hỗ trợ cả chế độ đa xử lý đối xứng (Symmetric MultiProcessing – SMP). Các gói liên quan được cài trong thư mục ẩn `./linux/kernel` và phần độc lập với kiến trúc vi xử lý nằm trong `./linux/arch`.

- Quản lý bộ nhớ (Memory management)

Một tài nguyên quan trọng khác mà nhân Linux quản lý là bộ nhớ. Để sử dụng bộ nhớ hiệu quả theo cách mà phần cứng quản lý bộ nhớ ảo, bộ nhớ được chia thành các trang (mỗi trang là 4KB đối với phần lớn loại vi xử lý). Linux có các cơ cấu quản lý lượng bộ nhớ khả dụng và các cơ cấu phần cứng để mapping giữa bộ nhớ vật lý và bộ nhớ ảo.

Việc quản lý bộ nhớ còn làm nhiều hơn là chỉ quản lý các trang 4KB. Linux dùng một sơ đồ định vị lát (slab allocator) lên trên mỗi trang. Sơ đồ này dùng trang 4KB làm cơ sở nhưng tạo một cấu trúc bên trong, theo dõi trang nào đầy, trang nào mới dùng một phần, trang nào còn trống.

Khi nhiều user sử dụng bộ nhớ, dung lượng có thể không đủ. Khi đó các trang nhớ được chuyển sang ổ cứng. Quá trình này được gọi là trao đổi (swapping) giữa bộ nhớ và ổ cứng. Các gói phần mềm liên quan đến quản lý bộ nhớ đặt trong thư mục `./linux/mm`.

- Hệ thống file ảo (Virtual file system)

Hệ thống file ảo (VFS) là một khía cạnh hay của nhân Linux, cung cấp một giao diện trừu tượng hoá chung cho hệ thống file. VFS tạo nên một lớp chuyển đổi giữa SCI và các hệ thống file của Linux.

![Ảnh](https://i.imgur.com/VpNgjRn.jpg)

Nằm trên cùng của VFS là lớp các API các chức năng như mở, đóng, đọc, viết file. Dưới cùng của VFS là lớp trừu tượng hệ thống file xác định các chức năng lớp trên thực hiện như thế nào. Đó là các plug-in đối với một hệ thống file cho trước (có trên 50 plug-in như vậy). Các phần mềm liên quan đến VFS nằm trong thư mục ./linux/fs.

Bên dưới lớp file hệ thống là bộ đệm cache (buffer cache) gồm các chức năng chung cho mọi hệ thống file (không phụ thuộc vào một kiểu hệ thống file riêng biệt nào). Lớp cache này tối ưu hoá việc truy cập vào các thiết bị vật lý bằng cách giữ dữ liệu trong một thời gian ngắn (hoặc đọc trước sao cho dữ liệu luôn có khi cần). Dưới bộ đệm cache là các driver thiết bị là giao diện của các thiết bị vật lý cụ thể.

- Các ngăn xếp mạng (Network stack)

Các ngăn xếp mạng được thiết kế theo một kiến trúc lớp mô phỏng theo đúng kiến trúc lớp của các giao thức. Nhắc lại rằng IP là giao thức lớp mạng lõi nằm bên dưới giao thức vận chuyển (thường là TCP). Bên trên TCP là lớp socket được gọi đến qua SCI.

Lớp socket là API chuẩn của hệ thống con network, tạo nên một giao diện cho các giao thức mạng khác nhau. Lớp socket quy định một cách quản lý kết nối và di chuyển dữ liệu chuẩn hoá giữa các điểm đầu cuối. Tài nguyên mạng nằm ở thư mục `./linux/net`.

- Các driver thiết bị (Device drivers)

Phần lớn mã nguồn của nhân Linux là các driver để điều khiển các thiết bị phần cứng. Cây thư mục của mã nguồn nhân Linux có một thư mục con driver trong đó có các thư mục con ứng với các thiêt bị khác nhau. Mã nguồn driver nằm ở `./linux/drivers`.

- Mã lệnh phụ thuộc kiến trúc vi xử lý (Architecture-dependent code)

Phần lớn Linux độc lập với kiến trúc vi xử lý, nhưng cũng có những bộ phận cần phải theo đúng từng kiến trúc cụ thể để hoạt động được và hiệu quả. Thư mục con `./linux/arch` chứa các mã nguồn phụ thuộc kiến trúc đó. Ví dụ với một máy trạm tiêu biểu, thư mục đó là i386

#### Quá trình khởi dộng trong Linux và các init level

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

- Các script trong INITRD được thực thi

Một vấn đề mà những người viết script đa mục đích phải đối mặt là: không thể nào đoán trước được chính xác cấu trúc máy tính của người dùng sẽ sử dụng bản Linux của họ... Máy tính của người dùng có những thành phần linh kiện nào.

Các INITRD cung cấp một giải pháp: một tập các chương trình nhỏ sẽ được thực thi khi kernel vừa mới được khởi chạy. Các chương trình nhỏ này sẽ dò quét phần cứng của hệ thống và xác định xem kernel cần được hỗ trợ thêm những gì dể có thể quản lý được các phần cứng đó. Chương trình INITRD có thể nạp thêm vào kernel các module bổ trợ. Khi chương trình INITRD kết thúc thì quá trình khởi động Linux sẽ tiếp diễn.

- Chương trình init được thực thi

Khi kernel được khởi chạy xong, nó gọi đến 1 chương trình duy nhất tên là init.

Tiến trình này có PID = 1, đây là "init cha" của các chuwong trình khác trên linux, do vậy nó sẽ không thể bị "kill".

Sau đó, init sẽ xem trong file `/etc/inittab` để biết được nó cần làm gì tiếp theo như: dựa vào runlevel mặc định để thực thi các script khởi động (initscript) tương ứng trong thư mục `/etc/rc.d`.

- Các initscript được thực thi dựa trên runlevel được chọn

Nếu kiểm tra trong file `/etc/inittab`, bạn sẽ thấy nó bao gồm hầu hết các đặc tả, chỉ dẫn để chạy các chương trình nào đó. Các script có tên bắt đầu bằng kí tự `S` sẽ được thực thi, bằng cách này, init sẽ khởi động tất cả các hệ thống con (subsystem) hoặc các dịch vụ (daemon) để tạo thành một hệ thống linux hoạt động hoàn chỉnh.

Tại thời điểm này, về cơ bản Linux đã khởi động xong, init cũng hoàn thành vai trò của mình: tạm thời, nó sẽ "ngủ" (ở trạng thái chờ đợi) cho tới khi có chương trình nào đó "chết" hoặc cần được khởi động lại. Tất cả các hoạt động của hệ thống bây giờ sẽ được thực hiện bởi các daemon khác nhau.

- Đăng nhập với giao diện đồ họa

Subsystem cuối cùng được init khởi động lên là XWindow, đây là một hệ thống cung cấp giao diện đồ họa cho người dùng (GUI) của Linux.

- Khi người dùng đăng nhập thành công vào hệ thống

Một chương trình shell (bash, sh, csh, ...) sẽ được bắt đầu.

Tất cả các chương trình mà bạn chạy và mọi thao tác khác mà bạn thực hiện trong suốt phiên làm việc sẽ được thực hiện bởi shell đó hoặc bởi chương trình khác mà được shell khởi động.

Khi bạn đăng xuất, shell đó và tất cả các tiến trình con của nó sẽ kết thúc. Sau đó, init sẽ "thức tỉnh" và bắt đầu một lời nhắc nhở đăng nhập mới.

Toàn bộ quá trình khởi động của hệ thống Linux được minh họa như hình sau:

![Ảnh](https://i.imgur.com/vjlbvV7.png)