# Shell là gì?
- Máy tính là một thiết bị các dữ liệu dưới dạng các bit nhị phân. Trong khi đó con người lại giao tiếp với máy tính thông qua giao diện đồ hoạ hoặc dòng lệnh. Vì vậy, một chương trình `shell` được sinh ra đóng vai trò ở giữa giúp biên dịch các thao tác, các dòng lệnh của người dùng sang ngôn ngữ máy tính. 
- Một hệ điều hành có nhiều loại shell khác nhau, trong đó có **bash shell**, là một shell mặc định được sử dụng trên linux.
- Thuật ngữ `shell script` là một chuỗi các lệnh được viết trong file text. Và shell sẽ thực thi file text này thay vì nhập vào các lệnh.
## Tạo shell scripts
- Bước 1: Tạo một file
- Bước 2: Dùng trình soạn thảo trên máy để mở file và viết các câu lệnh cần thực hiện trong 1 file có thể bao gồm các phép toán. 
  - Chú ý là dòng đầu tiên của file cần khai báo shell cụ thể sử dụng trong chương trình. Thường sẽ là `#!/bin/sh` hoặc `#!/bin/bash`.
  - Sau đó dùng lệnh `chmod` để cấp quyền thực thi cho file vừa tạo
  - Để chạy file đó ta có 3 cách sau
    - `./ten_file`
    - `bash ten-file`
    - `sh ten_file`  
## Khai báo biến trong bash shell
- Biến được gán trực tiếp. Giá trị của biến có thể là số hoặc một chuỗi. 
- `ten_bien=gia_tri`
- Chú ý, giữa tên biến dấu `=` và giá trị không được có dấu cách. Nếu giá trị là một chuỗi gồm nhiều từ thì cần đặt trong dấu `""`. 
- Để gọi giá trị biến đã gán, ta sử dụng ký tự `$` phía trước tên biến.
- Có thể sử dụng 1 trong 2 cách `$ten_bien` hoặc `${ten_bien}`.
- Một số biến mà ta không cần gán giá trị trực tiếp cho nó. Ta chỉ cần gọi nó ra còn giá trị của nó tuỳ thuộc vào lúc ta chạy chương trình. VD `./ten_file chuỗi`. Các biến đặc biệt là :
  - `$#` sẽ trả về tổng số từ của chuỗi
  - `$0` trả về tên file
  - `$1` trả về từ đầu tiên của chuỗi
  - `$2` trả về từ thứ 2 của chuỗi
  - `$9` trả về từ thứ 9 của chuỗi
  - `$@` trả về một chuỗi đầu đủ
- Ví dụ một file `test` có nội dung như sau:
```
#!/bin/sh
echo "Giá trị với $# chuoi"
echo "Đây là $0"
echo "Đây là $1"
echo "Đây là $2"
echo "Đây là tất cả ký tự $@"
```
- Chạy file có kết quả như sau
