<h1>Challenge description</h1>

![image](https://user-images.githubusercontent.com/100038173/207758145-9525959d-b4af-41a8-9e8e-cde67ba2e88d.png)
<h1>BEGIN</h1>

- Đề bài có cho tải 1 file xls. Thử mở file ra trên Window thì chỉ thu đc 1 sheet
![image](https://user-images.githubusercontent.com/100038173/207758687-7793923d-728d-4a12-afc3-67eba5fc0897.png)
- Để kiểm tra xem có ô nào có chữ màu trắng không thì Ctrl + A và chuyển chữ sang màu đỏ thì phát hiện ở phía dưới có các chữ số nhưng chưa biết để làm gì 
![image](https://user-images.githubusercontent.com/100038173/207758900-09b9e0c4-bd47-4888-ae50-387f55614cc1.png)
- Theo gợi ý của đề bài là trong đó có nhiều file ẩn đi nên mở bằng 7z của Window để giống với 1 file system.
![image](https://user-images.githubusercontent.com/100038173/207759053-fa7c638e-471a-4cff-aad0-4eb9181ff2eb.png)
- Thử mở file sharedString.xml trong thư mục xl thì có được các chỉ dẫn của bài. Có vẻ là tìm số và chuyển sang ASCII
![image](https://user-images.githubusercontent.com/100038173/207760333-73e29c88-e180-43b5-8d21-8d0b46897e0e.png)
- Mở worksheets thì có tới tận 4 sheets. 
![image](https://user-images.githubusercontent.com/100038173/207759096-de4d4de3-8cec-47f1-b14f-20fe60649d53.png)
- Thử kiểm tra thì 3 cái đầu đều là sheet bình thường tuy nhiên sheet2 và sheet3 bị ẩn khỏi excel nên ko thấy được. Có sheet4 chứa hint 
![image](https://user-images.githubusercontent.com/100038173/207759434-50f2c9a8-0e66-42c2-9567-307726b59701.png)
- Dựa vào từ cuối "DUPer hidden rows" có thể là các rows trong sheet bị ẩn đi. Để kiểm tra thì thử mở file xml của sheet1 
![image](https://user-images.githubusercontent.com/100038173/207759645-bae64ecd-f1e3-49a8-bbf0-42a3f7621aa9.png)
- Thử lấy các giá trị của từng row để so sánh với các row hiển thị trong sheet thì quả thực có những số bị ẩn đi
![image](https://user-images.githubusercontent.com/100038173/207760071-49c7f048-1b76-425f-b1f0-e2afcaef97b4.png)
- Thử chuyển các số bị ẩn đó sang mã ASCII thì có được phần đầu của flag
![image](https://user-images.githubusercontent.com/100038173/207760528-902d5e0f-6c16-44f9-8c78-eb3c76b544f3.png)
- Lặp lại quá trình với sheet2 và sheet3 thì ta thu được toàn bộ flag
![image](https://user-images.githubusercontent.com/100038173/207760647-f3b27d29-2385-4e91-a372-9622daab92aa.png)
