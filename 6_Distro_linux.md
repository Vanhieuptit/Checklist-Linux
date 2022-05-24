> # Distro là gì? Điều gì tạo nên distro?
- Distro là khái niệm để chỉ một hệ điều hành được tạo dựng từ tập hợp nhiều phần mềm dựa trên nhân Linux.
- Một bản distro Linux điển hình bao gồm `Linux Kernel`, `các công cụ và thư viện GNU`, `các phần mềm thêm vào`, `tài liệu`, và một `Window system` (phần lớn sử dụng X Window System), và `window manager`, và một `môi trường desktop`.
## Tại sao lại có distro?
- Đối với hệ điều hành như Windows hay Mac OS, nếu muốn sử dụng một phiên bản với các chức năng khác nhau, bạn phải cần chọn một trong các phiên bản mà Microsoft đang cung cấp.
- Với linux, các phiên bản hệ điều hành Linux không được sản xuất bởi một tổ chức duy nhất. Để làm nên một phiên bản hệ điều hành thì cần có
  - Nhân Linux
  - Công cụ và thư viên GNU
  - Phần mềm thêm vào
  - Window System
  - Window Manager 
  - Môi trường desktop
 - Các dịch vụ trên được phát triển độc lập với dịch vụ khác và đều là các **Open Source** được phân phối dưới dạng mã nguồn.
- Nếu muốn có một phiên bản Linux, ta phải lấy các mã nguồn đó sau đó tự lắp ráp tất cả. Đó là một công việc vô cùng mất thời gian và khó khăn.
=> Distro sinh ra nhằm cung cấp một bản hệ điều hành hoàn chỉnh bằng cách lặp ghép các dịch vụ trên và cung cấp chúng ở dưới dạng gói, được biên dịch trước. Các gói này nhanh chóng và dễ cài đặt.
># Các bản distro phổ biến
# 1 Debian GNU/Linux
![](https://imgur.com/R3mQCk9.jpg)
- Là một dạng hệ điều hành được phát triển từ sự cộng tác của các tình nguyện viên trên khắp thế giới trong Dự án Debian(công bố vào ngày `16/08/1993`)
- Tất cả các bản phát hành Debian đều có nguồn gốc từ Hệ điều hành GNU.
  - Nhà phát triển: `Debian Project`
  - Họ hệ điều hành: `Unix like`
  - Tình trạng: `Đang hoạt đông`
  - Kiểu mã nguồn:`Phần mềm tự do`
  - Phát hành lần đầu: `Tháng 9/1993`
  - Hệ thống quản lý gói: `APT(mức cao), dpkg(mức thấp)`
  - Loại nhân: `FreeBSD,NetBSD,linux`
  - Giao diện: `GNOME`
  - Giấy phép: `DFSG và các giấy phép tương thích`
  - Website chính thức `www.debian.org`
# 2 Ubuntu 
![](https://imgur.com/kQ0auAY.png)
- Là một hệ điều hành dựa trên Debian GNU/Linux
- Là một phần mềm mã nguồn mở cung cấp cho người dùng tự do chạy, sao chép, phân phối, nghiên cứu, thay đổi và cải tiến phần mềm theo giấy phép GNU-GPL.
- Các phiên bản Ubuntu được đặt tến theo dạng **YY .MM (tên)**. Trong đó YY tương ứng với năm phát hành, MM tương ứng với tháng phát hành, trong ngoặc () là tên được đặt cho phiên bản trước khi phát hành chính thức.
- Ví dụ bản Ubuntu mới nhất hiện tại là **21.10 (Impish Indri)**, phát hành vào tháng `10` năm `2021`.
  - Nhà phát triển: `Cannonical Ltd / Quỹ Ubuntu`
  - Họ hệ điều hành: `Unix-Like`
  - Tình trạng: `Đang hoạt động`
  - Kiểu mã nguồn:`Phần mềm tự do`
  - Phát hành lần đầu: `20/10/2004`
  - Phiên bản mới nhất: `Ubuntu 21.10 (Impish Indri) 14/10/2021`
  - Phương thức cập nhật: `Ubuntu Software Center + APT`
  - Hệ thống quản lý gói: `dpkg, APT, Snap, flatpak`
  - Nền tảng chính: `x86_64, ARM64, ARMhf`
  - Nhân:` Linux`
  - Giao diện: `GNOME 3.38 (Ubuntu 20.04), GNOME 40(Ubuntu 21.10)`
  - Giấy phép: `Chủ yếu là GNU GPL/một số chương trình dịch sẵn thương mại và các giấy phép khác.`
  - Website chính thức:` www.ubuntu.com`
# 3 Fedora Linux
![](https://imgur.com/WIy9dXt.jpg)
- Là một bản phân phối Linux được phát triển dựa trên cộng đồng theo Fedora Project và được bảo trợ bởi Red Hat (một công ty con của IBM), với sự hỗ trợ thêm từ công ty khác.
  - Nhà phát triển: `Fedora Project`
  - Tình trạng: `Hoàn tất`
  - Mã nguồn: `Mở, phần mềm tự do`
  - Phát hành lần đầu:` 6 tháng 11 năm 2003`
  - Phiên bản mới nhất: `Fedora 35/ ngày 2/11/2021`
  - Đối tượng: `Desktop, server, Cloud`
  - Phương thức cập nhật:` Yum`
  - Nền tảng chính: `x86_64`
  - Nhân: `Linux`
  - Giao diện : `GNOME Shell KDE Xfce`
  - Giấy phép:` Nhiều giấy phép phần mềm khác nhau`
# 4 Red Hat Enterprise Linux (RHEL)
![](https://imgur.com/HllEy2z.png)
- Là một distro Linux được phát triển bởi Red Hat và mục tiêu hướng tới thị trường thương mại
  - Nhà phát triển: `Red Hat`
  - Họ hệ điều hành:` Linux`
  - Kiểu mã nguồn: `phần mềm tự do`
  - Phiên bản đầu tiên: `Red Hat Enterprise Linux 2.1`
  - Phiên bản mới nhất: `Red Hat Enterprise Linux 7.5`
  - Giấy phép : `GPL`
  - Website chính thức:` www.redhat.com/rhel/`
# 5 CentOS 
![](https://imgur.com/pHh5OFV.png)
- Là một distro Linux, có nguồn gốc hoàn toàn từ Red Hat Enterprise Linux
  - Nhà phát triển : `CentOS Project`
  - Họ hệ điều hành:` Unix-like(dựa trên RHEL)`
  - Tình trạng: `Đang phát triển`
  - Kiểu mã nguồn: `Phần mềm tự do nguồn mở`
  - Phát hành lần đầu: `14 tháng 5 năm 2004`
  - Đối tượng: `Free computing(desktop, mainframe, server, workstation) `
  - Phương thức cập nhất: `Yum`
  - Hệ thống quản lý gói:  `RPM Package Manager`
  - Nền tảng chính: `x86_64`
  - Nhân:` Monolithic (Linux)`
  - Giao diện :` GNOME và KDE `
  - Giấy phép :`GNU GPL và giấy phép khác`
  - Website chính thức:` CentOS.org`
# Tài liệu tham khảo
https://vi.wikipedia.org/wiki/Debian
https://vi.wikipedia.org/wiki/Ubuntu
https://vi.wikipedia.org/wiki/Fedora
https://vi.wikipedia.org/wiki/CentOS
https://vi.wikipedia.org/wiki/Red_Hat_Enterprise_Linux