# Các bước thay đổi mật khẩu của Centos 7
- Bước 1: Khởi động lại Server, sau đó bấm phím bất kỳ để màn hình ở lại trình khởi động Grub, gõ `e` và tìm tới dòng `ro`
![](https://imgur.com/KWR43Qp.png)
- Thay thế `ro` bằng `rw init=/sysroot/bin/sh` 
![](https://imgur.com/ZsixHR1.png)
- sau đó nhấn Ctrl + X để vào chế độ Single Mode
- Truy cập hệ thống gốc bằng lệnh `chroot /sysroot`
![](https://imgur.com/dlV7hRZ.png)
- Tạo mật khẩu mới cho user bằng cầu lệnh `passwd`
- Update thông tin vào SElinux và thoát khỏi chế độ chroot:
```
# touch /.autorelabel
# exti
```
- Reboot lại hệ thống và đăng nhập với mật khẩu mới