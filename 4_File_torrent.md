> # Hiểu về File Torrent trên Internet
![](https://imgur.com/DaBTvg7.png)
- Trước tiên ta cần hiểu một số khái niệm cơ bản sau
# Mạng ngang hàng P2P (Peer to Peer)
- Là một kiến trúc mạng không định sẵn máy chủ và máy khách, hay nói cách khác, tất cả các máy tham gia đều bình đẳng và được gọi là **Peer**, 1 **peer** đóng vai đồng thời là máy khách và máy chủ ở trong mạng.
- Các thiết bị trong mạng ngang hàng không thuộc sở hữu của các nhà cung cấp dịch vụ, mà đơn giản là các máy tính được người sử dụng kiểm soát.
# Phân bố tệp trong P2P
- Trong mô hình client-server, máy chủ phải gửi tệp tới từng thiết bị một điều này, áp đặt một tải trọng khổng lồ lên máy chủ và tiêu tốn lượng băng thông máy chủ rất lớn
- Trong mô hình P2P, mỗi thiết bị có thể phân bố lại bất cứ lượng tệp nào mà nó nhận được tới bất cứ thiết bị ngang hàng khác.
# BitTorrent
- Đây là một giao thức mã nguồn mở thông dụng nhất trong mô hình P2P. 
- Người dùng sẽ tạo một file meta (hay chính là file **torrent** ta đang tìm hiểu) chứa thông tin về bản tải xuống mà không thực sự cung cấp dữ liệu tải xuống
- Trình theo dõi (**Tracker**) là yếu tố cần thiết để lưu trữ file torrent này, cùng với người hiện đang lưu trữ file đó.
- Vì BitTorrent là giao thức mở nên bất kỳ ai cũng có thể lập trình phần mềm máy khách hoặc **Tracker**
> ***Tổng kết lại một file.torrent là để tải xuống dữ liệu nhưng file này chỉ chứa thông tin về bản tải xuống của file chứa không chứa toàn bộ dữ liệu của file.*** 