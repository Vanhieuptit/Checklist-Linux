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
>## Các lệnh file system thiết yếu
### pwd (print working directory)
- Cho phép biết thư mục hiện hành mà người dùng đang làm việc


 