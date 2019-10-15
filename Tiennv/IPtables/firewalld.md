## Firewalld

Firewalld cung cấp một tường lửa được quản lý động với sự hỗ trợ cho các mạng / vùng tường lửa xác định mức độ tin cậy của các kết nối hoặc giao diện mạng. Nó có hỗ trợ cho các cài đặt tường lửa IPv4, IPv6, cầu nối ethernet và bộ IP. Có một sự tách biệt giữa thời gian chạy và các tùy chọn cấu hình vĩnh viễn. Nó cũng cung cấp giao diện cho các dịch vụ hoặc ứng dụng để thêm các quy tắc tường lửa trực tiếp.

#### Lợi ích khi sử dụng Firewalld

Các thay đổi có thể được thực hiện ngay lập tức trong môi trường runtime. Không cần khởi động lại các dịch vụ hoặc các deamon

Với giao diện tường lửa D-Bus, thật đơn giản cho các dịch vụ, ứng dụng và cả người dùng để điều chỉnh các cài đặt tường lửa. Giao diện hoàn tất và được sử dụng cho các công cụ cấu hình tường lửa firewall-cmd, firewall-config và firewall-applet.

Việc tách biệt cấu hình runtime và vĩnh viễn giúp có thể thực hiện các phép thử và kiểm tra trong thời gian chạy. Cấu hình runtime chỉ hợp lệ cho đến khi dịch vụ được reload, restart lần tiếp theo hoặc khi hệ thống được khởi động lại. Sau đó cấu hình vĩnh viễn sẽ được tải lại. Với môi trường runtime, có thể sử dụng để dành cho các cài đặt chỉ hoạt động trong 1 khoảng thời gian giới hạn. Nếu cấu hình runtime đã được sử dụng để đánh giá và không có bất cứ trục trặc khi hoạt động nào thì nó có thể lưu vào cấu hình vĩnh viễn

#### Đặc trưng

- API D-Bus hoàn chỉnh

- Hỗ trợ IPv4, IPv6, cầu nối và ipset

- Hỗ trợ NAT IPv4 và IPv6

- Firewall zones

- Danh sách các zones, services và icmptypes được xác định trước

- Simple service, cổng, giao thức, cổng nguồn, masquerading, port forwarding, icmp filter, rich rule, interface và source address handlig trong zones

- Định nghĩa dịch vụ đơn giản với các cổng, giao thức, cổng nguồn, mô-đun (netfilter helpers) và xử lý địa chỉ đích

- Ngôn ngữ phong phú cho các quy tắc linh hoạt và phức tạp hơn trong zones

- Thời gian quy tắc tường lửa trong zones

- Nhật ký đơn giản của các gói bị từ chối

- Giao diện trực tiếp

- Khóa cứng: Whitelist các ứng dụng có thể sửa đổi tường lửa

- Tự động tải các mô-đun hạt nhân Linux

- Tích hợp với Puppet

- Gợi ý dòng lệnh cho cấu hình trực tuyến và ngoại tuyến

- Công cụ cấu hình đồ họa bằng gtk3

- Applet sử dụng Qt4

#### Các distro sử dụng

Firewalld được sử dụng trên các bản phân phối linux sau làm công cụ quản lý tường lửa mặc định

- Rhel 7, CentOS 7

- Fedora 18 và mới hơn

- Có sẵn cho 1 số bản phân phối khác

#### Cấu trúc

Firewalld có thiết kế 2 lớp: lớp lõi ở dưới và lớp D-Bus ở trên cùng. Lớp lõi chịu trách nhiệm xử lý cấu hình và back ends như iptables, ip6tables, ebtables, ipset và bộ nạp module

Giao diện tường lửa D-Bus là cách chính để thay đổi và tạo cấu hình tường lửa. Giao diện được sử dụng bởi tất cả các công cụ trực tuyến do tường lửa cung cấp, ví dụ như firewall-cmd, firewall-config và firewall-applet. firewall-offline-cmd không giao tiếp với firewalld, nhưng thay đổi và tạo các tệp cấu hình firewalld sử dụng trực tiếp lõi firewalld với trình xử lý IO. firewall-offline-cmd có thể được sử dụng trong khi firewalld đang chạy, nhưng điều này không được khuyến khích

<img src="img/06.png">

#### Sự khác biệt giữa IPtables với firewalld

Firewalld là phiên bản firewall mới mặc định được sử dụng trong các phiên bản Rhel 7 để thay thế cho interface của IPtables. Về bản chất nó vẫn kết nối tới netfilter kernel code. Tuy nhiên, trái ngược với IPtables, firewalld có thể thay đổi cài đặt trong quá trình hoạt động bình thường mà không bị mất kết nối

