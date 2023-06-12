<h1> A beginner friendly and fun CTF. My team ranked 72/855 <h1>
<h1>Challenge I solved</h1>
  <h2>For</h2>
  
  -  Crack & Crack
  - Avengers
  - Hecked
  - LSB
  - BeepBop
  <h2>OSINT</h2>
  
  - Damn
  - Mission Moon
  - Lost
  - Try to hack me
  - The online Odyssey

  <h2>Mics</h2>
  
  - Google Form 1
  - Numbers
  - Amazing Song Lyrics

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
  
 
  

