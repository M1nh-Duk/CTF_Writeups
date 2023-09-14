![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/1f4e3fcb-cfb6-41d6-8980-43688932e712)

- Given a memory dump, I used Volatility to analyze it. Since the question mentions "password", I tried plugin <code>hashdump</code> of volatility 2 to get the existing hashes.
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/00f08599-6a92-42e5-8932-0ce9aab95dcf)

- Used crackstation to crack the last hash, I got the password but failed to submit the flag so probably not this one
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/d03e8c1e-bc9b-4cec-bebf-5e6e4336d6ff)

- Now let's list the process running

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/8206fcf8-cb19-44eb-ad0f-bdff356bf1f1)

- There is TrueCrypt.exe running, so it might encrypt something
- Let's check the command line to get closer to the processes
  
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/c6e65403-64f3-47be-8cb9-972447bc7374)
- So mspaint.exe and notepad.exe seem suspicious. I tried to dump the files opened by both processes but only the "findme" of notepad can be dumped.
- However, this file is unreadable if opened by notepad

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/3b5104ce-3745-4b7f-8285-f32117cd7757)

- Remember the process TrueCrypt.exe is running, it's pretty sure this file is encrypted
- Research a little bit, I found that TrueCrypt can not only encrypt the whole disk, it can encrypt partitions so this file may be the encrypted partition.
- I also found a way to decrypt it from another chall. (https://ctftime.org/writeup/37415)
- After decryption, there are 3 files but 2 of them are for trolling :)) The last one is an <code>odt</code> file. It's kind of a zip file so let's unzip it.
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/90bff343-8a42-4717-a9d5-2f5dda8016dc)
  - In the "data" folder there is a keepass database file. I tried to crack the password using john but then I remembered that there is 1 password that we found at the first place but not used yet.
  - Use that password to open and got almost 4300 passwords :)

  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/c0422e6e-0ab2-4c3f-93bb-fd865271b246)

- Now to find a way to get all those password (https://keepass.info/plugins.html#kpscript)
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/d09763bb-63a4-4204-b742-ee3c5571c8df)

- When scrolling down the list I found a very long base64 string

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/d415c62c-060a-4c6c-a196-825beea52bc9)

- So the final thing to do is use cyberchef to decode this string many times :(  and get the flag 

![Screenshot 2023-09-14 220122](https://github.com/M1nh-Duk/Writeups/assets/100038173/d4a8e2ab-44ef-4770-968c-55da88c5a3c4)

