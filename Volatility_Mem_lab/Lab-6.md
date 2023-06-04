<h1>Lab 6 - The Reckoning</h1>
<h3>Challenge Description</h3>

- We received this memory dump from the Intelligence Bureau Department. They say this evidence might hold some secrets of the underworld gangster David Benjamin.
- This memory dump was taken from one of his workers whom the FBI busted earlier this week. Your job is to go through the memory dump and see if you can figure something out.
- FBI also says that David communicated with his workers via the internet so that might be a good place to start.
<h3>BEGIN</h3>

- Sử dụng plugin pslist,chúng ta có thể thấy có các process đáng chú ý gồm chrome.exe,firefox.exe,WinRAR.exe,cmd.exe
![image](https://user-images.githubusercontent.com/100038173/204959341-aa5905c1-b7e2-4f34-bbf7-a375013bf1a1.png)
- Do có cmd.exe nên thử check các tham số bằng cmdline thì thấy có file flag.rar
![image](https://user-images.githubusercontent.com/100038173/204959457-7d091b6f-bb51-4dbf-94aa-bb7ad785cecd.png)
- Dump file và thử giải nén tuy nhiên thì cần password và có vẻ đây là phần thứ 2 của flag.
![image](https://user-images.githubusercontent.com/100038173/204959567-cc07d9a3-a2b9-445f-a2de-3bf703a327ff.png)
- Do có process của chrome nên ta thử tìm lịch sử duyệt web
![image](https://user-images.githubusercontent.com/100038173/204959941-85768eb1-3724-4c94-b20f-708f5f87b72b.png)
- Dump file có offset là <b>0x000000005da5a610</b> và mở bằng sqlite3 do format của history trong chrome là sqlite database
![image](https://user-images.githubusercontent.com/100038173/204960139-88bd271c-8aaf-4f45-986f-082cbc9924f7.png)
- Truy vấn bảng urls bằng câu lệnh <i>select * from urls</i> và trong 7749 urls như vậy, có 1 đường dẫn khả nghi
![image](https://user-images.githubusercontent.com/100038173/204960493-73d79242-3a74-4feb-ac6c-76bc6948f8df.png)
- Thử patse và tìm kiếm trên google thì có được 1 đường dẫn tiếp theo và gợi ý
![image](https://user-images.githubusercontent.com/100038173/204960630-1cbffef9-66da-4228-a875-b058b6216afe.png)
- Tiếp tục patse and search thì ta có được 1 file doc với ngôn ngữ khá lạ và khá dài
![image](https://user-images.githubusercontent.com/100038173/204960775-dd0ce21d-2a36-4f1d-bcca-fff09964a354.png)
- Khá troll khi tác giả để 1 url giữa đống ngôn ngữ kì lạ đó (may mắt mình 10/10 😅) 
![image](https://user-images.githubusercontent.com/100038173/204961003-b3e9c5e6-a05d-4a66-8c78-b268bcb20b85.png)
- Và chúng ta có 1 link Mega tuy nhiên lại cần key để giải mã. 
![image](https://user-images.githubusercontent.com/100038173/204961180-2dca2929-8f55-4aad-a542-10e5d9bf82a5.png)
- Trong url trước có gợi ý là gửi trong mail nên thử grep toàn bộ xem có cái mail nào không
![image](https://user-images.githubusercontent.com/100038173/204961363-659453b7-7c30-4fe8-b357-fc1d713aaf30.png)
- Trong rất nhiều kết quả hiện ra thì đột nhiên có 1 email address tương ứng với cái tên David Benjamin mà đề bài gợi ý vậy mà mình quên mất :(( 
- Chuyển sang grep với cái email address đó và thu được 1 đoạn key là "zyWxCjCYYSEMA-hZe552qWVXiPwa5TecODbjnsscMIU"
![image](https://user-images.githubusercontent.com/100038173/204961938-c377bd43-375d-425e-8bd2-7a5b6c70966c.png)
- Thử và thành công giải nén được file Mega 
![image](https://user-images.githubusercontent.com/100038173/204962165-3872e5fa-8d96-4319-8b5c-f23917388ae0.png)
- Tải về và mở ra là có phần flag thứ nhất 

![image](https://user-images.githubusercontent.com/100038173/204962216-c7b8bf60-9dd1-477b-865f-305e7fcd34d7.png)
- Tuy nhiên phần flag vừa tìm lại không phải key để giải nén file rar kia. Nên cần đi tìm 
- Đến đây thì do khá bí nên quyết định nhờ trợ giúp từ writeup và hóa ra đã bị sót 1 bước mà ko để ý.
- Do có cmd.exe nên ngoài cmdline thì còn cần dùng plugin consoles và có dòng env gợi ý về Environment variables.Nên thử dùng plugin envars và thấy password 

![image](https://user-images.githubusercontent.com/100038173/204965062-d41f0ef2-f083-4e35-b602-775ed7f2653b.png)
- Đến đây thì cơi như xong, giải nén file rar là có nửa còn lại của flag 
![image](https://user-images.githubusercontent.com/100038173/204965215-ee599739-1556-47a5-a6a2-acbc42ecf025.png)
![image](https://user-images.githubusercontent.com/100038173/204965258-930e127e-7511-4aa3-aae6-e7e857b0b9c3.png)



