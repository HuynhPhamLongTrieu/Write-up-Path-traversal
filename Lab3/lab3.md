[lab3.md](https://github.com/user-attachments/files/23211759/lab3.md)
Lab3: File path traversal, traversal sequences stripped non-recursively

Mô tả bài lab: Bài thực hành này chứa một lỗ hổng path traversal trong
việc hiển thị hình ảnh sản phẩm. Ứng dụng sẽ xóa các chuỗi path
traversal khỏi tên tệp do người dùng cung cấp trước khi sử dụng. Để giải
quyết bài thực hành, hãy truy xuất nội dung của tệp /etc/passwd.

Bước 1: Truy xuất ảnh trong bài lab  
![A group of darts on a table AI-generated content may be
incorrect.](image/image1.png){width="6.5in"
height="3.4590277777777776in"}

Bước 2: Bật chức năng Intercept trong Burpsuit để bắt request ảnh

![A screenshot of a computer AI-generated content may be
incorrect.](image/image2.png){width="6.5in"
height="2.5097222222222224in"}

Bước 3: Gửi gói tin đó đến repeater

![A screenshot of a computer AI-generated content may be
incorrect.](image/image3.png){width="6.5in"
height="5.372222222222222in"}

Bước 4: Thử thay đổi giá trị của tham số filename sang etc/passwd

![A screenshot of a computer AI-generated content may be
incorrect.](image/image4.png){width="6.5in"
height="3.477777777777778in"}

Ta thấy response trả về \"No such file\", có vẻ như file etc/passwd
không có trong thư mục hiện tại, ta thử lùi từng cấp thư mục một bằng
cách thêm ../ vào đường dẫn, ví dụ: ../etc/passwd là lùi 1 cấp  
  
![A screenshot of a computer AI-generated content may be
incorrect.](image/image5.png){width="6.5in"
height="3.4881944444444444in"}Sau khi lùi từ 1 thư mục đến 5 thư mục, ta
đều nhận được \"No such file\", có vẻ như vấn đề nhận được \"No such
file" không phải là do không có trong thư mục, suy đoán web đã xóa chuối
"../" ra khỏi giá trị của tham số filename  
  
Bước 5: Do suy luận ở bước 4 rằng web đã xóa chuỗi "../" ra khỏi giá trị
của tham số filename, ta thử đổi chuỗi "../" thành "....//", như vậy khi
xóa "../" thì chuỗi "....//" sẽ thành "../", ta cũng thực hiện việc lùi
từ 1 thư mục đến 5 thư mục  
![A screenshot of a computer AI-generated content may be
incorrect.](image/image6.png){width="6.5in"
height="3.4930555555555554in"}

Sau khi lùi đến thư mục thứ 3 thì ta đã có được nội dung của file
etc/passwd

![A screenshot of a computer screen AI-generated content may be
incorrect.](image/image7.png){width="6.5in"
height="3.467361111111111in"}
