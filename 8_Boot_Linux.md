> # Linux boot process - quá trình boot Linux
- Là quá trình khởi tạo hệ thống Linux. Nó bao gồm các bước từ khi ta bật máy đến khi giao diện người dùng sẵn sàng.
![](https://imgur.com/5zqGJeU.png)
## BIOS POST
- BIOS - Basic Input/Output System : là một nhóm lệnh được lưu trữ trên một chip firmware nằm ở trên bo mạch chủ (mainboard) của máy vi tính. BIOS kiểm soát các tính năng cơ bản của máy vi tính như: Kết nối và chạy trình điều khiển (driver) cho các thiết bị ngoại vi (chuột, bàn phím, usb,...) đọc thứ tự ổ cứng để khởi động các hệ điều hành, hiển thị tín hiệu lên màn hình v.v...Sau đó, nó sẽ giao lại quyền cho bootloader.
- POST - Power On Self Test : là chức năng tự kiểm tra khi nguồn bật, đây là việc đầu tiên BIOS làm khi nó khởi động máy tính.
- POST được xây dựng sẵn là một chương trình máy tính để kiểm tra phần cứng, đảm bảo mọi thứ sẵn có và đảm bảo chức năng của mình, trước khi BIOS bắt đầu khởi động. Nếu POST gặp phải trục trặc, khi bật máy sẽ phát ra tiếng bíp và sau đó dừng không tiếp tục khởi động nữa.
- Các lỗi POST hầu như là không sửa được (tức là máy tính coi như hỏng)
- Nếu sau khi POST kiểm tra các thiết bị phần cứng không có vấn đề gì, BIOS sẽ tìm kiếm và khởi chạy một hệ điều hành được chứa trong các thiết bị lưu trữ ổ cứng hay đĩa CD...
- Hệ điều hành Linux được cài trên ổ cứng thì BIOS sẽ tìm đến MBR (Master Boot Record)
## Master Boot Record (MBR)
- Sau khi BIOS xác định được thiết bị lưu trữ thì BIOS sẽ đọc trong MBR hoặc phân vùng EFI của thiết bị này để nạp vào bộ nhớ một chương trình.
- Chương trình này sẽ định vị và khởi động boot loader
![](https://imgur.com/2XukUWE.png)
## Boot Loader
- Bootloader là chương trình chịu trách nhiệm cho việc tìm và nạp nhân hệ điều hành
- Trong linux có 2 boot loader phổ biến là Grub và Isolinux.
- Trương trình này có mục đích: cho phép lựa chọn hệ điều hành có trên máy tính để khởi động, sau đó chúng sẽ nạp kernel của hệ điều hành đó vào bộ nhớ và chuyển quyền điều khiển máy tính cho kernel này.
- Dưới đây là một file cấu hình grun.cfg `/boot/grub2/grub.cfg`
![](https://imgur.com/Z86VP9L.png)
- Hệ thống sử dụng phương pháp BIOS/MBR, đây là bộ tải khởi động nằm ở khu vực đầu tiên của đĩa cứng. Kích thước của MBR chỉ là 512 byte.
- Trong giai đoạn này, bộ nạp khởi động kiểm tra bảng phân vùng và tìm một phân vùng có khả năng khởi động, sau đó nó sẽ tìm kiếm bộ tải khởi động.
- Với hệ thống sử dụng phương pháp EFI/UEFI, phần mềm UEFI đọc dữ liệu trình quản lý khởi động để xác định ứng dụng UEFI nào sẽ được khởi chạy từ nơi nào.
- Trình khởi động giai đoạng 2 nằm trong /boot. Màn hình hiển thị cho chúng ta chọn hệ điều hành để khởi động. Tiếp đến bộ nạp khởi động sẽ tải hệ điều hành vào RAM và chuyển quyền kiểm soát cho RAM.
![](https://imgur.com/Bt3lBfy.png)
## Linux kernel được nạp và khởi chạy
- Boot loader nạp một phiên bản dạng nén của Linux kernel. Nó tự giải nén và tự cài đặt lên bộ nhớ hệ thống nơi mà nó sẽ ở đó cho tới khi tắt máy.
- Sau khi chọn kernel trong file cấu hình của boot loader, hệ thống sẽ tự động nạp chương trình init trong thư mục /sbin.
![](https://imgur.com/3PueQSN.png)\
## Trương trình Init (initialization)
- INITRD (intit Ram Disk): đây là mô hình để load root file system tạm thời vào bộ nhớ để có thẻ được sử dụng như là một phần của quá trình khởi động linux.
- Nó chứa một tập các chương trình sẽ được thực thi khi kernel vừa mới được khởi chạy. Các trương trình đó sẽ quét phần cứng của hệ thống và xác định xem kernel cần được hỗ trợ thêm những gì để có thể quản lý được các phần cứng đó.
- Trương trình Initrd có thể nạp thêm vào kernel các module bổ trợ. Khi chương trình Initrd kết thúc thì quá trình khởi động Linux sẽ tiếp diễn bằng cách thực hiện chương trình `initramfs`
- Initramfs (init random-access memory file system): là một tập hợp đầy đủ các thư mục mà bạn có thể tìm thấy trên hệ thống tệp gốc bình thường,..Nó được đóng gói thành một kho lưu trữ `cpio` duy nhất và được nén bằng một trong số các thuật toán nén.
- Tại thời điểm khởi động, bộ nạp khởi động tải kernel và image initramfs vào bộ nhớ và khởi động kernel.
- `initramfs` và `initrd` được lưu trữ tại `/boot` trong Centos 7
## Chương trình init thực thi
- Kernel được khởi chạy xong, nó sẽ gọi duy nhất một chương trình tên là `init`.
- Tiến trình này có ID = 1 là cha của tất cả các tiến trình khác mà có trên hệ thống Linux.
- Có các mức init được nằm trong file cấu hình `/etc/intitab`:
  - **runlevel 0**: shutdown hệ thống
  - **runlevel 1**: chỉ dùng cho 1 người dùng để sửa lỗi hệ thống tập tin.
  - **runlevel 2**: không sử dụng
  - **runlevel 3**: dùng cho nhiều người dùng nhưng chỉ giao tiếp dạng `text`.
  - **runlevel 4**: không sử dụng
  - **runlevel 5**: dùng cho nhiều người dùng và được cung cấp giao diện đồ hoạ
  - **runlevel 6**: reboot hệ thống
- Sau khi xác định run level. Chương trình  /sbin/init sẽ được thực thi các file starup script được đặt trong các thư mục con của thư mục /etc/rc.d
![](https://imgur.com/4iWOZNu.png)
- Trong file script theo từng level, các tên tập tin bắt đầu bằng từ khoá `S` tức là tập tin sẽ được thực thi lúc khởi động hệ thống
- Nếu tập tin bắt đầu bằng `K` có nghĩa là tập tin đó được thực thi khi hệ thống shutdown. 
### Systemd
- Đối với các bản Linux hiện đại như Centos 7, RHEL 7 gần đây thì init và runlevel được thay thế bởi systemd và cũng thực hiện nhiệm vụ tương tự.
- Systemd cũng giống như init là tiến trình chạy đầu tiên trên hệ thống với ID = 1.
- `systemd` đọc tệp liên kết bởi `/etc/system/system/default.target` để xác định đích hệ thống mặc định. 
- Tệp mục tiêu trong hệ thống xác định các dịch vụ mà systemd bắt đầu.
- `systemd` sẽ bắt đầu mọi thứ trong `/etc/systemd/system/basic.target` trước khi bắt đầu multi-user service.
- `systemd` sử dụng mục tiêu thay vì runlevel. Có hai mục tiêu chính : multi-user.target và graphical.target tương ứng với runlevel 3 và runlevel 5.
- Để xem các mục tiêu mặc định hiện tại chúng ta chạy lệnh :`systemctl get-default`
- Để đặt mục tiêu mặc định cho chúng ta chạy lệnh : `systemctl set-default TARGET.target`
- `systemctl` là ứng dụng kiểm soát các dịch vụ quản lý hệ thống.
## Đăng nhập với giao diện
- Đây là quá trình cuối cùng và cũng quen thuộc với người dùng nhất.