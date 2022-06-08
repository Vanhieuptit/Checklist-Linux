> # Các lệnh Linux cơ bản
- Cấu trúc dòng lệnh shell có dạng tổng quát như sau:
`**command**  **[option]**  **arguments**`
- Trong đó:
  - command: tên lệnh
  - options: các tuỳ chọn, thường bắt đầu bằng `-` hoặc `--`
  - Nhiều tuỳ chọn có thể kết hợp bằng 1 kí hiệu `-`
  - Vd: `ls -l -a` <=> `ls -la`
  - arguments: tham số lệnh
> **Lưu ý**: dòng lệnh shell có phân biệt *chữ thường* và *chữ hoa*
# Một số mẹo giúp gõ câu lệnh dễ dàng hơn
- Dùng $\uparrow$ , $\downarrow$ để xem lại các lệnh vừa gõ
- `Ctrl` + `C` để huỷ lệnh
- `Ctrl` + `L` để làm mới màn hình terminal
- Dùng phím `Tab` để gõ nhanh tên file hoặc lệnh
- Dùng lệnh `history` để xem lại lịch sử gõ lệnh
- Gõ `![number]` với number là số thứ tự của câu lệnh trong mục `history` để xem lại nhanh câu lệnh
- `Ctrl`+`R` để tìm kiếm các lệnh đã gõ trước đó
> ## Lệnh man
- Dùng để xem hướng dẫn dùng 1 lệnh cụ thể trong Linux
`# man <tên lệnh>`
- Cấu trúc của một trang `man` như sau
```
NAME
tên lệnh - khái quát tác dụng của lênh
SYNOPSIS
cú pháp của lệnh
DESCRIPTION
mô tả cụ thể hơn về tác dụng của lệnh
OPTIONS
liệt kê cụ thể hơn về tác dụng của lệnh
FILES
liệt kê các tuỳ chọn lệnh và tác dụng của chúng
SEE ALSO
liệt kê các lệnh, các tài liệu,..., có liên quan đến lệnh 
REPORTING BUGS
địa chỉ liên hệ nếu gặp lỗi khi sử dụng lệnh
AUTHOR
tên tác giả của lệnh
```
![](https://imgur.com/Z6Dk7sy.png)
## pwd (print working directory)
- Cho phép biết thư mục hiện hành mà người dùng đang làm việc
## lsblk (list block devices)
- Dùng để liệt kê tên thiết bị, thông tin ổ đĩa và phân vùng trong Linux
- Thông thường, lệnh lsblk không cần bất kỳ tham số bổ sung nào cũng đủ để xác định ổ đĩa hoặc phân vùng bạn muốn làm việc. Tuy nhiên để tránh trường hợp nhầm lẫn tên thiết bị dẫn đến có thể phá huỷ hoặc làm hỏng dữ liệu ta cần thêm các tham số như
- `--help` : để xem những cột nào **lsblk** có thể hiển thị
  - VD: `lsblk --help` 
![](https://imgur.com/PzR2OBy.png)
- Có một vài tham số như
  - **ROTA** cho bạn biết liệu một block device (file đại diện cho một loại thiết bị nào đó với dữ liệu có thể đọc hoặc ghi theo dạng block) có thuộc về thiết bị lưu trữ dạng quay không, giá trị `1` là biểu thị dạng đĩa quay (HDD), `0` là không thể quay (SSD).
 - **DISC-GRAN** cho thấy mức độ chi tiết của việc loại bỏ hay giải phóng các khối dữ liệu không sử dụng. Đĩa cứng (HDD) không hỗ trợ tính năng này nên cột này hiển thị giá trị 0.
 - `lsblk -o +ROTA,DISC-GRAN`
 ![](https://imgur.com/cDidhpZ.png)
 - Khi thấy một danh sách các phân vùng, bạn có thể biết những gì chúng lưu trữ, dựa trên hệ thống dung lượng của chúng. 
    - Câu lệnh `lsblk -o +FSTYPE,LABEL`
![](https://imgur.com/HMBCFGY.png)
  - Hiển thị thiết bị di động hoặc thẻ nhớ USB
    - Câu lệnh `lsblk -o +RM` : lệnh này sẽ hiển thị thêm một cột cho bạn biết liệu thiết bị có thể tháo rời không. Giá trị **1** đồng nghĩa với **true**, ám chỉ một USB hoặc các loại phương tiện di động khác.
![](https://imgur.com/vDtOnHI.png)
  - Hiển thị model HDD/SSD: hữu ích trong việc bạn muốn tra cứu code chính xác của model thiết bị lưu trữ để nâng cấp firmware hoặc tải xuống driver.
    - Câu lệnh ` lsblk -d -o +MODEL`
![](https://imgur.com/3WaUwPt.png)
- Hiển thị UUID (Universally Unique Identifier) hệ thống file
  - Các bản Distro Linux cũ đã mount hệ thống file bằng cách chỉ định tên thiết bị của chúng trong `/etc/fstab`. Điều này không đáng tin cậy bời vì `/dev/sda2` có thể trở thành `/dev/sdb2`, khi ta thêm một thiết bị lưu trữ khác vào hệ thống. Vì vậy **UUID** được sử dụng thay thế, giá trị **UUID** vẫn không đổi dù cho bạn thêm vào hoặc loại bỏ bất chúng khỏi máy tính.
  - Để hiển thị UUID ta dùng câu lệnh: `lsblk -o +UUID`
![](https://imgur.com/YLoow1b.png)
## Lệnh dd
![](https://imgur.com/78sGWPI.png)
- dd là một lệnh giúp chuyển đổi và sao chép tệp. Câu lệnh `dd` được dùng để sử dụng trong các trường hợp sau:
  - Sao lưu và phục hồi toàn bộ dữ liệu ổ cứng hoặc một partition
  - Chuyển đổi định dạng dữ liệu từ ASCII sang EBCDIC hoặc người lại
  - Sao lưu lại MBR trong máy 
  - Chuyển đổi chữ thường sang chữ hoa và ngược lại
  - Tạo một file với kích cỡ cố định
  - Tạo một file ISO
- Cấu trúc câu lệnh ` dd if=<địa chỉ đầu vào> of=<địa chỉ đầu ra> <option>`
  - Option:
    -  `bs` = bytes: đọc ghi bao nhiêu file 1 lần
    -  `cbs`= bytes: chuyển đổi bao nhiêu byte một lần
    -  `count`= Blocks: thực hiện bao nhiêu block trong quá trình thực thi câu lệnh
    -  `skip`=blocks: bỏ qua bao nhiêu block đầu vào
    -  `conv`= Convs: chỉ ra các tác vụ cụ thể sau đây
      - `ascii`: chuyển đổi từ mã EBCDIC sang ASCII
      - `ebcdic`: chuyển đổi từ mã ASCII sang EBCDIC
      - `lcase`: chuyển đổi từ chữ thường sang hết thành chữ hoa
      - `ucase`: chuyển đồi từ chữ hoa sang chữ thường
      - `nocreat`: không tạo ra file đầu ra
      - `noerror`: tiếp tục sao chép dữ liệu khi đầu vào bị lỗi
      - `sync`: đồng bộ dữ liệu với ổ đang sao chép
  - Các định dạng byte được quy định như sau:
    - c = 1 byte
    - w = 2 byte
    - b = 512 byte
    - kB = 1000 byte
    - K = 1024 byte
    - MB = $ 10^6 $ byte    
    - M = (1024*1024) byte
    - GB = $ 10^9 $ byte   
- VD: Sao lưu toàn bộ ổ cứng
  - Câu lệnh: `dd if = /dev/sda of = /dev/sdb`: if đại diện cho đầu vào và of đại diện cho tập tin đầu ra. Tức là sau khi thực hiện xong câu lệnh trên, bản sao của /dev/sda sẽ có trong /dev/sdb.
- Tạo bản sao lưu của thư mục, tệp hoặc phân vùng và tạo image(iso,...)
  - Câu lệnh: `dd if=/dev/sda4 of=/home/backup/partition.img`
  - Khôi phục bản sao lưu trước đó bằng câu lệnh `dd if=/home/backup/partition.imd of=/dev/sda41`
- Sao lưu từ đĩa CDrom: ` dd if=/dev/cdrom of=/root/cdrom.img conv=noerror`
- Sao chép MBR: `dd if=/dev/sda1 of=/root/mbr.txt bs=512 count=1`
- Chuyển đổi chữ thường thành chữ hoa
`dd if=/root/test.doc of=/root/test1.doc conv=ucase`
- Tạo một phân vùng trống có dung lượng cố định
` dd if=/dev/zero of=/root/file1 bs=100M count=1`
> ## Lệnh mkdir 
- mkdir là viết tắt của (make directories)
- Là một lệnh cho phép user được tạo thư mục rỗng trên hệ điều hành Linux. 
- Có thể tạo được đồng thời nhiều thư mục, cũng như set quyền cho cả thư mục khi tạo ra.
- Cú pháp:
  - `mkdir  [option] [tên thư mục]`.
  - VD: `mkdir new` là tạo thư mục mới có tên là `new`
  - Các option như
    - `-m` :phân quyền cho thư mục. VD `mkdir -m 440 newdir` là tạo một thư mục tên là `newdir` với giá trị phân quyền là `440`.
    - `-p`: tạo thư mục con và tạo kèm thư mục cha của nó. VD: `mkdir -p /root/thu_muc1/thu_muc2` là tạo một thư mục cha có tên là `thu_muc1` sau đó tạo thư mục có tên `thu_muc2` là thư mục con của `thu_muc1`
    - `-v`: là hiển thị quá trình tạo ra thư mục và cho ra các thông tin như khởi tạo thư mục thành công hay thất bại, thư mục nào đã tồn tại.
  > ## Lệnh touch
  - Trong linux, mỗi file đều liên kết và chứa các thông tin
    -  `timestamp` 
    -  Thời gian truy cập
    -  Thời gian chỉnh sửa và thay đổi cuối cùng.
- Vì vậy khi tạo file mới, truy cập hay chỉnh sửa file thì `timestamp` này cũng tự động cập nhật chính xác lại thời gian trên file.
- Lệnh touch là một lệnh tạo file trên linux
- Cú pháp: ` touch [option] [file]`
  - Tạo 1 file txt rỗng (0 byte) mang tên **newfile**:  `touch newfile.txt`
  - Tạo ra nhiều file **a.txt**, **b.txt**, **c.txt**: `touch a.txt b.txt c.txt`
- Các option
  - `-a`: thay đổi thời gian truy cập file 
  - `-c`: tránh tạo file mới khi file không tồn tại
  - `-m`: cập nhật thời gian chỉnh sửa lần cuối cùng
  - `-c -t YYDDHHMM`: chỉnh thời gian truy cập và chỉnh sửa thời gian truy cập của file theo ngày giờ cụ thể.
  - `-t YYMMĐHHMM.SS`: chỉ định thời gian cụ thể khi tạo file
> ## Lệnh rm (remove files or directories)
- Là một dòng lệnh tiện ích được dùng để xoá các file và thư mục.
- Cú pháp `rm [option] [file]`
- file ở đây có thể là 1 hoặc nhiều file các file dk ngăn cách nhau bởi dấu cách.VD. `rm file1 file2 file3`
- Các option
  - `-d`: xoá thư mục 
  - `-r`: xoá thư mục không có dữ liệu và tất cả các file bên trong thư mục đó.
  - `-i`: yêu cầu nhắc người dùng xác nhận trước khi xoá dữ liệu.
  - `-l`: chỉ đưa ra 1 lời nhắc xác nhận khi xoá nhiều file.
  - `-rf`: xoá một thư mục hoặc file được bảo vệ chống ghi.
> ## Lệnh rmdir
- Dùng để xoá thư mục
- Cú pháp: `rmdir [option] [thư mục]`
- VD1: `rmdir thu_muc1` là xoá thư mục 1
- VD2: `rmdir thu_muc1 thu_muc2 thu_muc3` là xoá nhiều thư mục rỗng cùng 1 lúc. Chỉ xoá các thư mục rỗng còn không rỗng sẽ không bị xoá.
- Các option:
  -  `-p`: xoá thư mục hiện tại và cả thư mục cha của nó. VD `rmdir -p new1/new2`. Là xoá new2 rồi xoá new1, khác với `rmdir new1/new2` câu lệnh này chỉ xoá /new2 còn new1 vẫn giữ
  -  `-v`: in ra kết quả thư mục đã xoá
> # Lệnh echo
- Là một câu lệnh hiển thị một đoạn văn bản lên màn hình
- Cú pháp `echo [option] [text]
- Ví dụ: `echo vi du ve lenh echo` sẽ cho ra màn hình như sau
![](https://imgur.com/lj8dz0Z.png)
- Ví dụ 2: Gán một giá trị và dùng lệnh `echo` để gọi giá trị đó ra
```
# x = 10
# echo gia trị cua x là $x
```
![](https://imgur.com/KZY1R0W.png)
- Tìm kiếm các file có đuôi nào đó tại thư mục đang đứng. Ví dụ tìm kiếm file có đuôi `.txt` bằng echo như sau
![](https://imgur.com/law5WMY.png)
- Ghi vào file bằng echo. VD ghi đoạn text `day la file 1` vào file test
![](https://imgur.com/3ck7ctN.png)
> # Lệnh cp
- Là câu lệnh dùng để sao chép 1 file hoặc thư mục trong linux
- Sao chép 1 file tại thư mục đang làm việc sang thư mục ~/Documents
` cp file.txt ~/Documents/`
- Sao chép khi không đứng tại vị trí thư mục đang đứng, ta dùng đường dẫn 
`cp ~/Downloads/file.txt ~/Documents/
- Đổi tên file khi đang sao chép bằng
`cp ~/Downloads/ten_file_cu.txt ~/Documents/ten_file_moi.txt
- Sao chép nhiều file bằng cách liệt kê các file vào trong dấu {}. Ví dụ
` cp ~/Downloads/{file1,file2,file3,jpg,...} ~/Documents/`
- sao chép tất cả các file cùng loại
` cp ~/Download/*.jpg ~/Pictures/`
- Muốn sao chép nhiều loại file hơn ta cũng đặt vào trong dấu {}. VD `cd ~/Download/*.{jpg,png} ~/Picture/`
- Cụ thể hơn của câu lệnh cp
` cp [option] source destination`
- Option 
  - `-r`, `-R`: sao chép toàn bộ thư mục.
  - `-v`: hiển thị quá trình copy.
  - `-a`: copy toàn bộ thư mục và thêm thuộc tính duy trì của file.
  - `-n`: ép buộc lệnh copy không được ghi đè nếu file nguồn và file đích trùng tên.
  - `-f`: ép ghi đè khi 2 file bị trùng tên.
  -  `-p`: copy nhưng giữ lại các thuộc tính của file. Các thuộc tính bao gồm
    - Access time
    - Modification date
    - User ID
    - Group ID
    - File mode
    - Access Control Listst  
## Lệnh sed (stream editor)
- Là công cụ giúp thao tác với văn bản như tìm kiếm, chỉnh sửa xoá bằng dòng lệnh
- Cấu trúc lệnh `sed [options] [scripts] [input_file]
- Option:
  - `-i`: chỉnh sửa trực tiếp vào file.
- Cho 1 file `test.txt` có nội dung
```
Noi dung thu 1
Noi dung thu 2
Noi dung thu 3
```
- TH1: Tìm kiếm và thay thế (phân biệt chữ hoa và chữ thường). VD tìm kiếm từ `dung` và thay thế bằng `DUNG`:
` sed s/dung/DUNG/ test.txt`. Màn hình sẽ hiện nội dung sau khi thay thế, tuy nhiên nội dung gốc vẫn không bị ảnh hưởng.
![](https://imgur.com/VwTCB63.png)
- TH2: Tìm kiếm và thay thế (thay đổi luôn nội dung file). `sed -i s/dung/DUNG/i test.txt`
![](https://imgur.com/hCh51Qq.png)
- TH3: Tìm kiếm và thay thế (lưu nội dungg thay đổi ra file mới)
` sed -i .modified s/dung/DUNG test.txt`
## Câu lệnh wget (world wide web get)
- Là một câu lệnh dùng để trích xuất dữ liệu và nội dung từ nhiều web servers khác nhau.
- Để có thể sử dụng câu lệnh wget, ta cần tải nó về bằng `yum install -y wget`
- Sử dụng wget để tải từng file và lưu nó vào thư mục hiện hành. Ví dụ 
- Sử dụng wget để tải nhiều file bằng cách
  - Tạo một file `test.txt` sau đó mở nó lên và ghi cho nó các nội dung cần tải. Ví dụ:
```
https://wordpress.org/latest.zip
https://downloads.joomla.org/cms/joomla3/3-8-5/Joomla_3-8-5-Stable-Full_Package.zip
https://ftp.drupal.org/files/projects/drupal-8.4.5.zip
``` 
  - Lưu file lại sau đó chạy câu lệnh `wget -i test.txt`  . `-i` để lấy tất các các file chứa trong file test.
- Tải file về máy dưới 1 tên khác. Ví dụ `wget -O wordpress-install.zip https://wordpress.org/latest.zip`. Ý nghĩa là file tải về sẽ được lưu dưới tên wordpress-install.zip thay vì tên gốc.
- Tải file về 1 thư mục được chỉ định. Ví dụ: `wget -P documents/archives/ https://wordpress.org/latest.zip`. Lúc này file tải về sẽ xuất hiện trong thư mục documents/archives/.
- Giới hạn tốc độ tải file được dùng khi ta muốn tải 1 file lớn và tránh trường hợp chúng dùng hết băng thông của bạn. Ví dụ  `wget --limit-rate=500k https://wordpress.org/latest.zip` .
- Đặt số lần thử tải lại được dùng khi kết nối internet bị gián đoạn gây lỗi quá trình tải về. Để xử lý ta có thể tăng số lần thử lại bằng các dùng option `-tries`. VD: `wget -tries=100 https://wordpress.org/latest.zip`. 
- Tải file trong background được sử dụng khi ta muốn tải file cực lớn và cho nó chạy ẩn để làm các tác vụ khác. Ví dụ: `wget -b https://example.com/beefy-file.tar.gz`. Và để kiểm tra tiến trình và tính trạng ta dùng lệnh `tail -f wget-log`
- Tiếp tục tải file khi bị gián đoạn, mà không muốn tải lại file từ đầu, ta thêm option `-c`. VD: `wget -c https://example/very-big-file.zip`
- Tải nhiều file và ta muốn đánh stt cho chúng. Ví dụ `wget http://example.com/images/{1..50}.jpg`