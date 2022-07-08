# Keepalive là gì?
- HTTP là một giao thức không duy trì trạng thái kết nối. Khi client mở một kết nối TCP đến server, gửi request, nhận response xong xuôi thì sẽ đóng kết nối.
- Trường hợp client gửi rất nhiều request tới server, thì server sẽ phải đóng mở kết nối một cách liên tục, cách tiếp cần này rất không hiệu quả.
- Trong Nginx, keepalive là một chỉ thị được sử dụng để giữ kết nối mở cho một số yêu cầu nhất định đến máy chủ hoặc cho đến khi hết thời gin chờ yêu cầu. Trong thời gian duy trì kết nối, nếu client muốn gửi một request khác thì có thể sử dụng luôn kêt nối này thay vì phải tạo lại một kết nối TCP khác.
- Các nhà phát triển Nginx cho biết, 10000 kết nối không hoạt động sẽ chỉ sử dụng 2.5MB bộ nhớ
# Lợi ích của keepalive trong Nginx 
- Việc khởi tạo kết nối TCP mới có thể tiêu tốn nhiều tài nguyên như bộ nhớ và CPU. Tuy nhiên, việc giữ cho kết nối của bạn tồn tại trong Nginx có thể làm giảm mức sử dụng này. 
- Vì vậy, việc lưu giữ các kết nối https rất được khuyển khích.
- Nó có thể cải thiện trải nghiệ người dùng và hiệu suất của trang web. 
- Giúp tăng tốc độ trang web do khả năng cung cấp nhiều tệp trên cùng một kết nối, giảm độ trễ và tăng tốc độ tải trang web.
# Cấu hình keepalive trong Nginx
- Mở file cấu hình nginx
```
vi /etc/nginx/nginx.conf
```
- Các giá trị của keepalive có thể được được đặt trong khối http, server, 
- **keepalive_timeout**: cho biết máy chủ phải đợi bao lâu để nhận được yêu cầu từ máy khách. Tham số này thường vào khoảng từ 6 đên 10s. Nếu giá trị này quá cao, máy chủ sẽ bị quá tải và tài nguyên RAM sẽ bị lãng phí.
- **keepalive_disable**: cho phép bạn tắt tính năng keepalive cho các họ trình duyệt cụ thể. Cú pháp là 
```
keepalive_disable browser1 browser2:
```
- **keepalive_request**: qua một kết nối keepalive duy nhất, giá trị keepalice_requests cho biết số lượng yêu cầu tối đa mà nó có thể xử lý. Giá trị mặc định cho **keepalive_requests** là 100. Tuy nhiên, có thể đặt giá trị cao hơn, có xu hướng hữu ích trong việc thử nghiệm với tiện ích tạo tải gửi nhiều yêu cầu từ một ứng dụng khách.
# Mấu cấu hình keepalive trên nginx
```
upstream backend_sv {

  server 123.123.123.123:8080;
  server 123.123.123.124:8080:

  keepalive 32;
  keepalive_timeout 20s;
  keepalive_requests 20;
  keepalive_disabled msie6 safari;
}
```
- Với cấu hình này, Nginx sẽ giữ 32 kết nối tới mỗi backend server. Nếu có nhiều request được gửi đến và cần nhiều hơn 32 kết nối để kết nối tới mỗi upstream server thì Nginx sẽ mở thêm một số kết nối mới để đáp ứng nhu cầu hiện tại.
- Sau khi lượng request đã trở về mức bình thường thì Nginx sẽ đóng bớt các kết nối ít được dùng nhất để giảm số lượng kết nối về lại con số 32 như ta đã định.