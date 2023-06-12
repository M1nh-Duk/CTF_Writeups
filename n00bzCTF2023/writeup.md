<h1> A beginner friendly and fun CTF. My team ranked 72/855 <h1>
<h1>Challenge I solved</h1>
  <h2>For</h2>
  
  -  Crack & Crack
  - Avengers
  - Hecked
  - LSB
  - BeepBop
  
   <h2>Mics</h2>
  
  - Google Form 1
  - Numbers
  - Amazing Song Lyrics
  
  <h2>OSINT</h2>
  
  - Damn
  - Mission Moon
  - Lost
  - Try to hack me
  - The online Odyssey



  <h3>Crack & Crack</h3>
  
  - Using <code>zip2john</code> and <code>pdf2john</code> and <code>john</code> to crack 2 password required and get the flag
 <h3>Avengers</h3>
  
  - Got a video file which contains a bunch of changing binary, using this command to extract every frames from it <br><code>ffmpeg -i flag.avi output_frame%03d.png</code>
  - To read the content of each images and convert to string then use this script (Use in WSL): 
  
```
from PIL import Image
import pytesseract
import os

# Folder path containing the images
folder_path = '.'  # Replace with the path to your folder
res=[]
flag=''
# Iterate over the files in the folder
for filename in os.listdir(folder_path):
    # Check if the file is an image
    if filename.endswith('.png') :
        # Construct the full file path
        image_path = os.path.join(folder_path, filename)

        # Open the image file
        image = Image.open(image_path)

        # Perform OCR on the image
        text = pytesseract.image_to_string(image)
        res.append(text.replace('\n', ''))
        # Print the file name and extracted text
try:
    for i in res:
        i = int(i,2)
        flag+=chr(i)
except:
    pass
    
print(flag)
```
<h3>Hecked</h3>
- Given a pcap file and the question requires us to find the needed information to make the correct flag as follow:
  <b>"Flag is n00bz{md5sum(vulnerableService_serviceVersion_attackersFirstBashCommandOnTheHackedServer)}"</b>
- Simply just open and look around then I found the service is vsFTPd (not FTP), version number and the first command is <code>id</code>
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/b5aa68f1-ef10-417e-aec4-3008c11f196f)
  
<h3>LSB</h3>
  
- As the name provided, we have to extract the LSB stream in this wav file 
 - Use <code>stegolsb</code> to do it and we have the flag
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/e5536521-0078-4ba9-8fe9-809d0b5999c7)
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/6c6e26e9-6154-4347-9500-42139071a16d)

<h3>BeepBop</h3>
  - This is a SSTV audio then just use <code>RXSSTV</code> to get the flag
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/cb9dc894-3286-4ebc-963c-71f8fe236d4b)
  
  <h3>Google Form 1</h3>
  - Simply <code>CTRL U and CTRL F</code>
![Screenshot 2023-06-10 155605](https://github.com/M1nh-Duk/Writeups/assets/100038173/0d9b9e74-5f49-4e2f-b895-ce7c3197d59d)

<h3>Numbers</h3>
  
  - Use this script to solve:
  ```
  from pwn import *
import re
# Set up the connection to the nc server
host = 'challs.n00bzunit3d.xyz'  # Replace with the actual server IP
port = 13541  # Replace with the actual server port
conn = remote(host, port)

# Receive and print the initial message from the server
initial_message = conn.recvline().decode().strip()
print(f"Received: {initial_message}")

# Start the loop
while True:
    # Send a response to the server
    server_response = conn.recvline().decode().strip()
    match = re.match(r'How many',server_response)
    if match:
        numbers=re.findall(r'\d+',server_response)
        a = numbers[0]
        b = numbers[1]
        count=0
        for i in range(1, int(b)):
            count += str(i).count(a)
        print(f"Received: {server_response}")
        print(numbers)
        print(count)
        
        conn.sendline(str(count).encode())
    print(server_response)
  ```
  <h3>Amazing Song Lyrics</h3>
  
  - Google sign language  
  
  <h3>Damn</h3>

  - Google and find that this is the picture of recent dam which is broken in Ukraine, however don't trust Google Lens in this picture because it's said this dam is in China :)) 
  ![dam](https://github.com/M1nh-Duk/Writeups/assets/100038173/4a90d1d9-88d9-4875-acb9-0cc114a54992)
  
  <h3>Mission Moon</h3>
  - Use Google Lens and ChatGPT to solve
  <h3>Lost</h3>
  - This chall is indeed a very intersting one because I spent a lot of time and also the picture is distorted
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/574f70c2-e1bc-4d10-8bb6-9428389a8af8)
 - Starting by looking for the bridge in the middle of the picture. Using google lens, it's said some kind of bridge in the SanFransico, USA and after some time searching, it's <code>Oakland Bay Bridge</code> near Golden Gate Bridge.
  - Then I used a lot of time to locate the position because the angle is pretty hard to tell so I use google earth to try different location to represent the same angle as in the picture. And finally this is quite the near 
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/becdbef4-0d1f-4099-aaf5-771fb1d9f349)
- Now it's a bit guessy because the picture has flowers and there is a garden on the street  so I tried that name and got correct
  ![Screenshot 2023-06-11 011739](https://github.com/M1nh-Duk/Writeups/assets/100038173/73a5c3bd-f352-4293-9cea-60762bc39b44)
  
  <h3>Try to hack me</h3>
- Given a username and a supposedly hint "Try to hack me"
  
