![Screenshot 2023-07-10 204855](https://github.com/M1nh-Duk/Writeups/assets/100038173/cf1cc46d-45a6-44cf-b442-bec50ef35878)

- Bài cho 1 file pcap và như tên của bài thì chúng ta đi tìm protocol tftp. 

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/1fc5f26c-6d7e-488a-9b8e-ba960c911982)

- Từ packet này biết được rằng người dùng gửi yêu cầu đọc file flag.pdf với mode là <code>netascii</code>
- Giao thức này sử dụng UDP và port để control là 69 còn port gửi data là port khác

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/eb0ff105-3b4e-4a44-8bbe-75c57424d3f4)

- Tìm ra được data gửi đi và dùng <code>tshark</code> để lấy chúng đồng thời xóa 4 byte đầu ở các packet do đó là <code>opcode và block number</code> của tftp
- Đến đây thì file PDF bị báo corrupt và không mở được. <a href="https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol">Research thêm một tí </a> thì
mode netascii của tftp sẽ tự động chuyển đổi các kí tự xuống dòng "\n" (LF) thành cặp carriage return (CR) 
-  