Hình dưới đây mô tả mối quan hệ giữa IPtables và firewalld

<img src="img/07.png">

Như vậy cả 2 đều sử dụng IPtables tool để giao tiếp với kernel packet filter

Đối với các tệp cấu hình, IPtables sử dụng /etc/sysconfig/iptables và /etc/sysconfig/ip6tables, còn firewalld lại lưu nó dưới dạng 1 loạt các file xml trong /usr/lib/firewalld và /etc/firewalld. Tuy nhiên các tệp iptables và ip6tables sẽ không tồn tại nếu chưa cài đặt IPtables service bởi mặc định firewalld mới là dịch vụ được cài đặt

Firewalld sử dụng "zones" và "services" thay vì "chain" và "rules" trong IPtables

Firewalld quản lý các quy tắc được thiết lập tự động, chỉ những thay đổi mới được áp dụng, có tác dụng ngay lập tức mà không làm mất đi các kết nối và session hiện có

Đối với IPtables, mỗi 1 thay đổi đồng nghĩa với việc hủy bỏ toàn bộ các rules cũ và load lại 1 loạt các rules mới trong tệp iptables hoặc ip6tables.

#### 1 số khái niệm trong firewalld

- Zones

Trong firewalld, zone là 1 nhóm các quy tắc nhằm chỉ ra những luồng dữ liệu được cho phép, dựa trên mức độ tin tưởng của điểm xuất phát luồng dữ liệu đó trong hệ thống mạng. Có một số zones được xác định trước được cung cấp bởi firewalld.

Các zones được xác định trước theo mức độ tin cậy, theo thứ tự từ ít tin cậy nhất đến đáng tin cậy nhất

1. drop: ít tin cậy nhất, toàn bộ các kết nối đến sẽ bị từ chối mà không phản hồi, chỉ cho phép duy nhất kết nối đi ra

2. block: tương tự như drop nhưng các kết nối đến bị từ chối và phản hồi bằng thông báo từ icmp-host-prohibited (hoặc icmp6-adm-prohibited)

3. public: đại diện cho mạng công cộng, không đáng tin cậy. Các máy tính / services khác không được tin tưởng trong hệ thống nhưng vẫn cho phép các kết nối đến trên cở sở chọn từng trường hợp cụ thể

4. external: hệ thống mạng bên ngoài trong trường hợp bạn sử dụng tường lửa làm gateway, được cấu hình giả lập nat để giữ bảo mật mạng nội bộ mà vẫn có thể truy cập

5. internal: đối lập với external zone, sử dụng cho phần nội bộ của gateway. Các máy tính / services thuộc zone này khá đáng tin cậy

6. dmz: sử dụng cho các máy tính / services trong khu vực dmz (demilitarized) - cách ly không cho phép truy cập vào phần còn lại của hệ thống mạng, chỉ cho phép 1 số kết nối đến nhất định

7. work: sử dụng trong công việc, tin tưởng hầu hết các máy tính và 1 vài services được cho phép hoạt động

8. home: môi trường gia đình - tin tưởng hầu hết các máy tính và thêm 1 vài services được cho phép hoạt động

9. trusted: đáng tin cậy nhất - tin tưởng toàn bộ thiết bị trong hệ thống

- Rule

1 quy tắc là 1 phần của zone, là thẻ phần tử tùy chọn và có thể được sử dụng nhiều lần để có mục nhập rich language rule. 1 vùng có thể chứa 1 số quy tắc. Nếu 1 số quy tắc tương tác / mấu thuẫn, quy tắc đầu tiên phù hợp sẽ "chiến thắng"

Cấu trúc quy tắc chung

```
<rule [family="ipv4|ipv6"]>
  [ <source address="address[/mask]" [invert="True"]/> ]
  [ <destination address="address[/mask]" [invert="True"]/> ]
  [
    <service name="string"/> |
    <port port="portid[-portid]" protocol="tcp|udp"/> |
    <protocol value="protocol"/> |
    <icmp-block name="icmptype"/> |
    <masquerade/> |
    <forward-port port="portid[-portid]" protocol="tcp|udp" [to-port="portid[-portid]"] [to-addr="address"]/> |
    <source-port port="portid[-portid]" protocol="tcp|udp"/> |
  ]
  [ <log [prefix="prefixtext"] [level="emerg|alert|crit|err|warn|notice|info|debug"]/> [<limit value="rate/duration"/>] </log> ]
  [ <audit> [<limit value="rate/duration"/>] </audit> ]
  [
    <accept> [<limit value="rate/duration"/>] </accept> |
    <reject [type="rejecttype"]> [<limit value="rate/duration"/>] </reject> |
    <drop> [<limit value="rate/duration"/>] </drop> |
    <mark set="mark[/mask]"> [<limit value="rate/duration"/>] </mark>
  ]
</rule>
```

