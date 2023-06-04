<h1>Lab 5 - Black Tuesday</h1>
<h3>Challenge Description</h3>

- We received this memory dump from our client recently. Someone accessed his system when he was not there and he found some rather strange files being accessed. Find those files and they might be useful. I quote his exact statement,
- The names were not readable. They were composed of alphabets and numbers but I wasn't able to make out what exactly it was.
- Also, he noticed his most loved application that he always used crashed every time he ran it. Was it a virus?
- Note-1: This challenge is composed of 3 flags. If you think 2nd flag is the end, it isn't!! :P
- Note-2: There was a small mistake when making this challenge. If you find any string which has the string "L4B_3_D0n3!!" in it, please change it to "L4B_5_D0n3!!" and then proceed.
- Note-3: You'll get the stage 2 flag only when you have the stage 1 flag.
<h3>BEGIN</h3>

- Sử dụng pslist chúng ta có được process list. Trong đó, có process lạ là NOTEPAD.EXE
![image](https://user-images.githubusercontent.com/100038173/204434107-15c8591b-4cf1-4d30-8678-96d8e292e5aa.png)
- Sử dụng cmdline chúng ta có được các tham số của các process. Trong đó có 1 file đáng ngờ
![image](https://user-images.githubusercontent.com/100038173/204434573-cbc1a322-8615-404c-903c-e574233b3119.png)
- Dump file đó ra và thử giải nén. Tuy nhiên, phải có password để giải nén.
![image](https://user-images.githubusercontent.com/100038173/204434749-42112272-073b-4a31-a96e-0b5aa156f183.png)
- Trong đề bài có gợi ý đến 1 ứng dụng yêu thích nhưng thường xuyên bị crash. 1 trong những ứng dụng mà ai cũng dùng đó là trình duyệt. Vì vậy thử vận may với plugin iehistory xem.
![image](https://user-images.githubusercontent.com/100038173/204435322-04c0e06d-52e3-488f-9a90-969837eb2954.png)
- Có 1 dòng text khả nghi, thử decode nó ra thì thu được flag thứ 1 
![image](https://user-images.githubusercontent.com/100038173/204498946-4f01c0a8-aca5-4af3-91d1-6f41d74f7fb0.png)
- Và dùng flag đó là mật khẩu để giải nén thành công
![image](https://user-images.githubusercontent.com/100038173/204499097-4d090a86-7ff0-4afb-a025-1dcddc0b1b24.png)
- Mở file ảnh đó ra là có được flag thứ 2
![image](https://user-images.githubusercontent.com/100038173/204499240-4d6266dd-5996-41c6-b827-1f545cac5d4c.png)
- Đến đây còn flag thứ 3 chưa được tìm ra. Thử dùng plugin mftparser xem có file nào bị xóa đi hay ko thì thấy được 1 file tên là st4G3$$1.txt khá bí ẩn.
![image](https://user-images.githubusercontent.com/100038173/204500370-bffd21f8-67cd-4fa8-a973-498e53c73a68.png)
- Tuy nhiên thì sau khi thử 1 số cách không tìm ra file đó nên có vẻ như đây là 1 rabbit hole :((
- Thử tìm lại và nhớ ra có hint là Virus và process lạ tên lầ NOTEPAD.EXE, thử dump process đó ra
![image](https://user-images.githubusercontent.com/100038173/204539570-66215bae-9eb6-4c22-854b-2cb54ab0f432.png)
- Sau đó do là file PE nên dùng IDA và cuối cùng thì có được flag là các kí tự ngăn cách nhau
![image](https://user-images.githubusercontent.com/100038173/204539782-56e53ef8-a266-4a02-8264-ac0b767208a8.png)
- Flag 3: bi0s{M3m_l4B5_OVeR_!}


