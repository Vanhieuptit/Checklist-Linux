- SSH là giao thức điều khiển từ xa cho phép người dùng truy cập và thao tác trên serve ở xa thông qua Internet.
- Dữ liệu trao đổi giữa 2 máy sẽ được mã hoá một cách an toàn.
- Cú pháp: `ssh user@diachi`
 - `user`: là tên của user ta muốn kết nối vào.
 - `diachi`: là địa chỉ của máy ta muốn ssh, có thể là địa chỉ IP hoặc Domain name.
## Xác thực trong SSH
### Cách 1: Xác thực bằng password
- Là một cách xác thức đơn giản: ssh sẽ yêu cầu ta nhập mật khẩu của user mà ta muốn truy cập vào
 - Ưu điểm: là đơn giản và không phải cấu hình trước bất kỳ điều gì.
 - Nhược điểm: bảo mật yếu
### Xác thực bằng key
- Sử dụng 1 cặp key để xác thực (pri key và pub key)
- Public key là một mã công khai, được đặt ở nơi mà ta muốn kết nối vào ( trên user root, client của máy ở xa hoặc github)
- Private key là một mã bí mật ta phải cất giữ trên máy của mình.
## Cấu hình key
```
ssh -keygen [option
```
- Options:
  - `-b`: sau đó là số bit để định số bit cho key
  - `-t`: để định thuật toán tạo key. Có các loại sau: rsa, dsa, ecdsa, ed25519. Nếu không có option này thì mặc định sẽ sử dụng `rsa`
  - `-f`: để chọn vị trí lưu file key
  - `-p`: để thay đổi passphrase. Cú pháp `ssh-keygen -p -P oldpass -N newpass -f keyfile`
  - `-y`: để tạo một public key từ 1 private key.
  - Một số option khác xem tại `ssh-keygen --help`
- Bước 2: Sau khi tạo key ta vao thư mục `.ssh` bằng câu lệnh `cd .ssh`
- Tìm 2 file là 
  - `id_rsa`: là file chứa private key
  - `id_rsa.pub`: là file chưa public key 
- Bước 3: Đưa public key lên Server ta muốn SSH bằng cách 
  - Đăng nhập vào server t muốn SSH rồi tạo thư mục `.ssh` 
  - `chmod 700 .ssh` để phân quyền cho thư mục
  - Trong thư mục `.ssh` tạo file `authorized_keys` vào dùng lệnh `chmod 600 authorized_keys` để phần quyền cho file đó
  - Ta copy nội dung file `id_rsa.pub` trên client vào file `authorized_key vừa tạo`
- **Lưu ý**: để sử dụng SSH key ta cần phải tắt `SElinux` bằng cách vào file `/etc/selinux/config` sửa dòng `SELINUX=enforcing` thành `SELINUX=disabled` sau đó reboot lại server.  
- Bước 4: Bật xác thực kết nối SSH bằng key bằng cách sửa cấu hình file `/etc/ssh/sshd_config`
![](https://imgur.com/lqJaH77.png)
- `service sshd restart` để update thay đổi.
- Thực hiện tiếp bước 4 nhưng sửa thông số `PasswordAuthentication no` để không cho sử dụng SSH bằng xác thực mật khẩu. 
- `service sshd restart` để update lại thay đổi.
- Bước 5: Vì tài khoản root là user có đặc quyền cao nhất vì vậy ta sẽ phải ngăn không cho SSH truy cập vào tài khoản root bằng cách sửa file `/etc/ssh/sshd_config` sau đó bỏ dấu `#` ở dòng `#PermitRootLogin no`
`service sshd restart` để update lại thay đổi
- Bước 6: Giới hạn những user có thể login SSH vào hệ thống bằng cách vào file `/etc/ssh/sshd_config` tìm dòng `AllowUsers` và thêm vào những user mà bạn cho phép dùng SSH để login vào.
- VD:`#AllowUsers user1 user1`

 