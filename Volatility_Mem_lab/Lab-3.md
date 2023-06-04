<h1>Lab 3 - The Evil's Den</h1>
<h3>Challenge Description</h3>

- A malicious script encrypted a very secret piece of information I had on my system. Can you recover the information for me please?
- Note-1: This challenge is composed of only 1 flag. The flag split into 2 parts.
- Note-2: You'll need the first half of the flag to get the second.
<h3>BEGIN</h3>

- Với chall này, theo gợi ý của bài phát hiện ra đoạn script bằng filescan và grep
![image](https://user-images.githubusercontent.com/100038173/203980426-44a7e655-c762-4237-b75a-8c0002743336.png)
- Dump và mở file ra thì phát hiện thêm file vip.txt
![image](https://user-images.githubusercontent.com/100038173/203980702-38919841-e621-4a3f-99e4-d4d3c4c82c54.png)
![image](https://user-images.githubusercontent.com/100038173/203980804-adc3a342-def7-476e-9a7b-ef3bb08b2f24.png)
- Phân tích code thấy đoạn text được xor theo bài và sau đó được encode base64 nên cần decode và xor lại theo function bài để ra flag
![image](https://user-images.githubusercontent.com/100038173/203980842-7afcfc18-9bcb-4eb2-89aa-821600ee53cd.png)
![image](https://user-images.githubusercontent.com/100038173/203981415-5d0086c8-e561-4e9e-b6ce-75462f3bb959.png)
- Sử dụng phần đầu của flag này và dùng steghide với file ảnh được tìm thấy trong Desktop
![image](https://user-images.githubusercontent.com/100038173/203981572-be68dfbc-f801-4af0-a425-aa188831d3fe.png)
![image](https://user-images.githubusercontent.com/100038173/203981593-c68a92df-27af-4110-acdb-297dbfe672e7.png)

