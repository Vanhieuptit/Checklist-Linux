# Thiết lập cấu hình card mạng
- Check tình trạng mạng
```
nmcli d
```
- Ban đầu khi chưa thiết lập sẽ như sau
![](https://imgur.com/VqD2zZj.png)
- Để thiết lập cấu hình tĩnh cho card mạng ta sử dụng câu lệnh:
  - `nmcli c modify ens33 ipv4.address 192.168.19.132/24 ipv4.gateway 192.168.19.2 `. Ở đây tôi sử dụng địa chỉ trong dải 192.168.19.0/24.
  - `nmcli c modify ens33 ipv4.method manual`. Khởi tạo card mạng dùng là ip tĩnh. Nếu sử dụng IP động thì sửa `manual` thành `auto`.
  - `nmcli c up ens33` để khởi động lại card mạng.
- Lúc này chạy lệnh `nmcli d` ta thấy trạng thái của card mạng đã hiện
1[](https://imgur.com/RZFr6oi.png)
- Kiểm tra bằng cách ping đến địa chỉ gateway 192.168.19.2. Nếu kết quả trả về ping thành công từ là đã "thông mạng"
- Lúc này, card mạng đã được cấu hình hoàn chỉnh, tuy nhiên nếu reboot lại hệ điều hành thì card mạng sẽ về trạng thái ban đầu. Vì vậy ta cần phải sửa file cấu hình bằng cách 
```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
- Tìm đến dòng `ONBOOT=no` sửa `no` thành `yes`. Sau đó khởi động lại mạng bằng câu lệnh 
```
systemctl restart network
```
# Cập nhật hệ điều hành
- Để cập nhật hệ điều hành ta phải đảm bảo kết nối tới internet và thực hiện lệnh sau với quyền root
```
yum -y update
```
- Lúc này sau khi cập nhật ta đã có một server với các gói cập nhật mới nhất.
# Thiết lập múi giờ
- Trước tiên, để xem các múi giờ có sẵn bằng câu lệnh 
```
timedatectl list-timezones
```
- Câu lệnh này sẽ cung cấp cho bạn danh sách các múi giờ có sẵn cho máy chủ của bạn.
- Sau khi đã có thông tin các múi giờ chính xác cho máy chủ của mình, ta tiến hành cài đặt nó bằng câu lệnh
```
timedatectl set-timezone Asia/Ho_Chi_Minh
```
- Hệ thống sẽ cập nhật để sử dụng đúng múi giờ đã chọn. Bạn có thể xác nhận điều này bằng cách nhập:
```
timedatectl
```
