<h2> very nice challenge I solved after the competition time</h2>

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/78d00331-3e9d-43d8-ad6a-1041f3fa632e)

- We are given a png file but with nothing to be appeared. Just full of black

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/14a833fe-e10e-4c78-af0d-1a461cc4c320)

- When checking with <code>pngcheck</code> there is something wrong about the compression method. It's supposed to be 00 not 01 so I fixed it.

![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/45d6f02c-9b24-41d6-a3fb-f5f88f385ac8)
- But it's still the same. And I even delete most of the <code>IDAT</code> data but nothing changes. So I guess there's something wrong with the decompression so that the image viewer cannot render the image.
- At here I got stuck because I thought it's the zlib data and I tried to fix and decompress it.
- Turned out it's not zlib and I was suggested that we can search the header of the compress algorithm and it turned out the <code>zstd</code> compress algorithm 
(with the header starts with <code>28 B5 2F FD</code>).
![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/1c616e4e-29a0-4c1e-95ca-3239b78fcc94)
- So I used <code>pngsplit</code> to get the IDAT chunk and remove the chunk's length, name and checksum and only left with the compressed data.
- Then used this script to decompress the zstd data

```
import zstd
import binascii 

raw = open('D:\Download\png_parts\\test','rb').read()
data = zstd.decompress(raw)
data=binascii.hexlify(data).decode()

f = open('D:\Download\png_parts\\zsztd_decompressed_data','w')
f.write(data)
```

- Now compress with <code>zlib</code> with this linux command <code>zlib-flate -compress < zsztd_decompressed_data > compressed_zlib</code>
- Then put it in the original IDAT chunk and correct the length as well as the checksum. At here, we cannot see the flag because the question mentions something about half of the size. 
  Since this image is <code>800x800</code> so the new size is <code>1600x1600</code>. Correct the IHDR checksum as well and get the flag
  
  ![image](https://github.com/M1nh-Duk/Writeups/assets/100038173/4d1059f4-f4bc-4036-8cda-a205bc99d09e)

  
