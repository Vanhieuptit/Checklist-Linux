- Nén và giải nén là các lệnh thông dụng dùng để đóng gói và nén dữ liệu cơ bản trong linux
## Gzip - Gunzip
- Gzip được dùng khá phổ biến trong nền tảng Unix/Linux.
### Nén Gzip 
`gzip ten_file`
hoặc
`gzip [đường dẫn file] [tên file]`
- VD `gzip /etc/file1`
### Giải nén Gzip 
` gzip -d [đường dẫn file] [tên file]`
hoặc
` gunzip [đường dẫn file] [tên file]`
- VD: `gzip -d /etc/file1`
## Tar
- Gzip chỉ có thể làm việc trên 1 tập tin hoặc 1 dòng dữ liệu, do đó không thể lưu trữ được nhiều tập tin. Vì vậy, nếu muốn sử dụng cho nhiều tập tin thì chúng ta phải sử dụng TAR để đóng gói các file đó lại.
- Câu lệnh: `tar [options] [tên file].tar [các file cần đóng gói]`
  - VD: `tar -cvf file.tar file1 file1 file1 folder1 folder2`. Trong đó  `file.tar` là tên file mà chúng ta đặt, file1, folder1 là các tệp, thư mục muốn đóng gói trong tar.
- Các [option]:
  -  `c` được dùng tạo file lưu trữ
  -  `x` được dùng giải nén file lưu trữ
  -  `z` dùng nèn với gzip - luôn luôn cần có khi làm việc với định dạng tập tin gzip
  -  `j` nén với bunzip2 - luôn có khi làm việc với tập tin bunzip2 (.bz2)
  -  `f` chỉ đến file lưu trữ sẽ tạo-luôn có khi làm việc với file lưu trữ
  -  `v` hiển thị những tập tin đang làm việc lên màn hình
  -  `r` thêm tập tin vào file đã nén
  -  `u` cập nhật file đã có trong file nén
  -  `t` liệt kê những file đang có trong file nén
  -  `delete` - xoá file đã có trong file nén
  -  `totals` hiển thị thông tin số file tar
  -  `exclude` loại bỏ file theo yêu cầu trong quá trình nén
- Bung file ` tar -xvl file.tar`
  - Options:
    - `-x` (extract): giải nen (untar) gói định dạng .tar  
### Đóng gói và nén dữ liệu
- Tar thông thường chỉ giúp gom dữ liệu. Để nén dữ liệu giảm thiểu dung lượng, ta cần dùng các tuỳ chọn nén `z` cho **gzip** (định dạng .gz) hoặc `j` đối với **bunzip** (định dạng .bz2)
- Câu lệnh: ` tar -czvf file.tar.gz file1 file2 file3` thay `z` bằng `j` nếu dùng **bunzip**
- Giải nén: `tar -xzvf file.tar.gz`
- Lưu trữ và bỏ qua tập tin theo yêu cầu
- Câu lệnh: `tar -cvf [ten file] [đường dẫn] --exclude='tên file cần loại bỏ'`
  - VD: loại bỏ file *.pyc ra khỏi việc đóng gói nén dữ liệu tại thư mục /usr/lib/python3/dist-packages/apt ` tar -cvf ten_file.tar /usr/lib/python3/dist-packages/apt --exclude='*.pyc'`
## Zip - Unzip
- Cài đặt Zip bằng câu lệnh ` yum install -y zip` 
-  Cài đặt UnZip bằng câu lệnh ` yum install -y unzip` 
- Nén file / thư mục:
` zip -r file.zip file1 file2 file3`
- Nén file / thư mục có mật khẩu bảo vệ được mã hoá:
` zip -er file.zip file1 file2 file3`
- Giải nén bằng câu lệnh ` unzip file.zip`
- Giải nén file vào 1 thư mục cụ thể: ` unzip -d file-dir file.zip`