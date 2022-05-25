> # SE linux (Secure-enhanced Linux)
- Là một tính năng bảo mật của Linux kernel, được thiết kế để bảo vệ máy chủ chống lại các cấu hình sai và/hoặc các compromised daemons.
- Nó đặt các giới hạn và chỉ thị cho server và các trương trình: những file nào user có thể truy cập và những hành động nào user có thể thực hiện bằng cách đưa ra một chính sách bảo mật.
# DAC - Discretionary Access Control
- Là phương pháp giới hạn truy cập vào các đối tượng (file, dvd,...) dựa trên quyền truy cập của nhóm mà chúng thuộc về.
- Quyền truy cập trên đối tượng `user` (owner của file), `group`(tất cả các user thuộc group), `others` (các user không thuộc cả hai nhóm trên)
- Nhược điểm của DAC là khi 1 chương trình xâm nhập hệ thống và thừa hưởng quyền truy cập của user thực thi chương trình, khi đó chương trình xâm nhập có thể làm mọi việc mà user có quyền.
# MAC - Mandatory Access Control
- Phương pháp này thực thi theo nguyên tắc "quyền tối thiểu" và an toàn hơn.
- Các trương trình khi chạy chủ có thể làm những gì chúng cần để thực hiện nhiệm vụ, ngoài ra không được làm gì khác.
- VD: Nếu có một chương trình đáp ứng các yêu cầu đến 1 `socket` mà không cần truy cập vào file system, thì chương trình đó chỉ được lắng nghe trên 1 `socket` cố định mà không có quyền đụng đến file system. Nếu hacker tấn công và kiểm soát chương trình đó thì quyền truy cập của nó cũng được tối thiểu hoá rõ ràng.
- SE linux (MAC) phân loại đối tượng trong hệ thống Server làm 2 loại, sau đó sẽ đánh nhãn để kiểm soát và giám sát chương trình tương tác giữa 2 loại:
  - Subject: `user`, `process`
  - Objects: `files` (text/binary/sockets/named_pipes)
- Mặc định SE linux sẽ không cho phép tương tác giữa Subject và Object.
- SE Linux vẫn giữ nguyên các đắc tính của DAC và thêm vào các chức năng trên giúp hệ thống an toàn hơn nhiều.
# Có nên tắt SE linux
- Khi tắt SE linux, tức là đang loại bỏ cơ chế bảo vệ hệ thống khỏi những rủi ro bảo mật.
- Nếu có thể hiểu chuyên sâu SE linux và sử dụng chúng một cách thành thạo điều đó thì rất là tốt.
- Tuy  nhiên đối với người dùng cơ bản như quản lý VPS/Hosting hay những người không cần sự rườm ra thì hãy tắt ngày SE Linux đi, vì khi cài đặt và vận hành hệ thống Linux trên Centos/RHEL sẽ rất hay vướng phải các rule xử lý quyền hạn của SE Linux gây mất thời gian tìm hiểu và xử lý vấn đề, gián đoạn các hoạt động dịch vụ khác.
# Cách tắt SE linux
- Bước 1: Kiểm tra trạng thái hoạt động của SE Linux bằng câu lệnh `sestatus` và `getenforce`.
![](https://imgur.com/zfrsJCS.png)
- Tắt SE Linux tạm thời
  - Chỉ tắt SE Linux tạm thời trong thời gian hệ thống còn đang chạy. Nếu hệ thống restart lại thì tính năng SE Linux sẽ khôi phục lại trạng thái ban đầu trước khi bị tắt tạm thời
  - Câu lệnh: `sentenforce 0`
- Tắt SE Linux vĩnh viễn
  - Chỉnh sửa lại file `/etc/selinux/config`, thay đổi giá trị cấu hình SE Linux sang `disabled`
  - Câu lệnh: `vi /etc/selinux/config`
1[](https://imgur.com/M0mkDE6.png)
  - Sau khi edit tiến hành reboot và kiểm tra