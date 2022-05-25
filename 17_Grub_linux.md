# Grub là gì?
- GRUB (Grand Unified Bootloader): là một trương trình khởi động máy tính được phát triển bởi dự án GNU.
- GRUB cung cấp cho người dùng một lựa chọn cho phép khởi động một trong nhiều hệ điều hành được cài trên một máy tính hoặc lựa chọn một cấu hình hạt nhân cụ thể có sẵn trên các phân vùng của một hệ điều hành cụ thể.
- GNU GRUB được phát triển từ một gói phần mềm được gọi là Grand Unified Bootloader, nó được đặt làm trình khởi động mặc định cho Linux.
- Với tính năng chứng thực mật khẩu GRUB sẽ chỉ cho phép quản trị viên dùng các hoạt động tương tác GRUB, những người không có thẩm quyền sẽ không thể vào hệ thống qua chế độ Single User Mode để thay đổi mật khẩu `root` hay tinh chỉnh các giá trị của GRUB.
## Đặt mật khẩu cho GRUB
- Bước 1: Login với user `root`
- Bước 2: Tạo file backup `grup.cfg` và `10_linux`
```
# cp /boot/grub2/grub.cfg /boot/grun2/grub.cfg.orig
# cp /etc/grub.d/10_linux /etc/grub.d/10_linux.orig
```
- Bước 3: Chỉnh sửa file `10_Linux`
` vi /etc/grun.d/10_linux`
- Thêm vào cuối file nội dung sau: 
```
cat << EOF
set superusers="admin"
password admin P@ssw0rd
EOF
```
![](https://imgur.com/bh1n73Q.png)
- Bước 4: Tạo lại file `grun.conf` từ những cấu hình đã chỉnh sử:
`# grub2-mkconfig --output=/boot/grub2/grub.cfg`
- Bước 5: Khởi động lại hệ thống và kiểm tra
- Tại màn hình reboot nhấn `e` để chỉnh sửa `GRUB_MENU`. Nếu yêu cầu nhập lại user và password vừa tạo