<h2>LAB 1: Beginner's Luck</h2>
<h3>Challenge description</h3>

<p>My sister's computer crashed. We were very fortunate to recover this memory dump. Your job is get all her important files from the system. From what we remember, we suddenly saw a black window pop up with some thing being executed. When the crash happened, she was trying to draw something. Thats all we remember from the time of crash.</p>

<h3>BEGIN</h3>

- Có 3 gợi ý chính trong đề bài. Đó là:<br> "important file" -> gợi ý về 1 file tên là important hoặc file liên quan đến OS,... <br>"black window pop up with some thing being executed" -> Dễ liên tưởng tới cmd <br> "draw something" -> Chắc là 1 chương trình vẽ nào đó, có thể là paint
- Sau khi dùng plugin pslist thì đúng là có 2 tiến trình khả nghi:
![image](https://user-images.githubusercontent.com/100038173/203567924-a2c8ae16-7245-4ed2-a498-c69fe1a5d275.png)
- Dựa theo hint thứ 2 chúng ta dùng plugin consoles và thấy được 1 đoạn base64 khả nghi
 ![image](https://user-images.githubusercontent.com/100038173/203574716-a18c2d01-b037-4bf4-bd5f-4c517dc875ea.png)
- Decode ra và ta có được flag đầu tiên: 
![image](https://user-images.githubusercontent.com/100038173/203575019-73ab29be-c07d-4643-b6f6-dba54df0e172.png)
- Quay trở lại ảnh đầu tiên ta có 1 tiến trình là cmd.exe vì vậy thử check cmd bằng cmdline
![image](https://user-images.githubusercontent.com/100038173/203576792-6c8b487e-9865-4679-a10a-e4ef8fe627a0.png)
- Chúng ta thấy được có file Important.rar, có vẻ đây chính là gợi ý đầu tiên của bài. 
- Sử dụng filescan kết hợp với grep để lấy được offset của file
![image](https://user-images.githubusercontent.com/100038173/203577920-98fd5996-9fa2-4c29-bd23-bfb27f6ad2ad.png)
- Sau khi lấy được file rar, thử giải nén tuy nhiên cần password và cũng cho gợi ý.
- Sử dụng plugin hashdump theo gợi ý là có được đoạn hash NTLM của Alissa:
![image](https://user-images.githubusercontent.com/100038173/203580652-517b2258-067a-46fb-8f25-1fbd4ac6ed09.png)
- Sử dụng nó để giải nén và có được flag 3
![image](https://user-images.githubusercontent.com/100038173/203580944-12d34f83-cecc-42da-9bdb-9711b7c44b22.png)
<h3> Đoạn này do bí quá nên đọc writeup 😅</h3>
 - Tuy nhiên, chưa tìm được flag 2 và ta chưa sử dụng gợi ý mspaint.exe

 - Sau khi search google, có thể khôi phục ảnh từ data của process mspaint.exe nên sử dụng memdump 

![image](https://user-images.githubusercontent.com/100038173/203590349-5be2827c-7e67-4b59-b8e5-4e04c055a874.png)
- Sau đó, cần đổi tên file từ 2424.dump thành 2424.data để có thể đọc được thành raw data và sử dụng Gimp để nghịch
- Sau khi chỉnh height và width cũng như offset phù hợp thì ta có được flag 2

![image](https://user-images.githubusercontent.com/100038173/203587675-8428be81-78f0-442c-b090-7f2aac461626.png)
