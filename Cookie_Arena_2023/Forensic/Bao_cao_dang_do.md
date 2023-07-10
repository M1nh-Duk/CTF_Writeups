![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/c3545b2b-ceb3-4cce-bfe9-88e22af6dca3)

- Bài cho chúng ta 1 file crash dump
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/bef28eb4-38b0-4221-8759-10478e622327)
- Sử dụng <code>Windbg</code> để phân tích file này và có được process information cũng như hệ điều hành (OS) mà người dùng sử dụng
  
![Screenshot 2023-07-09 010529](https://github.com/M1nh-Duk/Writeups/assets/100038173/e959330c-06a9-45ad-8de2-b0368cef04ad)

- Có được OS version rồi thì dùng <code>Volatility 2</code> với profile <code>WinSP1x64</code> để đọc file. Trong các process thì có <code>WINWORD.exe</code> phù hợp với description của đề bài
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/b99fa3d4-1c24-4940-a67f-a5688215f8c1)

- Sử dụng plugin <code>handles</code> để xem các tài nguyên mở đến process này thì có 1 file khá đặc biệt

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/df09c184-4734-458b-80f0-e0ab2114f29c)

- Google thì file .asd chính là file lưu tự động của Word để nhằm mục đích phục hồi nếu có sự cố. Dump file này ra và phải bỏ vào đúng đường dẫn mặc định của Word
<code>C:\Users\Username\AppData\Roaming\Microsoft\Word\ </code> sau đó mở lên là phục hồi được và có flag
  
![Screenshot 2023-07-08 181419](https://github.com/M1nh-Duk/Writeups/assets/100038173/4444be2e-d34b-4c17-8546-890d787e0f62)
