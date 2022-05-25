> # Kiến trúc hệ điều hành Linux
- Gồm 3 phần : Kernel, Shell, Application
![](https://imgur.com/L5isyH8.png)
## Kernel (nhân)
![](https://imgur.com/q7yCnvh.png)
- Đây là trái tim của hệ điều hành, chứa các module, thư viện để quản lý và giao tiếp với phần cứng đảm bảo hầu hết các hoạt động của hệ thống.
- Phần Kernel chứa các trương trình quản lý bộ nhớ, CPU, quản lý file và các trình điều khiển thiết bị.
- Trong phần lớn các hệ thống, kernel là trương trình đầu tiên được nạp vào trong quá trình khởi động máy tính. 
- Kernel xử lý các yêu cầu vào/ra từ phần mềm, chuyển chúng thành hướng dẫn xử lý dữ liệu cho cpu.
- Các nhân khác nhau thực hiện các tác vụ của hệ điều hành khác nhau, tuỳ vào thiết kế cài đặt. 
  - Nhân nguyên khối (Monolithic kernel): thực hiện các nhiệm vụ của mình bằng cách thực thi toàn bộ mã hệ điều hành trong cùng một địa chỉ bộ nhớ
  - Nhân loại nhỏ (Microkernel): chạy hầu hết các dịch vụ tại không gian người dùng với mục đích tăng khả năng bảo trì và tính modul của hệ điều hành. 
  - Hybrid Kernel : là nhân có khả năng chọn lựa và quyết định những ứng dụng nào được phép chạy trong chế độ user hoặc supervisor.
- Kiểm tra phiên bản kernel trong linux
```
# uname -r
3.10.0-957.5.1.e17.x86_64
```
  - `3` là phiên bản kernel.
  - `10` là phiên bản sửa đổi chính hiện tại
  - `0` đề cập tới phiên bản sửa đổi phụ hiện tại
  - `957.5.1` đề cập đến bản vá cuối cùng được cập nhật cho phiên bản này
  - `e17` có nghĩa kernel này dành cho tất cả các phiên bản RHEL/CentOS 7
- Kiểm tra các phiên bản kernel đã cài đặt trên CentOS
```
# rpm -q kernel
  kernel-3.10.0-957.e17.x86_64
  kernel-3.10.0-957.5.1.e17.x86_64
```
- Xoá các bản kernel cũ hơn không dùng đến:
` yum remove kernel-3.10.0-957.e17.x86_64`
## Shell
- Là một trương trình thực thi các command từ người dùng hoặc từ các ứng dụng - tiện ích yêu cầu chuyển đến cho Kernel xử lý.
- Shell  phân tích cú pháp -> thông dịch yêu cầu của lệnh -> truyền thông điệp tới kernel -> nhận kết quả trả về từ kernel và hiển thị ra màn hình kết quả của lệnh.
- Bảo vệ Kernel từ các yêu cầu không hợp lệ.
- Các loại shell thông dụng:
  - **sh (the Bourne Shell)**: đây là shell nguyên thuỷ của Unix được viết bởi Stephen Bourne vào năm `1974 `và đến nay vẫn được sử dụng rộng rãi.
  - **Bash shell (Bourne-again Shell)**: là shell mặc định trên Linux được viết với Brian Fox và Chet Ramey cho dự án GNU. Bash được cải tiến từ sh, nó hỗ trợ nhiều cầu lệnh hơn.
  - **csh (the C shell**): shell được viết bằng ngôn ngữ lập trình C, được viết bởi Bill Joy-tác giả của trình soạn thảo văn bản vi nổi tiếng.
- Dấu nhắc shell : là một ký tự hoặc 1 tập ký tự luôn đứng tại điểm bắt đầu của bất kỳ dòng lệnh nào, nó ám chỉ rằng shell đã sẵn sàng nhận lệnh từ người dùng.
  - `$` dùng với người dùng thông thường 
  - `#` dùng cho user root
```
[root@localhost ~]#
[username@localhost root]$
```
## Applications
- Là các ứng dụng và tiện ích mà người dùng cài đặt trên Linux.
VD: ftp, samba, proxy,...

