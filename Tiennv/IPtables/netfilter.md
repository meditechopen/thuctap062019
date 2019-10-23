## netfilter

netfilter là 1 module (hay là 1 framework) được tích hợp sẵn trong nhân Linux 2.4 trở lên, cho phép các hoạt động liên quan đến mạng khác nhau được thực hiện dưới dạng các trình xử lý tùy chỉnh. Netfilter cung cấp các chức năng và hoạt động khác nhau để lọc gói, dịch địa chỉ mạng và cổng cũng như chỉnh sửa gói tin, cũng như các chức năng cần thiết để điều hướng các gói tin qua mạng và cấm các gói đến các vị trí nhạy cảm trong mạng

netfilter đại diện cho 1 tập hợp các hook bên trong kernel linux, cho phép các module kernel cụ thể đăng ký các hàm "callback" với ngăn xếp mạng của kernel. Các hàm đó, thường được áp dụng cho lưu lượng dưới dạng các quy tắc lọc và sửa đổi, được gọi cho mỗi gói đi qua hook tương ứng trong ngăn xếp mạng, tương ứng với các quá trình xử lý 1 packet trước khi vào các socket

#### Lịch sử

Tác giả ban đầu và đứng đầu netfilter/iptableslà Paul "Rusty" Russell. Rusty Russell bắt đầu dự án netfilter/iptables vào năm 1998; ông cũng là tác giả của tiền thân của dự án, ipchains. Khi dự án phát triển, ông thành lập Nhóm Netfilter Core (hay đơn giản là coreteam) vào năm 1999. Phần mềm họ sản xuất (netfilter) sử dụng giấy phép Giấy phép Công cộng GNU (GPL) và vào tháng 3 năm 2000, nó đã được sáp nhập vào phiên bản 2.3.x của Linux kernel mainline.

#### Những đặc điểm chính

- lọc gói không trạng thái (IPv4 và IPv6)

- lọc gói trạng thái (IPv4 và IPv6)

- tất cả các loại chuyển dịch địa chỉ mạng và cổng, ví dụ NAT/NAPT (IPv4 và IPv6)

- cở sở hạ tầng linh hoạt và mở rộng

- nhiều lớp API cho tiện ích mở rộng của bên thứ 3

#### Các thành phần

netfilter bao gồm 1 tập hợp các hook bên trong kernel linux, mỗi hook  lại có chức năng khác nhau

Có 5 hook netfilter mà chương trình có thể đăng ký. Khi các gói tiến triển qau ngăn xếp mạng, chúng sẽ kích hoạt các module kernel đã đăng ký với các hook này. Các hook mà gói tin sẽ kích hoạt tùy thược vào việc gói đến hay đi, đích đến của gói và liệu gói bị drop hay từ chối tại điểm trước đó

Các hook sau biểu thị các điểm được xác định rõ trong ngăn xếp mạng:

- NF_IP_PREROUTING: hook này sẽ được kích hoạt bởi bất kỳ lưu lượng truy cập đến nào ngay sau khi vào ngăn xếp mạng. Hook này được xử lý trước khi bất kỳ quyết định định tuyến nào được đưa ra liên quan đến nơi gửi gói.

- NF_IP_LOCAL_IN: hook này được kích hoạt sau khi gói đến được định tuyến nếu gói được định sẵn cho hệ thống cục bộ

- NF_IP_FORWARD: hook này được kích hoạt sau khi gói đến được định tuyến nếu gói được chuyển tiếp đến máy chủ khác

- NF_IP_LOCAL_OUT: hook này được kích hoạt bởi bất kỳ lưu lượng truy cập ngoài được tạo cục bộ nào ngay khi nó vào ngăn xếp mạng

- NF_IP_POST_ROUTING: hook này được kích hoạt bởi bất kỳ lưu lượng đi hoặc chuyển tiếp nào sau khi định tuyến diễn ra và ngay trước khi được đưa vào đường truyền

Kernel module muốn đăng ký các hook này phải cung cấp số ưu tiên để giúp xác định thứ tự chúng sẽ được gọi khi hook được kích hoạt. Điều này cung cấp phương tiện cho nhiều module (hoặc nhiều nhiên bản của cùng 1 module) được kết nối với từng hook nói theo số thứ tự xác định. Mỗi module sẽ được gọi lần lượt và sẽ trả lại quyết định choi netfilter framework sau khi xử lý cho biết những gì sẽ được thực hiện với gói

#### Sử dụng netfilter hook bên trong kernel

Để sử dụng netfilter bên trong kernel, bạn sẽ cần tạo 1 hàm hook và đăng ký nó bằng các sử dụng cấu trúc `nf_register_hook` nhận `nf_hook_ops*` hoặc cấu trúc `nf_register_net_hook` nhận `struct net*` và `struct nf_hooks_ops`. Bạn cần chọn chức năng tùy thược vào phiên bản kernel

1 ví dụ `struct` chứa các trường:

```
struct nf_hook_ops
{
	/* User fills in from here down. */
	nf_hookfn			*hook;
	struct net_device	*dev;
	void				*priv;
	u_int8_t			pf;
	unsigned int		hooknum;
	/* Hooks are ordered in ascending priority. */
	int					priority;
};
```

- hook: 1 con trỏ tới 1 hàm được gọi ngay khi hook được kích hoạt. Hàm này từ loại `nf_hookfn` có chữ ký khác nhau trong các phiên bản khác nhau của kernel. Hãy chắc chắn hàm này trả về `NF_DROP` (drop gói), `NF_ACCEPT` (để gói tiếp tục trong hành trình của nó) hoặc `NF_QUEUE` (nếu bạn muốn các gói xếp hàng để xử lý trong không gian người dùng)

- hooknum: 1 trong những mã định danh hook (ví dụ: NF_IP_POST_ROUTING)

- pf: mã định danh giao thức (ví dụ: `PF_INET` đối với IPv4)

- priority: mức đọ ưu tiên của hook (trong trường hợp các hook khác được đăng ký trong hệ thống). Ưu tiên này có thể là 1 trong những ưu tiên quy định tại các enum `nf_ip_hook_priorities`, được định nghĩa trong tệp tin `netfilter_ipv4.h` (ví dụ: `NF_IP_PRI_FIRST`, `NF_IP_PRI_RAW`)

