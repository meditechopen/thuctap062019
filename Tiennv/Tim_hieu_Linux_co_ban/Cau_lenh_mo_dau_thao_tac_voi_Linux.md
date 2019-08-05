## Câu lẹnh mở đầu thao tác với Linux

#### Trong Linux, có rất nhiều câu lệnh (command) để người dùng có thể tương tác, sau đây là một số lệnh cơ bản khi mới bắt đầu sử dụng Linux để bắt đầu làm quen.

- `su` [user]: chuyển sang người dùng khác

- `sudo -i` hoặc `su`: đăng nhập với tư cách người dùng root. Nếu bạn gõ `sudo -i` thì bạn sẽ phải nhập mật khẩu của người dùng hiện tại, còn nếu bạn gõ `su` thì bạn sẽ phải nhập mật khẩu của user root.

- `exit` hoặc `logout`: thoát khỏi người dùng hiện tại

- `passwd`: đổi mật khẩu cho user

- `useradd` và `userdel`: tạo và xóa 1 người dùng khỏi hệ thống

- `groupadd` và `groupdel`: tạo và xóa 1 nhóm người dùng khỏi hệ thống

- `reboot`: khởi động lại hệ thống

- `shutdown` và `poweroff`: tắt hệ thống (trong một số trường hợp, đôi khi hệ thống yêu cầu bạn phải cần quyền root mới có thể tắt máy hoặc khởi động lại được, bạn chỉ cần ghi câu lệnh kèm với `sudo` ở trước)

- `init 0` và `init 6`: 2 câu lệnh đùng để tắt và khởi động lại hệ thống. Lệnh `init` được dùng để chuyển đổi chế độ môi trường (runlevel) khác nhau trên Linux như single-mode, X-Desktop, tắt, khởi động lại. Cần lưu ý khi sử dụng lệnh `init` vì có thể nhầm lẫn giữa option tắt hoàn toàn (0) và khởi động lại (6).
