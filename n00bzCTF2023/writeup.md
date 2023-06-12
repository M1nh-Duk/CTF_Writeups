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

