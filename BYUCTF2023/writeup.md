<h1>Challenges I solved:</h1>

- <strong>Jail</strong>:
  - Leet 1

- <strong>Forensics</strong>:
  - kcpassword
  - Bing Chilling
  - What does the cougar say ?
  

<h2>Jail</h2>
<h3>Leet 1</h3>

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/d4d530a5-654f-414c-8c96-28ab14050188)
- From the source code, we know that if we enter a number and the number is not equal to 1337 then we get nothing. But there is an <code>eval</code> function that can execute anything inside. So with this simple payload we can get the flag: <code>print(FLAG)</code>
<h2>Forensics</h2>
<h3>kcpassword</h3>
- We are given a file contains password. On Mac machine, if auto-logon is enabled then the password is XOR with a static string and stored in a file. So I found this script that can do it: https://tinyapps.org/blog/201709070700_kcpassword.html

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/28ecbc3e-4011-41d4-9929-601583fd85b5)
 
 
 <h3>Bing Chilling</h3>
- Extract from the zip file and we are given a <code>.odt</code> file which is like a zip file so I opened in WinRar and examine then I saw flag in a xml file contains macro

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/fa78b0f5-e57a-4b97-b5fe-c0a1bd62b38b)

 <h3>What does the cougar say ?</h3>

 - We are given a .mp4 file. While watching, I noticed at around 1:02 minute of the video there is a pop up embeded so I use <code>ffmpeg</code> to get every frames of the video and saw a half of a flag
 
 ![Screenshot 2023-05-20 105027](https://github.com/M1nh-Duk/Writeups/assets/100038173/46e920df-0473-482d-945f-3909c32bedab)
 - The other half I got by opening the video in audacity and view the spectrogram
  ![Screenshot 2023-05-20 151556](https://github.com/M1nh-Duk/Writeups/assets/100038173/bc71f16f-0e1a-4ed4-b674-5d2c59db3b42)
