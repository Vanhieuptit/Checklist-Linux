> # Mount filesystem trong Linux
- Khi ổ đĩa được phân vùng, Linux cần một số cách để truy cập dữ liệu trên các phân vùng. Không giống như Windows (thực hiện bằng cách gán các ký tự ổ đĩa cho mỗi phân vùng), Linux sử dụng một cây thư mục (folder tree) thống nhất: trong đó mỗi phân vùng được gắn kết tại một điểm gắn kết(mount point) trên cây đó.
## Mount Devices
#### File /etc/fstab
- fstab (file system table) là một bảng lưu trữ thông tin các thiết bị, mount point và các thiết lập của nó. Tức là kiểm soát các **filesystem** nào được mount.
- Các thông tin trong `/etc/fstab` :
  - Đường dẫn tới file đại diện cho thiết bị
  - Mount point: thiết bị được mount vào thư mục nào
  - Các tuỳ chọn : chỉ ra thiệt bị được mount như thế nào 
- file `fstab` này được lưu trữ dưới dạng `plain text` nên có thể chỉnh sửa dễ dàng bằng câu lệnh `cat`  và `vi`.
- Cấu trúc file `fstab` có dạng
![](https://imgur.com/0Orq4aQ.png)
- Cột 1: Lưu tên thiết bị (UUID) hoặc đường dẫn tới file thiết bị trong thư mục `/dev`
  - Để biết UUID của phân vùng hoặc thiết bị, sử dụng câu lệnh `blkid`
- Cột 2: Cho biết **mount point** (thiết bị được mount đến thư mục nào)
- Cột 3: Định dạng file system của thiết bị. Thông thường là `ext3`, `ext4`, `reiserfs`, `swap`, `ISO 9660`, `vfat`, `ntfs`, `nfs`, `xfs`, `auto`,...
- Cột 4: Chứa các tuỳ chọn
  - **auto**: tự động mount thiết bị khi khởi động lại
  - **noauto**: phải chạy lại lệnh mount khi khởi động hệ thống.
  - **user**: cho phép người dùng thông thường được quyền mount
  -   **nouser**: chỉ user `root` mới được quyền mount.
  -   **exec**: cho phép chạy các lệnh nhị phân trên thiết bị
  -   **noexec**: không cho phép chạy lệnh nhị phân trên thiết bị
  -   **ro**: (read-only): chỉ cho phép quyền đọc trên thiết bị
  -   **rw**: (read-write): cho phép quyền đọc/ghi trên thiết bị
  -   **sync**: thao tác nhập xuất (I/O) trên file system diễn ra không đồng bộ.
  -   **defauls**: tương đương các tập tuỳ chọn ở trên.
- Cột 5: là tuỳ chọn chương trình sao lưu file system
  - nếu là `0` : bỏ qua việc sao lưu
  - nếu là `1`: thực hiện sao lưu
- Cột 6: là tuỳ chọn cho chương trình `fsck` dò lỗi file system:
  - nếu là `0`: bỏ qua việc kiểm tra
  - nếu là `1`: thực hiện việc kiểm tra
![](https://imgur.com/BdqghJ4.png)
#### UUID
- Trước đây, trường thiết bị của fstab đơn giản chỉ là các các tên như `/dev/sd3` cho phân vùng thứ 3 trên ổ cứng thứ nhất. Tuy nhiên, khi các ổ đĩa thường xuyên **add** và **remove** dẫn tới thứ tự sẽ thay đổi liên tục, `sdb3` có thể thành `sda3`
- UUID sinh ra để giải quyết vấn đề này.
### Tên thiết bị trong Linux
- **cdrom**: đĩa CDROM/DVD
- **hd***: ổ đĩa IDE, ATA
  - **hda**: ổ cứng thứ nhất
  - **hdb**: ổ cứng thứ hai
    - **hdb1**: phân vùng thứ nhất của ổ cứng thứ hai
- **sd***: ổ đĩa SCSI, SATA (SSD, HDD), USB
  - **sda**: ổ cứng thứ nhất
  - **sdb**: ổ cứng thứ 2
    - **sdb1**: phân vùng thứ nhất của ổ cứng thứ hai
- **nvme0***: ổ cứng SSD NVMe
  - nvme0n1: ổ nvme thứ nhất
  - nvme0n2: ổ nvme thứ hai
- **tty***: cổng giao tiếp (COM,...)
- **eth***: cổng Ethernet
## Lệnh mount thiết bị trong linux
- `mount [option] [device_name] [mount_point]`
- Trong đó các [Option]:
  - `-v`: chế độ chi tiết, cung cấp thêm thông tin về những gì mount định thực hiện
  - `-w`: mount hệ thống tập tin với quyền đọc và ghi
  - `-r`: mount hệ thống tập tin chỉ có quyền đọc
  - `-t`: xác định lại hệ thống tập tin được mount. Những loại hợp lệ là `ext2`, `ext3`, `ext4`, `vfat`, `iso 9600`,...
  - `-a`: mount tất cả các hệ thống tập tin được khai báo trong `fstab`
  - `o`: remount (fs) chỉ định việc mount lại file system nào đó
## Mount bằng Udisks
- Udisks là một phần quan trọng của phần mềm được sử dụng trong nhiều bản phân phối Linux.
- Nó có trách nhiệm quản lý các thiết bị lưu trữ như bộ nhớ flash USB và ổ cứng. Với nó đi kèm một công cụ dòng lệnh gọi là `udisksctl` 
- Cú pháp: udisksctl [lệnh]
- Vd: `udiskctl mount -b /dev/sd[b1,b2,...]`
- Tham số `-b` đơn giản biểu thị rằng những gì bạn đang mount từ một thiết bị
## Mount kiểu truyền thống
- Câu lệnh `mount /dev/sd[b1,b2,...] /mnt`
- `mnt` ở đây là thư mục để ta mount vào
- Câu lệnh Unmount `unmount /dev/sd[b1,b2,...]`
