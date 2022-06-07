- SSH là giao thức điều khiển từ xa cho phép người dùng truy cập và thao tác trên serve ở xa thông qua Internet.
- Dữ liệu trao đổi giữa 2 máy sẽ được mã hoá một cách an toàn.
## Yêu cầu để có thể SSH
- 1 máy ảo cài hệ điều hành Centos 7
- 1 máy windows có cài phần mềm mobaxterm
Trước tiên, ta cần ssh vào máy chủ bằng mobaxterm với địa chỉ ip máy chủ, port SSH là 22
- Cú pháp: `ssh user@diachi`
 - `user`: là tên của user ta muốn kết nối vào.
 - `diachi`: là địa chỉ của máy ta muốn ssh, có thể là địa chỉ IP hoặc Domain name.
## Xác thực trong SSH
### Cách 1: Xác thực bằng password
- Là một cách xác thức đơn giản: ssh sẽ yêu cầu ta nhập mật khẩu của user mà ta muốn truy cập vào
 - Ưu điểm: là đơn giản và không phải cấu hình trước bất kỳ điều gì.
 - Nhược điểm: bảo mật yếu
### Cách 2: Xác thực bằng key
- Sử dụng 1 cặp key để xác thực (private key và public key)
- **Public key** là một mã công khai, được đặt ở nơi mà ta muốn kết nối vào ( trên user root, client của máy ở xa hoặc github)
- **Private key** là một mã bí mật ta phải cất giữ trên máy của mình.
## Tạo key và cấu hình SSH bằng key cho máy chủ
- Sau khi đã SSH bằng mật khẩu thành công lên máy chủ, ta thực hiện câu lệnh `ssh -keygen -t rsa`. Đây là câu lệnh tạo key đơn giản và dễ thực hiện nhất. Ngoài ra còn có các option khác tuỳ theo mục đích của mình
```
ssh -keygen [option]
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
- Bước 3: Cấp quyền cho thư mục bằng câu lệnh `chmod 700 .ssh`
  - Trong thư mục `.ssh` tạo file `authorized_keys` chứa key publich bằng câu lệnh `mv id_rsa.pub authorized_key` và dùng lệnh `chmod 600 authorized_keys` để phần quyền cho file đó
- **Lưu ý**: để sử dụng SSH key ta cần phải tắt `SElinux` bằng cách vào file `/etc/selinux/config` sửa dòng `SELINUX=enforcing` thành `SELINUX=disabled` sau đó reboot lại server.
- Bước 4: Lưu key đã tạo về máy client mà ta sử dụng để SSH bằng cách 
![](https://imgur.com/hkOuFUd.png)  
- Bước 5: Bật xác thực kết nối SSH bằng key bằng cách sửa cấu hình file `/etc/ssh/sshd_config`
![](https://imgur.com/UmfLfvg.png)
- Sửa thông số `PasswordAuthentication no` để không cho sử dụng SSH bằng xác thực mật khẩu. 
- Sửa dòng `AuthorizedKeyfile` bằng cách thềm `/root/` trước `.ssh/authorized_keys`
- Vì tài khoản root là user có đặc quyền cao nhất vì vậy ta sẽ phải ngăn không cho SSH truy cập vào tài khoản root bằng cách sửa file `/etc/ssh/sshd_config` sau đó bỏ dấu `#` ở dòng `#PermitRootLogin no`
- `UserPAM yes` thành `UserPAM no`.
`service sshd restart` để update lại thay đổi
- Bước 6: Giới hạn những user có thể login SSH vào hệ thống bằng cách vào file `/etc/ssh/sshd_config` tìm dòng `AllowUsers` và thêm vào những user mà bạn cho phép dùng SSH để login vào.
- VD:`#AllowUsers user1 user1`
## Sử dụng key để SSH bằng mobaxterm
- Sau khi đã thiết lập cấu hình hoàn tất trên máy chủ, ta kết thúc phiên SSH bằng mật khẩu.
- Lúc này, nếu ta SSH lại bằng cách thông thường sẽ bị server từ chối
![](https://imgur.com/FXNkvAQ.png)
- Lúc này ta phải sử dụng SSH bằng xác thực key trong mobaxterm như sau
![](https://imgur.com/Ox0PZIM.png)
- Key chính là file ta vừa lưu ở bước 4. Key này là private key
![](https://imgur.com/zvwQ2Fa.png)
 