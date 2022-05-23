> # Processes trong linux
- Process (hay tiến trình) được hiểu là khi ta thông báo một lệnh trong Linux, nó tạo và bắt đầu một tiến trình mới. Khi bạn cố gắng thực hiện một lệnh ls để liệt kê nội dung thư mục, bạn bắt đầu một tiến trình.
- Tiến trình hiểu theo cách đơn giản, là một ví dụ của trương trình đang chạy. 
- Có hai loại Process
  - Foreground Process
  - Background Process
## Foreground Process 
- Mọi process mà bạn bắt đầu chạy là foreground process. Nó nhận input từ bàn phím và gửi output tới màn hình.
- Trong khi một trương trình đang chạy trong foreground và cần một khoảng thời gian dài, chúng ta không thể chạy bất kỳ lệnh khác (bắt đầu một process khác) bởi vì dòng nhắc lệnh không có sẵn tới khi chương trình đang chạy kết thúc process và thoát ra.
- Ví dụ:
![](https://imgur.com/Vp5ikM2.png)
## Background Process
- Background process chạy mà không được kết nối với bàn phím của bạn. Nếu background process yêu cầu bất cứ đầu vào từ bàn phím, chương trình sẽ đợi.
- Lợi thế của chạy một trương trình trong background là có thể chạy các lệnh khác: không phải đợi tới khi nó kết thúc để bắt đầu một process mới.
- Để bắt đầu một background process, thêm dấu "&" tại cuối lệnh.
- VD: ping -c 10 8.8.8.8 &
![](https://imgur.com/pb8M0HG.png)
## Jop ID với Process ID
- Background process và foreground thường được thao tác thông qua số Job ID.
- Job ID thì khác với Process ID và được sử dụng vì nó ngắn hơn
- Một công việc có thể bao gồm nhiều process đang chạy trong seri hoặc tại cùng một thời gian, song song, vì thế sử dụng Job ID là dễ dàng hơn theo dõi các tiến trình riêng lẻ.
## **Parent Process** (PPID) và **Child Process** (PID)
- Mỗi tiến trình Unix có hai ID được gán cho nó: Process ID (PID) và Parent ID (PPID)
- Mỗi tiến trình trong hệ thống có một Parent Process
## Zombie Process và Orphan Process
- Thông thường, khi một tiến trình con(Child Process) bị `kill`, tiến trình cha (Parent Process) được thông báo thông qua ký hiện `SIGCHLD`. Sau đó, Parent Process có thể thực hiện một vài công việc khác hoặc bắt đầu lại child process nếu cần thiết.
- Tuy nhiên, đôi khi parent process bị `kill` trước khi **Child process** của nó bị `kill`. Trong trường hợp này, **parent process** của tất cả các process, "init process", trở thành PPID mới. Đôi khi những process này được gọi là **Orphan Process**
- Khi một process bị `kill`, danh sách liệt kê `ps` có thể vẫn chỉ **process** với trạng thái `Z`. Đây là trạng thái `Zombie`, hoặc **process** không tồn tại. **Process** này bị `kill` và không được sử dụng. Những process này khác với Orphan Process. Nó là những **process** mà đã chạy hoàn thành nhưng vẫn có một cổng vào trong bảng **process**
## Daemon Process
- Là các **background process** liên quan tới hệ thống mà thường chạy với quyền hạn truy cập của **root** và các dịch vụ yêu cầu từ **process** khác.
# Bảng thông tin về Process
- Hệ điều hành lưu trữ một cấu trúc danh sách bên trong hệ thống gọi là bảng tiến trình.
- Một **Bảng tiến trình** quản lý tất cả PID của hệ thống cùng với thông tin chi tiết về các tiến trình đang chạy.
- Các tham số
  - `UID` là tên của người dùng đã gọi tiến trình
  - `PID` là định danh mà hệ thống cấp cho tiến trình
  - `PPID` là định danh của tiến trình cha
  - `C` là số tiến trình con của một tiến trình
  - `STIME` là thời gian tiến trình cha được sử dụng
  - `TIME` là thời gian chiếm CPU của tiến trình
  - `CMD` toàn bộ dòng lệnh khi tiến trình được triệu gọi
  - `TTY` là màn hình terminal ảo nơi thực hiện tiến trình
# Các câu lệnh về Process
- `ps` - process status
- Dùng để quan sát các process đang chạy
- Cấu trúc lệnh
` ps [options]`
  - Option: 
    - `-f` (full format): hiển thị đầy đủ thông tin về các **process** 
    - `-e`: hiển thị đầy đủ các process (bao gồm cả system process).
    - `-A`: trả về kết quả tương tự `-e` ![](https://imgur.com/Uy71Cvg.png)
     - `-u`: hiển thị các process liên quan đến user hiện hành đang sở hữu. Để liệt kê ra cùng lúc nhiều user là sử dụng dấu `,` để ngăn cách giữa các user.![](https://imgur.com/sOkazhR.png)
     - `-p PID`: hiển thị thông tin process cụ thể
     - `-C`: hiển thị các tiến trình có câu lệnh được chỉ ra. VD `ps -fC tên lệnh`
     ## Tắt tiến trình đang chạy
     - Sử dụng câu lệnh khi ta gặp phải tình trạng một ứng dụng không hoạt động và chúng ta không thể đóng nó lại bằng cách bình thường
     - Để đóng một chương trình đang chạy, ta phải kiểm tra xem `PID` của nó là gì. Sau đó ta sử dụng câu lệnh `kill PID` để tắt tiến trình. VD 
![](https://imgur.com/TAQ0IIf.png)
