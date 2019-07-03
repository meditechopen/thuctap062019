## Hướng dẫn cài CentOS 7 và Ubuntu 16
Đầu tiên chúng ta nên trang chủ của centOS và Ubuntu để tải bản iso của hệ điều hành :
- CentOS : [https://www.centos.org/download/](https://www.centos.org/download/)
	
- Ubuntu 16.4 : [http://releases.ubuntu.com/16.04/](http://releases.ubuntu.com/16.04/)
### 1. Cài CentOS 7 trên VMware :
- Đầu tiên ta ấn tạo máy ảo mới trên VMware
- nhấn chọn Typical rồi Next

![alt](https://i.imgur.com/hH1Wzeh.png)
- Chọn phương thức cài OS :

![alt](https://i.imgur.com/ihgbhuZ.png)

- Chọn hệ điều hành và phiên bản cài đặt

![alt](https://i.imgur.com/Qxx11bo.png)

- Đặt tên và chọn nơi lưu máy ảo

![alt](https://i.imgur.com/sJRyAbl.png)

- Chọn Install CentOS 7 rồi Enter

![alt](https://i.imgur.com/b1EffgW.png)

- Chọn ngôn ngữ rồi Continue

![alt](https://i.imgur.com/k2D4e5O.png)

- kích vào `Date & Time` để thiết lập thời gian

![alt](https://i.imgur.com/1HLJFwf.png)

- Chọn múi giờ rồi `Done`

![alt](https://i.imgur.com/6FLpDvH.png)

- Kích chọn `Installation Destination ` để chọn ổ đĩa và tạo các Partion

![alt](https://i.imgur.com/BCkePvc.png)

- Chọn ổ đĩa cài đặt OS và chọn 2 phương thức cấu hình partion là tự động hoặc tự cấu hình

![alt](https://i.imgur.com/pJXTsyB.png)

- kích chọn `Network & Hostname` để cài đặt cổng mạng

![alt](https://i.imgur.com/Jtvku9Z.png)

- Chuyển Ethernet sang `ON` để card mạng hoạt động

![alt](https://i.imgur.com/YL7zxo4.png)

- Nhấn `Begin Installation` để bắt đầu cài đặt

![alt](https://i.imgur.com/2d26U4E.png)

- Chọn `Root Password` để thiết lập mật khẩu Root

![alt](https://i.imgur.com/eurfsdG.png)

- Nhập mật khẩu rồi done

![alt](https://i.imgur.com/5C6T6ny.png)

- nhấn `User Creation` để tạo User

![alt](https://i.imgur.com/CRE6FgT.png)

- Nhập tên User và mật khẩu rồi done

![alt](https://i.imgur.com/hz9KFAw.png)

- khi đã hoạt thành, nhấn `Reboot` để khởi động lại

![alt](https://i.imgur.com/ECPUKbj.png)

- nhập tài khoản root và mật khẩu để đăng nhập với quyền Root

![alt](https://i.imgur.com/gsaT2Ze.png)

- Đăng nhập thành công

![alt](https://i.imgur.com/p5ARbvx.png)

- Tạo một snapshot `Begin`

![alt](https://i.imgur.com/yzzQqUF.png)

### 2. Cài Ubuntu 16.4 trên VMware :
- Đầu tiên ta ấn tạo máy ảo mới trên VMware
- nhấn chọn Typical rồi Next
![alt](https://i.imgur.com/hH1Wzeh.png)
- chọn phương thức cài OS :
![Imgur](https://imgur.com/T78cxSl.png)
- chọn kiểu OS và phiên bản :
![Imgur](https://imgur.com/WNw3Y89.png)
- đặt tên và nơi lưu trữ cho máy ảo :
![Imgur](https://imgur.com/jQTID8N.png)
- chọn Install Ubuntu để tiến hành cài đặt :
![Imgur](https://imgur.com/NbGtrtM.png)
- chọn phương thức cài đặt rồi continue
![Imgur](https://imgur.com/U26yxJ7.png)
- có 2 tùy chọn nên lưu ý tại Installation type :
		- Erase disk and install Ubuntu : tùy chọn này sẽ xóa toàn bộ dữ liệu trong máy tính sau khi cài đặt. Chỉ lựa chọn khi ổ cứng của bạn không có dữ liệu. Nếu máy tính của bạn đã cài đặt Ubuntu, bạn có thẻ chọn tùy chọn này để cài đặt mới Ubuntu.
		- Something else : Nếu máy tính của bạn chưa từng cài đặt Ubuntu, bạn cần phải _Check vào tùy chọn này_ để tạo phân vùng cài đặt Ubuntu.
- Vì cài trên Vmware nên mình sẽ chọn tùy chọn 1, nhấn Install now để tiếp tục.
![Imgur](https://imgur.com/sbagcsh.png)
- chọn continue để tự tạo phân vùng :
![Imgur](https://imgur.com/3DisNS2.png)
- chọn múi giờ :
![Imgur](https://imgur.com/uy1pffH.png)
- chọn ngôn ngữ bàn phím và tạo user-name.
- sau khi cài đặt thành công, nhấn restart để khởi động lại hệ điều hành :
![Imgur](https://imgur.com/3XpwweF.png)
- nhập password để đăng nhập :
![Imgur](https://imgur.com/44DJpZB.png)
- quá trình cài đặt Ubuntu trên VMware hoàn thành, bạn có thể thêm snapshot để quay về điểm này.
![Imgur](https://imgur.com/2JNUadg.png)

