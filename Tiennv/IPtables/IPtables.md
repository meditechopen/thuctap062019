## IPtables

IPtables là 1 tường lửa dựa trên lọc gói, miễn phí và có sẵn trên linux

Thực chất IPtables chỉ là giao diện dòng lệnh để tương tác với tính năng lọc, chỉnh sủa gói, NAT của netfilter framework

IPtables/netfilter gồm 2 phần là netfilter ở trong nhân linux và IPtables nằm ngoài nhân. IPtables chịu trách nhiệm giao tiếp với người dùng và sau đó đẩy các luật của người dùng vào cho netfilter xử lý. Netfilter tiến hành lọc các gói dữ liệu ở mức IP. Netfilter làm việc trực tiếp trong nhân, nhanh và không làm giảm tốc độ của hệ thống

#### Lịch sử

Trước IPtables, các gói phần mềm dùng để quản lý tường lửa trên linux là ipchains trong linux kernel 2.2.x và ipfwadm trong linux kernel 2.0.x, dụa trên BSD. Cả 2 chương trình này đều thay đổi mã mạng để chúng có thể thao tác các gói, vì nhân linux thiếu khung kiểm soát gói chung cho đến khi netfilter được giới thiệu

IPtables giữ lại các ý tưởng chính trong ipfwadm: các danh sách luật, trong đó mõi luật chỉ ra những dấu hiệu cần tìm trong 1 gói tin và các hành động sẽ thực hiện với 1 gói tin thảo mãn các dấu hiệu. ipchains thêm khái niệm chains rules và IPtables mở rộng ra tables. 1 table được tra cứu khi cần quyết định phải nat gói tin, vaf1 table khác chỉ ra phải lọc gói như thế nào.

Cach phân chia này cho phép IPtables sử dụng thông tin mà lớp giám sát kết nối thu được từ gói tin, những thông tin thường gặp trong nat. Điều này làm cho IPtables hiện đại hơn ipchains vì nó có khả năng giám sát trạng thái của kết nối và chuyển hướng, thay đổi hay dừng các gói tin dựa trên trạng thái của kết nối, không chỉ dựa vào nguồn, đích hay nội dung gói tin. 1 tường lửa sử dụng IPtables theo cách này còn được gọi là stateful firewall, trong khi ipchains chỉ là stateless firewall. Ta có thể nói rằng IPtables có thể nhận thức được ngữ cảnh của gói tin đang di chuyển, từ đó đưa ra 1 quyết định đúng đắn hơn cho các gói tin và kết nối

Hiện nay chúng ta có nftables - một sự thay thế cho IPtables được sử dụng trên các bản phân phối linux mới gần đây (ví dụ CentOS 8)

#### Những việc IPtables có thể làm

- xây dựng tường lửa cho hệ thống dựa trên stateless và stateful packet filtering

- triển khai các cụm cluster stateless và stateful firewall với tính sẵn sàng cao

- sử dụng NAT và masquerading để chia sẻ truy cập internet nếu bạn không có đủ địa chỉ IP công cộng

- sử dụng NAT để thực hiện transparent proxies

- hỗ trợ các hệ thống tc và iproute2 được sử dụng để xây dựng các bộ định tuyến theo chính sách và QoS tinh vi

- thực hiệm một số tác vụ (thêm, gây xáo trộn) với packet như thay đổi TOS/DSCP/ECN trong IP header

#### Các thành phần trong IPtables

Cơ chế packet filtering của iptables hoạt động bao gồm 3 thành phần sau: tables, chains và targets.

1. Table

Tường lửa IPtables sử dụng các bảng để tổ chức các quy tắc của nó. Các bảng này phân loại các quy tắc theo loại quyết định mà chúng được sử dụng để đưa ra. Hiện nay có 4 loại table khác nhau:

- Filter table: là một trong những bảng được sử dụng rộng rãi nhất trong iptables. Bảng Filter được sử dụng để đưa ra quyết định về việc có nên để gói tin tiếp tục đến đích dự định hay từ chối yêu cầu của nó hay không. Theo cách nói tường lửa, đây được gọi là "lọc" gói. Bảng này cung cấp phần lớn các chức năng mà mọi người nghĩ đến khi thảo luận về tường lửa

- NAT table: Bảng NAT được sử dụng để thực hiện các quy tắc dịch địa chỉ mạng. Khi các gói vào network stack, các quy tắc trong bảng này sẽ xác định xem và cách sửa đổi địa chỉ nguồn hoặc đích của gói để tác động đến cách gói và bất kỳ lưu lượng phản hồi nào được định tuyến. Điều này thường được sử dụng để định tuyến các gói đến các mạng khi không thể truy cập trực tiếp

- Mangle table: được sử dụng để thay đổi các tiêu đề IP của gói theo nhiều cách khác nhau. Chẳng hạn, bạn có thể điều chỉnh giá trị TTL (Time To Live) của một gói, kéo dài hoặc rút ngắn số bước nhảy mạng hợp lệ mà gói có thể duy trì. Các tiêu đề IP khác có thể được thay đổi theo cách tương tự. Bảng này cũng có thể đặt "dấu" nhân bên trong trên gói để xử lý thêm trong các bảng khác và bằng các công cụ mạng khác. Dấu này không chạm vào gói thực tế, nhưng thêm dấu vào kernel's representation của gói

- Raw table: tường lửa IPtables có trạng thái, nghĩa là các gói được đánh giá liên quan đến mối quan hệ của chúng với các gói trước đó. 1 gói tin có thể thuộc một kết nối mới hoặc cũng có thể là của 1 kết nối đã tồn tại. Các tính năng theo dõi kết nối được xây dựng trên đỉnh của bộ lọc mạng cho phép IPtables xem các gói như một phần của kết nối hoặc phiên liên tục thay vì như một luồng các gói rời rạc, không liên quan. Theo dõi kết nối một cách logic thường được áp dụng rất sớm sau khi gói truy cập vào giao diện mạng. Bảng raw có chức năng được xác định rất hẹp. Mục đích duy nhất của nó là cung cấp một cơ chế đánh dấu các gói để từ chối theo dõi kết nối
