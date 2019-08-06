## File system trong Linux

#### Nói đơn giản FileSystem là thứ xác định các cách thức tổ chức, quản lý dữ liệu hay có thể nói là cách thức quản lý cách dữ liệu được đọc và lưu trên thiết bị. File system cho phép người dùng truy cập nhanh chóng và an toàn khi vào các tệp tin thư mục khi cần thiết.

<img src="img/08.png">

#### Những loại FileSystem được Linux hỗ trợ:

- FileSystem cơ bản: ext2, ext3, ext4, XFS, Btrfs, JFS, NTFS v.v.
- FileSystem dành cho dạng lưu trữ Flash (Thẻ nhớ các thứ..): ubifs, JFFS2, YAFFS v.v.
- FileSystem dành cho cơ sở dữ liệu.
- Filesystem mục đích đặc biệt: procfs, sysfs, tmpfs, squashfs, debugfs,…

Một phân vùng là một vùng chứa trong đó có một filesystem được lưu trữ , trong một số trường hợp thì filesystem có thể mở rộng hơn một phân vùng nếu filesystem sử dụng các liên kết.

#### So sánh giữa hệ thống file (FileSystem) giữa Window và Linux

| | Window | Linux |
| --- | --- | --- |
| Phân vùng | Disk1 | /dev/sda1 |
| Loại Filesystem | NTFS/VFAT | EXT2/EXT3/EXT4/XFS/BTRFS… |
| Mounting Parameters | DrivelLetter | MountPoint |
| Thư mục gốc | C:\ | / |

#### Filesystem Hierarchy Standard

Filesystem của hệ điều hành Linux được tổ chức theo tiêu chuẩn cấp bậc của hệ thống tập tin Filesystem Hierarchy Standard (FHS). Tiêu chuẩn này định nghĩa mục đích của mỗi thư mục.

Hình bên dưới là cấu trúc cây thư mục trong Linux:

<img src="img/09.png">

