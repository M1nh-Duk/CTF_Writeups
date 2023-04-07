<h1>Description </h1>
<b>The iMoS is responsible for collecting and analyzing targeting data across various galaxies. The data is collected through their webserver, which is accessible to authorized personnel only. However, the iMoS suspects that their webserver has been compromised, and they are unable to locate the source of the breach. They suspect that some kind of shell has been uploaded, but they are unable to find it. The iMoS have provided you with some network data to analyse, its up to you to save us.</b>
<h1>Solution</h1>
- This is a large pcap file with over 19000 packets

![image](https://user-images.githubusercontent.com/100038173/230541632-8f5b7e71-814c-4389-a06b-d458a277a5f0.png)

- There are many protocols in this file but the first thing to look at is HTTP protocol

![image](https://user-images.githubusercontent.com/100038173/230541852-20a350b4-f109-45b6-9123-7270c0eecfc9.png)

- After digging around quite much time, I found that there is a webshell from the ip address of <b>146.70.38.48</b> so this could possibly the ip address of the attacker
![image](https://user-images.githubusercontent.com/100038173/230542281-51e14f9e-7b38-4560-a204-0a73a32b591f.png)
- Filtered this ip and looked around for a bit more, I found there is a suspicious packet containing PHP script 

![image](https://user-images.githubusercontent.com/100038173/230543229-c7120251-01be-4cfe-8412-d7ca63138b5f.png)
![image](https://user-images.githubusercontent.com/100038173/230543509-e8910068-33fc-4645-90db-c51c36a783f1.png)
- This is an obfusticated PHP script and by changing the last line from "eval" to "echo", I can have the full code which contains the flag

![image](https://user-images.githubusercontent.com/100038173/230543682-444d06ff-685b-4a0a-944c-60709d9d54b3.png)


