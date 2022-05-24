> # Partition là gì?
-  **Partition** được hiểu là những phân vùng nhỏ (hay phân vùng logic) được chia ra từ một ổ cứng vật lý.
- Đây là cách chia và quản lý một ổ cứng đơn giản và hiệu quả 
  - Ví dụ: Trên một ổ cứng vật lý, ta phân ra một vùng quan trọng để chứa dữ liệu của hệ điều hành và 1 phân vùng để chứa phim, nhạc).
- Việc quản lý riêng biệt các phân vùng có nhiều ưu điểm như:
  - Dễ dàng cài đặt hệ điều hành
  - Sao lưu đơn giản hơn
  - Có thể cài đặt nhiều hệ điều hành trong cùng một ổ cứng (mỗi hệ điều hành cài ở một phân vùng riêng biệt)
- Dữ liệu trên 1 partition A sẽ được phân tách với dữ liệu trên partition B, mọi thao tác trên partition này sẽ không ảnh hưởng đến partition kia.
## Các loại partition
![](https://imgur.com/IEDXxj3.jpg)
- **Primary partition:** đây là những phân vùng có thể được dùng để boot hệ điều hành
- **Extended partition:** đây là vùng dữ liệu còn lại khi ta đã phân chia ra các primary partition, extended partition chứa các logical partition trong đó 1 ổ cứng chỉ có thể chứa 1 extended edition.
- **Logical partition:** các phân vùng nhỏ nằm trong extended partition, thường dùng để chứa dữ liệu.
## MBR và GPT
- Thông tin về các partition của ổ cứng sẽ được lưu trữ trên MBR (Master Boot Record) hoặc GPT (GUID Partition Table) tuỳ loại ổ cứng hỗ trợ. 
- Đây là hai loại chuẩn cấu hình và quản lý các partition trên ổ cứng
### MBR
- Hình dưới đây mô tả kiến trúc của một ổ đĩa MBR
![](https://imgur.com/eUMgS2a.png)
- MBR (Master Boot Record) là một khu vực khởi động đặc biệt nằm ở đầu một ổ đĩa. Khu vực này có một Boot Loader được cài đặt trên hệ điều hành và các thông tin về phân vùng Logical của ổ đĩa.
![](https://imgur.com/srPzXLp.png)
- Một ổ đĩa MBR hỗ trợ tối đa 4 phần vùng chính (Primary Partition). Ở đầu các phần vùng sẽ có các sector (với dung lượng bằng nhau 512 bytes). Toàn bộ thông tin về partition đều được lưu ở sector đầu tiên phân vùng. 
![](https://imgur.com/uqI7l09.png)
### GPT 
- GPT (GUID Partition Table) là chuẩn mới hơn MBR, hỗ trợ đến 128 phân vùng trên một ổ đĩa vật lý. Thông tin về các partition sẽ được ghi thành nhiều bản rải rác khắp ổ vật lý.
- Trên ổ đĩa MBR, dữ liệu của phần vùng và dữ liệu khởi động được lưu trữ ở một vị trí. Nếu dữ liệu này bị ghi đè hoặc hỏng, khi đó bạn sẽ phải gặp các rắc rồi. Ngược lại GPT lưu trữ nhiều bản sao của các dữ liệu này trên đĩa, do đó bạn có thể khôi phục các dữ liệu nếu dữ liệu này bị lỗi.
- GPT hỗ trợ cơ chế kiểm tra và chỉnh sửa dữ liệu dựa trên CRC (cyclic redundancy check). Nhờ 2 cơ chế này, chuẩn GPT làm giảm tỷ lệ mất mát dữ liệu. Ngoài ra, nếu ta cần khởi tạo một phần vùng với dung lượng lớn hơn 2TB, ta sẽ phải dùng GPT vì MBR không hỗ trợ dung lượng lớn hơn 2TB.
### Công cụ phân vùng ổ cứng
#### fdisk
- Chỉ để tạo phân vùng dưới 2TB
- Chỉ hỗ trợ ổ cứng chuẩn MBR
- Cấu trúc lệnh:
`fdisk [options][/dev/...]
  - Options: `l`: liệt kê tất cả các ổ cứng và các partition
  - Command sử dụng trong lệnh:
    - `n`: tạo mới 1 partition
    - `p`: hiển thị **partition table**
    - `q`: thoát mà không lưu thay đổi
    - `w`: lưu thay đổi và thoát
    - `d`: xoá 1 partition
#### gdisk
- Hỗ trợ ổ cứng chuẩn **GPT**
- Cấu trúc câu lệnh
`gdisk [option] [/dev/...]`
- Options:
  - `-l`: liệt kê các ổ cứng và phân vùng chuẩn GPT
  - `-g`: chuyển ổ cứng từ **MBR** sang **GPT**
  - `-m`: chuyển ổ cứng từ **GPT** sang **MBR**
- Command: tương đương lệnh `fdisk`
#### parted
- Tên đầy đủ là **GNU Parted 3.x**
- Hoạt động với tất cả các chuẩn ổ cứng như **MBR**, **GPT**,...
- Hỗ trợ nhiều tính năng hơn `fdisk` và cũng dễ sử dụng hơn.
- Cấu trúc lệnh:
` parted [options][/dev/...] 
  - Options:
    - `-l`: liệt kê các ổ cứng và phân vùng
    - `-v`: hiển thị version của **GNU Parted**
  - Command:
    - `mkpart [type] [start] [end]`: tạo 1 phân vùng mới
      - Type: "btrfs", "ext3", "ext4", "fat16", "fat32", "hfs", "linux-swap", "ntfs", "reiserfs", "xfs" + "primary", "logical", "extended"
      - Start, End: mặc định là đơn vị MB
    - `mklabel [label type]`: tạo nhãn cho ổ cứng
      - Label Type: "gpt", "msdos", "loop", "sun", "mac"
    - `name [partition name]`: đặt tên cho phân vùng
      - Chỉ hoạt động trên ổ cứng chuẩn GPT, MAC, PC98
    - `printf`: in ra partition table của ổ cứng
    - `quit`: thoát khỏi `parted`
    - `resizepart [partition] [end]: thay đổi kích cỡ partition
    - rm [partition] [flag] [state]: gắn cờ
      - Flag: "boot", "root", "swap", "hidden", "raid", "lvm", "lba", "legacy-boot", "palo"
      - State: on/off
    - `unit [unit]`: chọn đơn vị khi hiển thị trong `parted `
      - Unit: "s" (sector), "B" (Bytes), "kB", "MB", "MiB", "GB", "TB", "TiB", "%" (phần trăm ổ đĩa), "cyl" (cylinders) 