<h2>DOWN BAD</h2>

- We are given a PNG in this chall. With the chall's name contains "Down" and the picture pointing downward so I think of changing the height and get the flag:
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/182d0908-a7dc-4ca3-bbe3-9c75764a644a)

<h2>LIST</h2>

- We are given a pcap file in this chall. Since the description of the chall suggests that there is a RCE and we can find that there is a site to upload command with the source of <code>index.php</code>

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/6db15ed1-1a26-406b-8a33-c08dec750025)

- Follow the stream to see the commands. So far, there are 2 commands of this stream: <code>id</code> and <code>ls</code>
<br> We know that the command is sent to the web using <code>POST</code> method. Now filter to get any POST method of other streams

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/82da3941-d7c6-431c-8a2d-ea819c6b3a72)

- There are about 30 packets that contain command. Try to run some first commands we can see that the <code>name</code> option of the command (find) contains TFCCTF:
  
![Screenshot 2023-07-31 165355](https://github.com/M1nh-Duk/Writeups/assets/100038173/a68737c7-fd25-4415-9f1d-f73d9b9effe0)

- Now use tshark and a bit of formating to get the flag

  ![Screenshot 2023-07-28 210913](https://github.com/M1nh-Duk/Writeups/assets/100038173/b82eda7f-726b-47c2-bb2e-89d215f7eecd)