- Services

Firewalld service có thể là 1 danh sách các local port, các giao thức cũng như các đích đến và cũng là 1 danh sách các module trình hỗ trợ tường lửa được tải tự động nếu 1 dịch vụ được kích hoạt. Việc sử dụng các dịch vụ được xác định trước giúp người dùng dễ dàng kích hoạt và vô hiệu hóa quyền truy cập vào 1 dịch vụ

1 dịch vụ có chính xác 1 thuộc tính

`name="string"`

tên của dịch vụ sẽ được kích hoạt. Để có được 1 danh sách các tên dịch vụ hợp lệ, hãy nhập `firewall-cmd --get-services`

- Port

Là các cổng được sử dụng cho kết nối. Tất cả các thuộc tính của 1 mục nhập cổng là bắt buộc

`port="portid[-portid]"`

Port có thể là 1 cổng đơn "portid" hoặc nhiều cổng "portid portid portid"

- Rich rule

Rich rule là 1 tính năng bổ sung của firewalld cho phép bạn tạo các quy tắc tường lửa tinh vi hơn. Ví dụ

	- whitelist 1 phạm vi ip ngoại trừ 1 ip trong phạm vi này
	
	- định tuyến lại yêu cầu đến từ 1 cổng và chuyển tiếp nó đến 1 cổng khác
	
	- giới hạn số lượng yêu cầu đến trong mỗi giây / phút / giờ / ngày
	
	- ghi các mục nhật ký cụ thể vào /var/log/message khi có yêu cầu nhất định đi qua

Định dạng của lệnh để thêm rich rule như sau

`firewall-cmd [--zone=zone] --add-rich-rule='rule' [--timeout=timeval]`

tham số timeout được cung cấp, quy tắc hoặc các quy tắc chỉ duy trì hoạt động trong khoảng thời gian được chỉ định và sẽ tự động bị xóa sau đó. Giá trị thời gian có thể được theo sau bởi s(giây), m(phút) hoặc h(giờ) để chỉ định đơn vị thời gian. Mặc định là giây.

nếu muốn xóa bỏ

`firewall-cmd [--zone=zone] --remove-rich-rule='rule'`

- Source

LÀ 1 thẻ phân tử trống tùy chọn được sử dụng để liên kết 1 địa chỉ nguồn, dải địa chỉ, địa chỉ MAC hoặc ipset với 1 zone. 1 mục nguồn có chính xác 1 trong những thuộc tính sau

	- nguồn là đại chỉ ip hoặc địa chỉ ip mạng có subnet mask cho IPv4 hoặc IPv6. Địa chỉ phải phù hợp với họ quy tắc (IPv4 / IPv6). Subnet mask được thể hiện bằng các ký hiệu dấu chấm thập phân (/xxxx) hoặc tiền tố mạng (/x) cho IPv4 và ký hiệu tiền tố (/x) cho các địa chỉ mạng IPv6. Có thể đảo ngược ý nghĩa của 1 địa chỉ bằng cách thêm "not" trước "address". Tất cả trừ địa chỉ được chỉ định sẽ được khớp sau đó
	
	`address="address[/mask]"`
	
	- nguồn là 1 địa chỉ MAC, nó phải có hình thức `XX:XX:XX:XX:XX:XX`
	
	`mac="MAC"`
	
	- nguồn là 1 ipset
	
	`ipset="ipset"`
	
#### Cài đặt firewalld
	
- Firewalld được cài đặt mặc định trên CentOS / Rhel 7. Nếu chưa cài đặt, hãy chạy lệnh sau

`yum install firewalld`

- Khởi động firewalld

`systemctl start firewalld`

- Kiểm tra tình trạng hoạt động

`systemctl status firewalld`

<img src="img/08.png">

- Thiết lập firewalld khởi động cùng hệ thống

`systemctl enable firewalld`

- Kiểm tra lại

`systemctl is-enabled firewalld`

<img src="img/09.png">

Ban đầu, bạn không nên cho phép firewalld khởi động cùng hệ thống cũng như thiết lập permanent, tránh bị khóa khỏi hệ thống nếu thiết lập sai. Chỉ thiết lập như vậy khi bạn đã hoàn thành các quy tắc tường lửa cũng như test cẩn thận.

- Khởi động lại

```
systemctl restart firewalld
firewall-cmd --reload
```

- Dừng và vô hiệu hóa firewalld

```
systemctl stop firewalld
systemctl disable firewalld
```

#### Cấu hình firewalld

- Thiết lập các zones

Liệt kê tất cả các zones trong hệ thống

`firewall-cmd --get-zones`

<img src="img/10.png">

Kiểm tra zone mặc định

`firewall-cmd --get-default-zone`

