
![Screenshot 2023-07-10 180107](https://github.com/M1nh-Duk/Writeups/assets/100038173/8cb4eefd-7dbd-4e9f-a11c-0aa4995271ff)

- Đề bài cho chúng ta 1 file NTUSER.DAT. Đây là file chứa các registry key của user hiện tại trên máy victim.
- Vậy nên chúng ta sẽ load nó vào <code>regedit</code> trên Windows

  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/d274ada1-74cf-4ef6-a291-095abd077c4a)
- Sau khi thử tìm với các key liên quan đến bài thì trong key <code>\Software\Microsoft\Windows\CurrentVersion\Run</code> chứa code Powershell khả nghi

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/c7dd2d95-f47b-4b40-a4f8-d49f2b57f986)
