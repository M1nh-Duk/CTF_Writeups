<h1>
    CyberHavoc CTF - Forensics
</h1>
<br>
<h2>
    The Cryptic Sound

</h2>
<h3> Description</h3>
    
Elliot was working late at night when he suddenly heard a strange sound coming from his computer. At first, he thought it was just a glitch or some interference, but the sound kept repeating. Elliot felt a strange sense of unease and began to suspect that there might be a hidden message in the sound.
<h3> Solution</h3>

- We are given a .wav file. Open it and listen we can see that it is morse code.
- Simply put it in the Decoder online and grap with the flag format  
![](https://i.imgur.com/m7mNxEp.png)

<br>
<h2>
Broken Inside
</h2>
<h3> Description</h3>
    
Elliot got this broken data, seemed to contain some hidden information, possibly related to the havoc he had been investigating. Fixing this could lead him to valuable clues in his pursuit of the rogue group responsible for the chaos in the cyber world.

<h3> Solution</h3>

- This is a steganography challenge. Both <code>file</code> and <code>exiftool</code> cannot identify the file so we have to see the hex 

![](https://i.imgur.com/JzRXY6h.png)
![](https://i.imgur.com/vlx9nCQ.png)

- We can see some familiar chunks like <code>IDAT</code>, <code>IEND</code> at the end of the file, <code>bKGD</code>,<code>cHRM</code>,... so this is definitely a broken <b>PNG</b>
- Go to wiki(https://en.wikipedia.org/wiki/PNG) to correct the <code>Header</code> and <code>IHDR</code> chunk of the image, rename and get the flag 
![](https://i.imgur.com/p03bETe.png)

<br>
<h2>
Decrypting the Memories
</h2>
<h3> Description</h3>
    
Elliot came across a mysterious file while investigating a cyber attack. The file had an unknown extension and appeared to be encrypted. Elliot realized that it might contain important information related to the attack and decided to analyze it. He spent hours trying to decrypt the file, but his efforts were in vain. Just when he was about to give up, he noticed some strange patterns in the code. He continued to dig deeper and was eventually able to extract valuable information from the file. The information led him to the source of the attack, allowing him to take appropriate action and prevent any further damage.


<h3> Solution</h3>

- We are given a zip file but it is password protected. Just try to crack it using <code>zip2john</code> and <code>john</code>

![](https://i.imgur.com/YaEFsUG.png)
- Then we have a memory dump file so we can use volatility 3 to analyze it 

![](https://i.imgur.com/DoNNjZn.png)
- Listing all the current processes, we can see that there are suscpicious process named <code>cmd.exe</code> with PID of 1892 and <code>notepad.exe</code> with PID of 1596  

![](https://i.imgur.com/YH5fTRX.png)

- Since there is <code>cmd.exe</code> so we must check the cmd
- Nothing important but we have this line:

![](https://i.imgur.com/BIXS8OW.png)

- Now we must find and dump that file. However, using plugin <code>filescan</code> that file canot be found so digging around with the keyword <code>Document</code> I found many suspicious files and after dumping, the file "I_am_Here.txt.txt.txt" contains Morse code
![](https://i.imgur.com/lcjGSQD.png)
- Decode and replace the # sign to get the flag
![](https://i.imgur.com/3zwtR8I.png)
