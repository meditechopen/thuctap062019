# Tìm hiểu và sử dụng Markdown
### Tổng quan ngôn ngữ Markdown :
 - **Markdown** là ngôn ngữ đánh dấu văn bản được tạo ra bởi John Gruber. Markdown là một dạng ngôn ngữ đánh dấu văn bản gọn nhẹ được thiết kế nhằm định dạng theo cú pháp các đoạn plain text sao cho chúng có thể được chuyển đổi dễ dàng qua lại với HTML hoặc một vài dạng khác. Markdown thường được sử dụng trong các file readme.me (file dùng để mô tả ngắn project hoặc sản phẩm) hoặc viết các tin nhắn trong các diễn đàn thảo luận và dùng để tạo ra các đoạn văn bản có cấu trúc phức tạp chỉ bằng một công cụ sử lí văn bản thô.
## Các cú pháp trong Markdown :
### Lập đề mục :
`# H1`
# H1
`## H2`
## H2
`### H3`
### H3
`#### H4`
#### H4
`##### H5`
##### H5
`###### H6`
###### H6
### Nhấn mạnh :
`Kiểu chữ nghiêng có thể dùng *dấu sao* hoặc _dấu gạch dưới_`
Kiểu chữ nghiêng có thể dùng *dấu sao* hoặc _dấu gạch dưới_
`Kiểu chữ đậm có thể dùng hai **dấu sao** hoặc hai __dấu gạch dưới__`
Kiểu chữ đậm có thể dùng hai **dấu sao** hoặc hai __dấu gạch dưới__
`Chúng ta cũng có thể trộn hai kiểu này bằng **dấu sao và _gạch dưới_**`
Chúng ta cũng có thể trộn hai kiểu này bằng **dấu sao và _gạch dưới_**
### Danh sách :
#### Danh sách dạng chỉ số :
 - Phần tử đầu tiên của danh sách
 - Phần tử thứ hai
 ... danh sách con
 - Phần tử thứ 3
#### Danh sách có thể dùng dạng kí tự :
```
	* Dấu sao
* Dấu sao
	- Dấu trừ
- Dấu trừ
	+ Hoặc dấu cộng
+ Hoặc dấu cộng
```

* Dấu sao
	* Dấu sao
- Dấu trừ
	- Dấu trừ
+ Hoặc dấu cộng
	+ Hoặc dấu cộng
### Liên kết :
`[Liên kết ngay cùng dòng](https://google.com)`
[Liên kết ngay cùng dòng](https://google.com)
`Các URL cũng được tự động sinh ra
http://www.example.com or <http://www.example.com>`
Các URL cũng được tự động sinh ra
http://www.example.com or <http://www.example.com>
### Hình ảnh :
```
Chỉ vào hình ảnh để xem tiêu đề.

Viết trên cùng dòng:
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
```
Chỉ vào hình ảnh để xem tiêu đề.

Viết trên cùng dòng:
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
```
Viết theo cách tham chiếu: 
![alt text][logo] 

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"
```
Viết theo cách tham chiếu: 
![alt text][logo] 

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"

### Code và làm nổi bật cú pháp :
```
Nếu code chỉ trong một dòng bạn có thể dùng `dấu huyền`
```
Nếu code chỉ trong một dòng bạn có thể dùng `dấu huyền`
```
``` Nếu code trên nhiều dòng: 
var s = "JavaScript syntax highlighting"; 
alert(s); ```
```
### Trích dẫn :
`>Trích dẫn trên 1 dòng`
>Trích dẫn trên 1 dòng

`>>Trích dẫn trên dòng thứ 2`
>>Trích dẫn trên dòng thứ 2


