# Tìm hiểu và sử dụng Github
## Tổng quan
**GitHub** là một dịch vụ cung cấp kho lưu trữ mã nguồn Git dựa trên nền web cho các dự án phát triển phần mềm. GitHub cung cấp cả phiên bản trả tiền lẫn miễn phí cho các tài khoản. Các dự án mã nguồn mở sẽ được cung cấp kho lưu trữ miễn phí. Với sysadmin, git và github được sử dụng để lưu trữ các file cấu hình, các script, viết các bài hướng dẫn, các bản nháp,...
## Các khái niệm, thuật ngữ cơ bản trên Github :
- **Repository** : là nơi lưu trữ mã nguồn của bạn mà người khác có thể sao chép (clone) lại mã nguồn đó nhằm làm việc. Repository có hai loại là _Local Repository_ (Kho chứa trên máy cá nhân) và Remote _Repository_ (Kho chứa trên một máy chủ từ xa).
		- repository private : là kho chứa cá nhân của bạn, nơi chỉ bạn nhìn thấy được tài liệu của mình.
		- repository public : là nơi mà tài liệu của bạn được đẩy lên và tất cả mọi người đều có thể thấy và sao chép lại.
- **Fork** : Một fork là một bản copy của một repository (Kho chứa source code của bạn trên [Github](https://github.com)). Việc fork một repository cho phép bạn dễ dàng chỉnh sửa, thay đổi source code mà không ảnh hưởng tới source gốc.
	- sử dụng fork : khi bạn muốn fix bug source code hay chỉnh sửa tài liệu trên repo của một ai đó, bạn cần làm theo các bước sau :
			- Fork repo đó về tài khoản Github của mình
			- thực hiện fix bug
			- gửi PR tới repo gốc
Khi chủ sở hữu của repo đó thấy PR, sẽ review chỉnh sửa của bạn và tiến hành merge nội dung chỉnh sửa vào source, tài liệu gốc.
- **Commit** : Trên mỗi branch bạn làm việc, sau khi sửa đổi các file source code... Những thay đổi đấy cần được lưu lại bằng cách tạo ra một điểm mốc đánh dấu. Điểm đánh dấu các thay đổi này gọi là Commit. Tại mỗi commit, git chụp lại toàn bộ dữ liệu, tạo ra một snapshot version hóa dữ liệu.
Mỗi commit được tạo ra gồm một số thông tin chính:

	-   Tên và email của ngưởi tạo commit
	-   Ngày giờ commit được tạo ra
	-   Message: Mô tả cho sự các sửa đổi (Để sau này xem lại còn biết nó sửa vì mục đích gì)
	-   Một ID là một chuỗi SHA gồm 2 dạng: Full và Short.
    -   Full: Chuỗi SHA đầy đủ
    -   Short: Là 7 ký tự đầu tiên được cắt ra từ chuỗi Full
 - **Branch và Merge** : chia nhánh và gộp nhánh của Repository
	- Các nhánh sẽ độc lập với nhau và phát triển một tính năng, không gây ảnh hưởng đến các nhánh khác. Khi các nhánh hợp nhất lại với nhau thì gọi là **merge**, nhánh mặc định sẽ là `master`. Branch ở trên local repo thì gọi là `local branch`, Branch ở trên remote repo thì gọi là `remote branch`. Một Branch trên local có thể liên kết với 1 hoặc nhiều branch trên remote hoặc không branch nào cả.
	- Git cho phép và khuyến khích bạn tạo nhiều branch tại máy tính cá nhân của bạn, việc tạo, sáp nhập và xóa bỏ những branch này diễn ra rất nhanh chóng.
	- Thông thường thì branch master chứa phiên bản code chạy tốt nhất để deploy lên production, branch dev để bạn có thể kiểm thử lại chức năng và một vài branch nhỏ để xây dựng các tính năng mới.
	- Sau khi viết code để thực hiện chức năng mới ở branch nhỏ xong, bạn hợp nhất (**merge**) code vào branch dev, kiểm tra lại, nếu ok thì tiếp tục **merge** code từ dev vào master.
	- Việc chuyển đổi trạng thái code từ branch này sang branch khác hoàn toàn dễ dàng, nếu như chức năng mới của bạn bị lỗi, bạn hoàn toàn có thể xóa branch đó đi mà chẳng gây ảnh hưởng gì đến những chức năng khác.
 - **Remote** : Để đẩy code lên server repository, chúng ta cần các tham chiếu tới server repository tương ứng. Các tham chiếu này được gọi là  `Remote`. Mỗi remote sẽ có các thông tin:
	-   Tên remote
	-   URL: đường link tới repository (Có hai dạng tương ứng cho 2 giao thức http và ssh).
- **Git Pull Request** : 
	- Định nghĩa : Pull Request dùng để bạn thông báo với người khác về các thay đổi bạn đã đẩy lên kho Github (Github repo). Một khi pull request được gửi, người nào quan tâm có thể review lại các thay đổi, hoặc thảo luận các sửa đổi tiềm năng và có thể theo đó đẩy tiếp các commit của họ nếu cần thiết.
	- Có 2 cách chính để làm việc với pull request là PR từ forked repo hoặc PR từ nhánh bên trong repo.
### Tìm hiểu, làm việc, các thao tác cơ bản với Git
- **git init** : khởi tạo một Repo mới
- **git status** : hiển thị thông tin trạng thái của Repo, **git status -s** hiển thị thông tin ngắn gọn hơn
- **git add** : cập nhật nội dung thay đổi của các file, file mới ... vào index, đưa chúng vào **staged** để chuẩn bị cho việc commit tiếp theo, một số cách sử dụng tham số với lệnh này như : 
		- **git add filename** : thêm file có tên chỉ ra trong tham số
		- **git add *.c** : thêm tất cả các file có phần mở rộng .c
		- **git add -A** : thêm mọi thứ có sự thay đổi (file mới, xóa file, nội dung thay đổi,...)
		- **git add .** : thêm mọi thứ trừ loại xóa file
		- **git add -u** : thêm mọi thứ trừ file mới
- **git commit**
		- **git commit -m "Thông báo ..."** : thực hiện commit, lưu snapshot vào DB Git
		- **git commit --amend -m "..."** : commit, nhưng cập nhật thông tin vào commit cuối
- **git clone path** : sao chép một Repo có địa chỉ là path ( có thể là địa chỉ mạng như http://github.com/... hoặc SSH git@github.com:... , có thể là ở chính máy của bạn như C:\Path\...)
- **git log** : xem lại lịch sử commit. Nếu muốn hiển thị thông tin **n** commit cuối thôi thì thêm tham số **-n** vào **git log -n**, nếu muốn hiển thị thông tin gì thay đổi trong từng commit thì thêm tham số **-p**, **git log --pretty=oneline** hiển thị thông tin mỗi commit trên một dòng
- **git diff** : xem nội dung thay đổi giữa thư mục làm việc và Staged nếu có, hoặc giữa thư mục làm việc với commit cuối. **git diff --staged** xem sư thay đổi của nội dung trong staged và commit cuối.
- **git rm filename** : xóa file khỏi thư mục làm việc.
- **git reset HEAD filename** : hủy bỏ việc thay đổi trạng thái file, ví dụ hủy đưa vào Staged
- **git checkout --filename** : khôi phục thay đổi nội dung của filename, việc khôi phục ở trạng thái hiện tại có thể là khôi phục từ Staged nếu có, nếu không thì khôi phục từ commit cuối. Nếu muốn khôi phục file từ một commit cũ có mã hash thì làm như sau :
		- **git checkout [hash] filename** : khôi phục lại filename
		- **git checkout [hash] .** : khôi phục các file về phiên bản theo commit cũ
### Tìm hiểu quá trình trong Github :
- Đầu tiên file mà bạn đang làm việc sẽ được lưu ở workspace/working tree.
- Sau đó để có thể commit file thì bạn phải add nó vào Staging Area/Index, đây sẽ là khu vực lưu trữ những thay đổi của bạn trên tập tin để nó có thể commit, vì đối với git muốn commit tập tin nào thì tập tin ấy phải nằm trong Staging Area. Một tập tin khi nằm trong Staging Area thì sẽ có trạng thái là Staged.
- Sau đó ta thực hiện commit để đưa tập tin đã được thay đổi ấy lên Local branch.
- Nếu cảm thấy cần thay đổi tập tin thì ta sử dụng git checkout để đưa về working tree, nếu không ta dùng git push để đẩy tập tin lên remote repo.
- quá trình được thể hiện qua hình sau :
<img src="https://i.redd.it/nm1w0gnf2zh11.png">

### User name và Credential trong git :
- Git sử dụng username để giúp xác định ai là tác giả của một commit trong repo. Khi bạn thực hiên bất kì thao tác nào liên quan đến remote thì bắt buộc phải nhập thông tin đăng nhập. Nhưng nếu mỗi thao tác đều phải nhập username và passwd thì rất phiền, vì vậy chúng ta nên dùng `credential store` để lưu trữ mật khẩu trên disk, nghĩa là nó sẽ tự động đang nhập cho mỗi thao tác của bạn.
