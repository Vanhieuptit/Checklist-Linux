# Find
- Câu lệnh `find [không gian tìm kiếm] [options]`
- Options:
  - `-name [tên file]`: tìm kiếm file với tên đã biết.
     - VD1: `find / -name root` là tìm kiếm file có tên là `root` nằm trong thư mục `/` 
     - VD1: `find /etc -name *.conf` là tìm kiếm file có đuôi `.conf` trong thư mục `/etc`
  - `-atime`(**access time**): thời gian file được read hoặc write
  - `-mtime` (**modify time**): thời gian file được sửa đổi
  - `-ctime` (**change time**): thời gian thông tin của file được thay đổi như (chủ sở hữu file, loại, sự cấp phép của file,...)
     - VD: `find /etc -ctime 2`: tìm file có sự thay đổi mới xảy ra trong 2 ngày vừa qua 
  - `perm [number_mode]`: tìm file theo permission
     - VD: `find /etc -perm 644`: tìm file có permission trong `/etc` là 644
     - Thêm dấu `-` trước `[number_mode]` để biểu thị số `permission` tối thiểu của tìm kiếm
   - `size n` (n là kích cỡ cần tìm)
     - VD: Tìm file có dung lượng 100k trong /etc
```
find /etc -size 100K (file = 100K)
               +100K (file > 100K)
               -100K (file < 100K)
```
  - `-uid [UID]`: tìm theo user sở hữu
  - `gid [GID]` : tìm theo group sở hữu file
  - ` -maxdepth [level]`: tìm theo cấp cao nhất của thư mục con 
  - ` -mindepth [level]`: tìm theo cấp nhỏ nhất của thư mục con
  - `type [features]` : tìm theo thể loại 
    - `f`: file thường
    - `d`: thư mục
    - `l`: symbolic link (soft link)
    - `c`: character devices
    - `b`: block devices
  - `-amin`, `-mmin`, `-cmin`: tìm kiếm theo phút
  - `-name head*`: tìm file bắt đầu bằng `head`
# Which
- `which` là 1 chương trình đơn giản và nhỏ gọn có mục đích xác định đường dẫn file thực thi. Nó phép user có thể sử dụng output của chương trình làm thông tin đường dẫn tuyệt đối thành input cho các lệnh hay shell script khác `$PATH`.
- Cấu trúc lệnh
` which [options] [command]`
  - `-a`: hiển thị toàn bộ các đường dẫn file trương trình được tìm thấy trên các thư mục
    - VD: `which -a echo`
# whereis
- Là trương trình giúp tìm 3 thông tin sau về 1 trương trình hoặc 1 command trên linux:
  - Đường dẫn file binary
  - Đường dẫn vị trí source code
  - Đường dẫn vị trí trong manual cho trương trình hay command đó
- Câu lệnh:
` whereis [options] [program/command]`
- Tìm đường dẫn đến trương trình: mặc định, `whereis` sẽ tìm cả 3 thông tin liên quan:
 - `-b`: chỉ tìm file binary
 - `-m`: chỉ tìm file manual
 - `-s`: chỉ tìm file source code 