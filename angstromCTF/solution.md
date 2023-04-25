<h1>
    angstromCTF 2023

</h1>

<h3>
    Challenges I solved :
</h3>

* Misc
    - Physics HW
    - Admiral Shark
    - Simon Says
    - better me 
* Web

    - Celeste Speedrunning Association
    - shortcircuit
    - directory
    - Celeste Tunneling Association

<h2>
    Misc
</h2>

<h3>
    Physics HW
</h3>     

- We are given a PNG file
![](https://i.imgur.com/mnO0YfI.png)
- Using <code>zsteg</code> to get the flag which is hidden by LSB steganography
![](https://i.imgur.com/CIDZ48d.png)


<h3>
    Physics HW
</h3>     

- We are given a pcap file. After analyzing, I found suspicious stream

![](https://i.imgur.com/6aAY2wV.png)

- Extract it, it appears to be a ZIP file because of those "PK". However, it is broken so we have to fix it by adding the local header of the first entry of the zip file (by adding "504b0304")

![](https://i.imgur.com/nvtRou0.png)

- Rename the file to zip, open and look for the flag
![](https://i.imgur.com/FPyJTyj.png)
 
<h3>
    Simon Says
</h3>     

- My teammate wrote this script and I adjusted a little bit
```

from pwn import *

check = "Combine the first"

r = remote("challs.actf.co", 31402)

for i in range(21):
    string = r.recvline()
    first_three = string[31:34]
    last_three = string[-4:-1]
    result = first_three + last_three
    
    r.sendline(result) 
    print(string)
    #print(f"Attempt: {i}, result: {result}")
    
  
         
r.interactive()

```
- However, running the script from our shells was insufficient because it's too slow. So I ran it on a cloud environment <b>Replit</b> and it's suprisingly fast enough to get the flag

![](https://i.imgur.com/bLAo6tG.png)

<h3>
better me 
</h3>     

- This chall is a bit tricky at first and I had to search a lot to find the correct way to jailbreak the GPT model. Luckily, I found an appropriate prompt in this site https://www.jailbreakchat.com/ and get the flag 

![](https://i.imgur.com/nL2asVf.png)

<br>
<h2>
    Web
</h2>


<h3>
Celeste Speedrunning Association
</h3>     

- We are given a site to submit a button. Just simply open Burp and adjust the request parameter and get the flag

![](https://i.imgur.com/vAbUhEm.png)

<h3>
Celeste Speedrunning Association
</h3>     
- We are given a site with a srcipt

![](https://i.imgur.com/5EWBRI0.png)
- Just reverse the script and get the correct flag

![](https://i.imgur.com/07dfMO7.png)

<h3>
    Directory
</h3>     

- We are given a site with many directories (4999)
- I wrote a simple script to find the correct directory and get the flag
```
import requests

for i in range (4999):
    print(f"Trying: {i}")
    response = requests.request('GET',f"https://directory.web.actf.co/{i}.html")
    # print(response.text)
    if "your flag is in another file" in response.text:
        pass
    else:
        print(f"URL: https://directory.web.actf.co/{i}.html ")
        print(f"Content: {response.text}")
        break
```
![](https://i.imgur.com/27IhqPE.png)

<h3>
   
Celeste Tunneling Association
</h3>  

- We are given a site with source code. Read the code and find that if the host to be "flag.local" then we could get the correct site

![](https://i.imgur.com/XCZJ3UX.png)

![](https://i.imgur.com/8UZVoW4.png)

- Open burp to adjust the header and get the flag

![](https://i.imgur.com/TxgkWOb.png)
