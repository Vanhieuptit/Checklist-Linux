> # Set IP trên Centos 7
## Sửa file 
- Để đặt IP cho Centos 7 ta thực hiện sửa file cấu hình mạng trong thư mục `etc` bằng cách thực hiện câu lệnh  
```
vi /etc/sysconfig/network-scripts/[tên card mạng]
```
- Nếu chưa biết tên card mạng ta sử dụng câu lệnh
```
cd /etc/sysconfig/network-scripts
``` 
sau đó sử dụng lệnh 
```
ls
``` 
để lấy tên card mạng.
![](https://imgur.com/u7VM1bo.png)
- Sau khi đã vào được chế độ chỉnh sửa file cấu hình ta có ý nghĩa của các thông số sau
  - `DEVICE`: tên card mạng
  - `ONBOOT`: 
      - `yes`: khởi động khi `service network restart`
      - `no` không khởi động  
  - `BOOTPROTO`:
    - static: dùng IP tĩnh
    - dhcp: nhận IP từ DHCP Server
  - `IPADDR`: địa chỉ IP của card mạng (khi cấu hình IP tĩnh)
  - `NETMASK`: địa chỉ subnetmask (khi cấu hình IP tĩnh)
  - `GATEWAY`: địa chỉ gateway (khi cấu hình IP tĩnh)
  - `DNS1`: địa chỉ DNS Server (khi cấu hình IP tĩnh)
  - `USERCTL:
    - `yes`: cho phép user thường cấu hình sửa đổi
    - `no`: không cho phép user thường cấu hình sửa đổi
- Ví dụ thiết lập ip tĩnh cho server với các thông số: 
 ```
 Địa chỉ ip: 192.168.10.1/24
 Gateway: 192.168.10.2
 DNS1 8.8.8.8
 DNS2 8.8.8.1
 ```
![](https://imgur.com/3FH6MI2.png)
## Cấu hình bằng trương trình nmcli
- ***nmcli*** (NetworkManager Command Line Interface) là công cụ giúp điều khiển quản lý mạng bằng dòng lệnh thông qua NetworkManager.
- Với công cụ này, ta có thể tạo, hiển thị, chỉnh sửa, xoá, kích hoạt và huỷ kích hoạt các kết nối mạng, cũng như kiểm soát và hiển thị trạng thái thiết bị mạng.
### Các câu lệnh 
- Cấu trúc cơ bản của câu lệnh nmcli là 
```
nmcli Options Object {COMMAND | help}
```
- Các (OBJECT) bao gồm
  - general: làm việc với các hoạt động, trạng thái của NetworkManager.
  - networking: toàn bộ việc điều khiển mạng chung.
  - radio: quản lý phần vô tuyến.
  - connection: quản lý các kết nối.
  - decvice: làm việc với các thiết bị mà NetworkManager quản lý.
###Ví dụ các câu lệnh 
```
nmcli device
```
- Dùng để hiện thị các thiết bị mạng sẵn có
![](https://imgur.com/AeVgYYp)
```
nmcli -a
```
- Đưa ra các thông số tối thiểu về card mạng như MAC, MTU, IP,...
![](https://imgur.com/iAqKmxt.png)
```
nmcli -v
```
- Hiển thị phiên bản của trương trình `nmcli`
![](https://imgur.com/9mJoXms.png)
```
nmcli general status
```
- Hiển thị trạng thái chung của NetworkManager 
```
nmcli general logging
```
- Kiểm soát log của NetworkManager
```
nmcli connection show
```
- Hiển thị tất cả các kết nối
### Câu lệnh rút gọn trong nmcli
- Các câu lệnh có thể được rút ngắn lại bằng việc sử dụng các ký hiệu đầu của các tuỳ chọn, ví dụ
```
nmcli connection  add type ethernet
```
có thể được viết thành
```
nmcli c a type eth
```


