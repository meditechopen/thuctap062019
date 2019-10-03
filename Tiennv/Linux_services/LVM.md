## Logical Volume Manager (LVM)

Logical Volume Manager (LVM): là phương pháp cho phép ấn định không gian đĩa cứng thành những logical volume khiến cho việc thay đổi kích thước trở nên dễ dàng hơn (so với partition). Với kỹ thuật Logical Volume Manager (LVM) bạn có thể thay đổi kích thước mà không cần phải sửa lại table của OS. Điều này thật hữu ich với những trường hợp bạn đã sử dụng hết phần bộ nhớ còn trống của partition và muốn mở rộng dung lượng của nó

#### Vai trò

LVM là kỹ thuật quản lý việc thay dổi kích thước lưu trữ của ổ cứng

- Không để hệ thống bị gián đoạn hoạt động

- Có thể kết hợp Hot Swapping (thao tác thay thế nóng các thành phần bên trong máy tính)

- LVM có thể gom nhiều ổ đĩa cứng thành một ổ ảo, giúp tăng kích thước lưu trữ.

#### Các thành phần trong LVM

Ta có mô hình các thành phần trong LVM

<img src="img/101.png">

- Hard Drives -driver: thiết bị lưu trữ dữ liêu, ví dụ như trong linux nó là /dev/sda, /dev/sdb, ...

- Partition: là các phâ vùng của hard driver, mỗi hard driver có 4 partition, trong đó partition bao gồm 2 loại là primary và extend partition

	- Primary partition: phân vùng chính, có thể khởi động. Mối đĩa cứng có tối đa 4 phân vùng này
	
	- Extended partition: phân vùng mở rộng, có thể tạo 
	
- Physical Volumes: là 1 cách gọi khác của partition trong kỹ thuật LVM, là thành phần cơ bản được sử dụng bởi LVM. 1 physical volume không thể mở rộng ra ngoài pham vi 1 ổ đĩa. Có thể kết hợp nhiều physical volume thành volume groups

- Volume Group: nhiều physical volume trên những ổ khác nhau được kết hợp lại thành 1 volume group. Volume Group được sử dụng để tạo ra các Logical Volume, trong đó người dùng có thể tạo, thay đổi kích thước, lưu trữ, gỡ bỏ và sử dụng. Với LVM Volume Group được xem như một ổ đĩa ảo.

<img src="img/102.png">

> Một điểm cần lưu ý là boot loader không thể đọc /boot khi nó nằm trên Volume Group. Do đó không thể sử dụng kỹ thuật LVM với /boot mount point

- Logical Volume: Volume Group được chia nhỏ thành nhiều Logical Volume, mỗi Logical Volume có ý nghĩa tương tự như partition. Nó được dùng cho các mount point và được format với những định dạng khác nhau như ext2, ext3, ext4,… Khi dung lượng của Logical Volume được sử dụng hết ta có thể đưa thêm ổ đĩa mới bổ sung cho Volume Group và do đó tăng được dung lượng của Logical Volume. Ví dụ bạn có 4 ổ đĩa mỗi ổ 5GB khi bạn kết hợp nó lại thành 1 volume group 20GB, và bạn có thể tạo ra 2 logical volumes mỗi disk 10GB

<img src="img/103.png">

- File Systems: tổ chức và kiểm soát các tập tin. Được lưu trữ trên ổ đĩa cho phép truy cập nhanh chóng và an toàn. Sắp xếp dữ liệu trên đĩa cứng máy tính. Quản lý vị trí vật lý của mọi thành phần dữ liệu

#### Sử dụng LVM

Đầu tiên ta add thêm một số ổ cứng vào máy

Chạy lệnh `lsblk` sẽ thấy có 3 ổ mới được add thêm, mỗi ổ 10GB

<img src="img/104.png">

Trong đó sdb, sdc, sdd là các Hard Drives mà mình mới thêm vào

- Tạo Logical Volume trên LVM

Tạo Partition:

Từ các hard drivers trên hệ thống, ta tạo các partition. Ở đây với ổ sdb tôi sử dụng lệnh `fdisk /dev/sdb`

<img src="img/105.png">

trong đó:

n: thêm partition mới

p: primary partition

1: đánh số partition (từ 1-4)

First sector: để mặc định

Last sector: +1G để partition vùa tạo có dung lượng 1G

t: thay đổi loại partition

8e: hex code của LVM

w: lưu lại

Tương tự, tạo thêm các partition từ sdb và sdc

Tạo Physical Volume:

Tạo các physical volume lần lượt là /dev/sdb1 và /dev/sdc1

```
pvcreate /dev/sdb1
pvcreate /dev/sdc1
```

Bạn có thể kiểm tra các physical volume bằng câu lệnh `pvs` hoặc `pvdisplay`

<img src="img/106.png">

Tạo Volume Group:

Tiếp theo ta sẽ nhóm các physical volume thành 1 volume group

`vgcreate vg-demo1 /dev/sdb1 /dev/sdc1`

"demo1" là tên của volume group

Có thể sử dụng câu lệnh sau để kiểm tra lại các Volume Group đã tạo

`vgs` hoặc `vgdisplay`

<img src="img/107.png">

Tạo Logical Volume:

Từ một Volume Group, chúng ta có thể tạo ra các Logical Volume bằng cách sử dụng lệnh sau

`lvcreate -L 1G -n lv-demo1 vg-demo1`

trong đó:

"-L": Chỉ ra dung lượng của logical volume

"-n": Chỉ ra tên của logical volume

lv-demo1 là tên Logical Volume, vg-demo1 là Volume Group mà tôi tạo ở bước trước

> Lưu ý là chúng ta có thể tạo nhiều Logical Volume từ 1 Volume Group

Có thể sử dụng câu lệnh sau để kiểm tra lại các Logical Volume đã tạo

`lvs` hoặc `lvdisplay`

<img src="img/108.png">

Mount và sử dụng:

Tôi sẽ tạo ra một thư mục để mount Logical Volume đã tạo vào thư mục đó

`mkdir demo1`

Format các Logic Volume thành các định dạng như ext2, ext3, ext4

`mkfs -t ext4 /dev/vg-demo1/lv-demo1`

<img src="img/109.png">

Tiến hành mount logical volume lv-demo1 vào thư mục demo1 như sau

`mount /dev/vg-demo1/lv-demo1 demo1`

Kiểm tra lại dung lượng của thư mục đã được mount

`df -h`

<img src="img/110.png">

> Lưu ý đây là kiểu mount mềm, sẽ bị mất nếu máy khởi động lại. Để có thể sử dụng ngay cả khi reboot máy cần phải mount cứng.

- Thay đổi dung lượng Logical Volume trên LVM:

