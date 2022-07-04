# Các option trong câu lệnh firewall
- VD câu lệnh cài firewall khi cấu hình Apache:
```
# firewalld-cmd --zone=public --add-service=http
# firewalld-cmd --zone=public --add-service=http --permanent
# firewall-cmd --reload
```
- `zone`: là một nhóm các quy tắc nhằm chỉ ra những luồng dữ liệu được cho phép, trong đó có các quy tắc như:
  -  **drop**: ít tin cậy, toàn bộ kết nối đến sẽ bị từ chối mà không phản hồi, chỉ cho phép duy nhất kết nối đi ra
  -  **block**: tương tự như drop nhưng các kết nối đến bị từ chối và phản hồi bằng tin nhắn từ icmp-host-prohibited (hoặc icmp6-adm-prohibited)
  -  **public**: đại diện cho mạng công cộng, không đáng tin cậy. Các máy tính/services khác không được tin tưởng trong hệ thống nhưng vẫn cho phép các kết nối đến trên cơ sở chọn từng trường hợp cụ thể.
- Hiệu lực của các quy tắc 
- `runtime` (mặc định): có tác dụng ngay lập tức, mất hiệu lực khi reboot hệ thống.
- `permanent`: không áp dụng cho hệ thống đang chạy, cần reload mới có hiệu lực, tác dụng vĩnh viễn cả khi reboot hệ thống
- Câu lệnh reload firewall `firewall-cmd --reload`
# Cài đặt firewalld
- Firewall được cài mặc định trên Centos7. Nếu chưa có ta có thể tải nó xuống bằng câu lệnh `yum install firewalld`
- Khởi động firewalld `systemctl start firewalld`
- Kiểm tra tình trạng hoạt động `systemctl status firewalld`
- Thiết lập firewalld khởi động cùng hệ thống `systemctl enable firewalld`
- *Lưu ý: không nên cho phép Firewalld khởi động cùng hệ thống cũng như thiết lập Permanent, tránh bị khoá khỏi hệ thống cũng như thiết lập sai. Chỉ khi hoàn thành thiết lập tất cả các quy tắc tường lửa cũng như test cẩn thận mới cho phép khởi động lại cùng hệ thống.*
- Khởi động lại firewalld
```
systemctl restart firewalld
firewall-cmd --reload
```
- Dừng và vô hiệu hoá firewalld
```
systemctl stop firewalld
systemctl disable firewalld
```
# Thiết lập cấu hình firewalld
## Thiết lập các zone
- Liệt kê tất cả các zone trong hệ thống `firewall-cmd --get-zones`
- Kiểm tra zone mặc định `firewalld-cmd --get-default-zone`
- Kiểm tra zone active (được sử dụng bởi giao diện mạng) `firewalld-cmd --get-active-zones`
- Liệt kê các service/port được cho phép trong zone cụ thể
```
firewalld-cmd --zone=public --list-services
firewalld-cmd --zone=public --list-port
```
## Thiết lập các service
- Sử dụng `-add-service`: ví dụ 
```
firewall-cmd --zone=public --add-service=http
firewall-cmd --zone=public --add-service=http --permanent
```
## Vô hiệu hoá service
- Sử dụng `-remove-service`: ví dụ 
```
firewall-cmd --zone=public --remove-service=http
firewall-cmd --zone=public --remove-service=http --permanent
```
## Thiết lập cho port
- Mở port bằng các thêm tham số `-add-port`. Ví dụ
```
firewall-cmd --zone=public --add-port=9999/tcp
firewall-cmd --zone=public --add-port=9999/tcp -permanent
```
- Mở một dải port bằng
```
firewall-cmd --zone=public --add-port=4990-5000/tcp
firewall-cmd --zone=public --add-port=4990-5000/tcp --permanent
```
- Đóng port tương tự nhưng đổi `--add-port` thành `--remove-port`
- 
