<h1>Lab 2 - A New World</h1>
<h3>Challenge description: </h3>
- One of the clients of our company, lost the access to his system due to an unknown error. He is supposedly a very popular "environmental" activist. As a part of the investigation, he told us that his go to applications are browsers, his password managers etc. We hope that you can dig into this memory dump and find his important stuff and give it back to us.
<h3>BEGIN</h3>

- Gợi ý từ đề bài:<br>"environmental" activist -> có thể gợi ý về environment variable<br>"applications are browsers, his password managers" -> có thể là các tiến trình đang chạy<br>"his important stuff" -> có thể là file tên important
- Sau khi xác định profile, sử dụng pslist thì ta có các tiến trình khả nghi bao gồm chrome.exe, KeePass.exe và notepad.exe

![image](https://user-images.githubusercontent.com/100038173/203689603-c3a66188-5593-4a36-a1ce-4734b7ffe622.png)
- Sử dụng gợi ý đầu tiên là về environment variable ta dùng plugin envars để thu được toàn bộ và thấy 1 đoạn text khả nghi:
![image](https://user-images.githubusercontent.com/100038173/203690099-6c076ba8-1f14-4e94-8d3b-bc86cd41ef50.png)
- Decode base64 thì thu được flag đầu tiên
![image](https://user-images.githubusercontent.com/100038173/203690155-0678fe33-0bd8-4693-a3a7-86a6ef525d54.png)
- Trong process list vẫn có cmd.exe vì vậy nên thử chạy plugin cmdline và thấy được có 1 file lạ tương ứng với process KeePass.exe
![image](https://user-images.githubusercontent.com/100038173/203911796-2b5b7898-a229-45a4-b4e0-778c7e096108.png)
- Tìm và dump file ra sau đó mở bằng KeePass trên Window tuy nhiên database phải có password mới vào được.
- Thử dùng filescan kết hợp với grep password và chúng ta có file Password.png
![image](https://user-images.githubusercontent.com/100038173/203912089-6b42c1ae-fe65-4f7e-b350-27ba92a935bd.png)
- Dump và mở file ra là thấy password
![image](https://user-images.githubusercontent.com/100038173/203912177-fb1301b2-02cb-4ca0-9c15-28e62e715d64.png)
- Mở được database chứa password và ở trong phần Recycle bin sẽ chứa flag
![image](https://user-images.githubusercontent.com/100038173/203912331-a2450338-918c-435c-ae19-d7e862491307.png)
- Copy password ở mục Flag ra là có flag thứ 2
![image](https://user-images.githubusercontent.com/100038173/203912477-2ac627e7-d8d2-4cb5-b46f-66d038dabc4f.png)
- Để tìm được flag 3 với gợi ý là chrome.exe thì ta sẽ đi tìm lịch sử của trình duyệt này. Thử grep -i history và ta có folder 
![image](https://user-images.githubusercontent.com/100038173/203915720-c6ede63e-6adc-4a93-9e57-b49c78fc8c07.png)
- Dump file ra và đổi tên để thuận tiện hơn.
- Được biết file này là dạng database của sqlite và do đó sử dụng tool sqlite3 để xem database này có gì 
![image](https://user-images.githubusercontent.com/100038173/203916033-e0e6c585-3da3-45a3-bf62-9a003ad0f997.png)
- Thử tìm trong bảng urls thì có chứa tất cả các url mà user đã từng search trên chrome
![image](https://user-images.githubusercontent.com/100038173/203916281-44dc3949-1d3d-4519-8713-b009cdf35857.png)
- Trong đó có 1 đường link lạ:
![image](https://user-images.githubusercontent.com/100038173/203916379-1890d4c5-1dfa-4ce1-80d1-87e30e7fc245.png)
- Thử paste lên chrome thì ra 1 folder chứa file Important.zip. Download về và giải nén tuy nhiên file phải có password
![image](https://user-images.githubusercontent.com/100038173/203916977-23da40e1-4a4f-4797-a94c-054296368c2f.png)
![image](https://user-images.githubusercontent.com/100038173/203916610-3692c140-e3ce-4b11-81bc-640385756c21.png)
- Với gợi ý là SHA1 của flag3 lab1 thì dễ dàng có được password
![image](https://user-images.githubusercontent.com/100038173/203916737-7cb5683e-575d-46d6-b6d4-0c8657f3161b.png)
- Cuối cùng unzip và lấy flag 3 thôi
![image](https://user-images.githubusercontent.com/100038173/203916836-fbc54bb6-27ab-4f17-8296-8ffab2a48a79.png)


