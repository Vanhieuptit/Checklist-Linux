# Cách thức cài đặt trong Linux
- Các phần mềm trên linux không tự đóng gói sẵn bởi vì chúng phải chạy trên nhiều hệ thống khác nhau trong họ Unix như Solaris, AIX, HP-UX,...
- Với mỗi loại hệ thống, nếu muốn sử dụng được phần mềm thì ta cần phải biên dịch lại chúng.
- Một số nhà phát triển đã biên dịch sẵn các phần mềm cho chúng ta ra các gói có dạng rpm và cùng với sự hỗ trợ của công ty Red Hat, chúng ta cũng đã có những chương trình quản lý các phần mềm một cách hiệu quả.
## Cài đặt từ `rpm`
- RedHat Package Manager (RPM) là hệ thống quản lý những package được linux hỗ trợ cho người dùng.
- Chúng giống như định dạng file nén mà trong đó chứa tất cả những file chạy và cấu hình của phần mềm, thông tin phần mềm, nhà sản xuất, những yêu cầu về hệ thống...
- Đặc tính của RPM:
  - Khả năng nâng cấp phần mềm
  - Truy vấn thông tin hiệu quả
- Package được đóng gói có dạng:
` <Tên package>-<Phiên bản>.<số hiệu>.<kiến trúc>.rpm`
  - VD: teamviewer-14.2.8352.x86_64.rpm
- Cú pháp lệnh **rpm**:
` rpm [options] <package/package_name>`
  - Options:
    - `i`: cài đặt
    - `-e`: xoá
    - `-u`: update
    - `qa`: tìm phần mềm (đã được cài đặt trên hệ thống)
    - `ql`: tìm nơi cài đặt
    - `--nodeps`: không kiểm tra các gói phụ thuộc
    - `-v` verbose hiển thị đẹp mắt hơn
    - `-h`: hiển thị dấu # khi giải ném gói
- VD: rpm -ivh teamviewer-14.e.8352.x86_64.rpm
## Cài đặt từ Yum
- YUM (yellowdog updater modifier): cài đặt, xoá, truy vấn các phần mềm từ các reposity trên internet hay local một cách tự động.
- yum phải được chạy dưới quyên root
- Cú pháp lệnh Yum:
` Yum [options] [name/group_of_software]`
- Options:
  - `-y`: thực hiện theo lệnh mà không cần hỏi
  - `install`: cài đặt phần mềm
  - `remote`: xoá phần mềm
  - `list installed`: xem các phần mềm đã cài đặt
  - `groupinstall`: cài 1 nhóm phần mềm
  - `groupremove`: gỡ bỏ 1 nhóm phần mềm
  - `clean`: xoá các cache, plugin, meta-data...
  - `search`: tìm kiếm các phần mềm trên các repo 
  - `update`: cập nhật phần mềm
- Kiểm tra các repo có sẵn:
```
# cd /etc/yum.repos.d
# ls
```