- Trong linux chia làm hai kiểu người dùng là `user` và `root`
# Root
- Là tài khoản dùng để thực thi các module, script cần thiết phục vụ cho hệ điều hành
- Trên một máy chạy hệ điều hành linux chỉ có duy nhất một tài khoản `root` và có thể có rất nhiều `user`
- Tài khoản `root` thường do người quản trị nắm giữ và không thể đổi tên hay xoá bỏ
- Tài khoản `root` có quyền cao nhất, và có thể làm bất cứ điều gì nó muốn vì vậy chỉ nên làm việc với tài khoản `root` khi muốn thực hiện công tác quản trị hệ thống, trong các trường hợp khác chỉ nên làm việc với tài khoản `user`.
# User
- Là những tài khoản để login sử dụng hệ điều hành
- Tài khoản `user` được người quản trị cấp và nó sẽ bị giới hạn một số quyền.
# Các câu lệnh quản lý user
- `useradd`: là lệnh tạo tài khoản user
` useradd [options][login_name]
- **Option** 
  - `-c`(comment):tạo bí danh
  - `-u`: set user ID: mặc định sẽ lấy số ID tiếp theo để gắn cho user (bắt đầu từ 1000)
  - `-d`: chỉ định thư mục home cho user
  - `-g`: chỉ định group phụ (group mở rộng)
  - `-s`: chỉ định sell cho user sử dụng
- `useradd [tên user mới]`: tạo user
- `passwd [tên user cần đặt pass]`: đặt mật khẩu cho user
- `useradd -d /[tên thư mục] [tên user]`: tạo user với thư mục tuỳ chọn
- `useradd -G [tên group]`: tạo user với group tuỳ chọn
- `useradd -M [tên user]`: tạo user nhưng không tạo thư mục riêng
- Xoá user
`userdel [tên user]`
- Tạo group mới: `groupadd [Tên group mới]`
- Đặt mật khẩu cho group: `gpasswd [tên group]`
- Xoá group: `groupdel [Tên group]`
- Thêm user vào 1 group: `usermod -G [tên group]`
- Xoá user ra khỏi group: `gpasswd -d [tên user] [tên group]`
- Xem danh sách các user: đứng ở thư mục /home gõ lệnh `ll`
- Xem danh sách các group: `cat /etc/group/`
- Xem 1 user thuộc những group nào: `group [tên user]` khi ở tài khoản root hoặc lệnh `group` để xem user của mình nằm trong những group nào

