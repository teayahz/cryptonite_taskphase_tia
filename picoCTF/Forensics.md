# Trivial Flag Transfer Protocol

**Flag:** `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`

**Solution:** 
- The given file was a *PCAPNG* file, and on looking that up, I installed *Wireshark* to view the contents in the file.
- I exported the *TFTP* (Trivial File Transfer Protocol) objects of the given file by opening it on Wireshark and going to File -> Export Objects.

![tftp1.jpg](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tftp1.JPG?raw=true)

- I opened the files `instructions.txt` and `plan` and found the following strings of letters which seemed to be a cipher - ROT13 to be precise.
```
instructions.txt: GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA

plan: VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
```
 
- On decoding both: 
```
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN

IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
```

- Here, it's implied that the program in `program.deb` file has to be installed and the code `DUEDILIGENCE` is used to view the data in the bitmap files.
- I ran `sudo apt-get install ./program.deb` which installed *Steghide*, a common tool used in steganography.
- I then used the `steghide` command with each of the 3 `.bmp` files, with `steghide extract -sf ./picture1.bmp`. It asked for a passphrase and here I entered `DUEDILIGENCE`. This resulted:
```
steghide: could not extract any data with that passphrase!
```
This could also be done with `steghide extract -sf ./picture1.bmp -p "DUEDILIGENCE"`.
- I ran the same command with the second image and got the same output. But with the third picture I got the following output:
```
wrote extracted data to "flag.txt".
```
- I then ran `cat flag.txt` to read the flag.

**Concepts learnt:**
1. Pcap files & TFTP
2. The use of Wireshark
3. Steghide

**Mistakes & other approaches:** 
- Steghide didn't initially install properly by running the program file, so I did the installation outside of it.
- For the cipher, I first tried Caesar cipher and it worked for the number 13 - which is essentially ROT13.

**Resources:**
- https://manpages.ubuntu.com/manpages/bionic/man1/steghide.1.html
- https://cryptii.com/

# tunn3l v1s10n

**Flag:** `picoCTF{qu1t3_a_v13w_2020}`

**Solution:**
- I first opened the file given on a hex editor and noticed the first few characters - `42 4D` that stood for BM which represents a *bitmap file*.

  ![tunnelhex1](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunnelhex1.png?raw=true)

- A few changes had to be made so that this file could be viewed, and so I looked up the header format for bitmap files, and noticed a mismatch with a few characters at the end of line 1, `BA D0`, & I changed them and saved it with .*bmp* and got this image.

![tunnelhex2](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunnelhex2.png?raw=true)  ![tunn3l_v1s10n_1.bmp](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunn3l_v1s10n_1.bmp?raw=true)
  This says `notaflag{sorry}` and appears to be a part of the image, and so more had to be edited in the hex.

- I noticed that height was represented with `32 01` and changed it to `32 03`, and got the flag from the top right corner, but the image was still coloured and cropped incorrectly.

![tunnelhex3](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunnelhex3.png?raw=true) ![tunn3l_v1s10n.bmp](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunn3l_v1s10n.bmp?raw=true)

Out of curiosity, to obtain a clearer image, I made the following changes: 
 -  I changed the values at the end of the first line to `36 00 00 00 | 28 00` by looking at an example of a bitmap header. 
 -  The values at `32 01 00 00` (306 px, found through a decimal to hex converter) in the original file are used to change the height whereas `6E 04` is the width (1134 px), and this could be increased massively by changing `01` to `03`. 
 - So, `32 03` changed the height to 818 px, but the flag was still slightly cropped out. 
 - I changed `32` to `40` and this fit the flag in the image and the final resolution of the image is 1134 x 832.

  ![tunnelhex4](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunnelhex4.png?raw=true) ![tunn3l_v1s10n_new.bmp](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/tunn3l_v1s10n_new.bmp?raw=true)


**Concepts learnt:**
1. The bitmap .bmp file format
2. The header format for .bmp files
3. Conversion of decimal to hex and its use in changing the header of the file
4. A little about little endian format of storing as .bmp files use it and that's the format of hex

**Mistakes & other approaches:**
- While changing some values such as the offset and dimensions directly, some didn't work as the hex value entered didn't correspond to a decimal value, and the .bmp file didn't open.
- Before changing the offset to `36`, I tried other options to fit the crop of the image perfectly - like `BA D0` to `BA F0` which almost did it, but some values changed the colouring of the image itself, and some didn't work as other values in the header had to be changed along with it.

**Resources:**
- https://en.wikipedia.org/wiki/BMP_file_format#Example_1
- https://www.rapidtables.com/convert/number/decimal-to-hex.html
- https://hexed.it/

# m00nwalk

**Flag:** `picoCTF{beep_boop_im_in_space}`

**Solution:**
- The challenge gave a WAV file. I put it through Audacity on spectrogram view, and found out that the pattern of the beats represented that of *SSTV*'s.
-  To analyse this file, installed the tool called *RX-SSTV* after searching for tools to decode SSTV.
- I played the audio from my media player and simultaneously recorded it on RX-SSTV, using the RX option of Scottie 1 as a hint stated "*What is the CMU mascot?, that might help select a RX option*" \[Scotty].
This led to the formation of pixels from the beats of the audio which led to this final image containing the flag.

  ![m00nwalk1.jpg](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/m00nwalk1.jpg?raw=true)

**Concepts learnt:**
1. SSTV (Slow-scan television) which is used to transmit images over radio waves.

**Mistakes & other approaches:**
- I tried a few other tools for decoding the audio file such as *qsstv* but I struggled with linking & recording the audio.

**Resources:**
- https://www.qsl.net/on6mu/rxsstv.htm

# Blast from the Past

**Flag:** `picoCTF{71m3_7r4v311ng_p1c7ur3_12e0c36b}`

**Solution:**
- The initial image was an ordinary photo of a wall with a painting. 
- Using exiftool with the command `exiftool -G1 -a -s original.jpg1`, metadata can be viewed including the timestamps which need to be changed to `1970:01:01 00:00:00.001+00:00`.
- This could be done by either editing the hex data to these values or using exiftool commands. 
- First, I used the hex editor to modify CreateDate, ModifyDate & DateTimeOriginal individually but it could be done with `exiftool -AllDates='1970:01:01 00:00:00.001' original_modified.jpg`. The output after connecting to the checker program was: 
```bash
MD5 of your picture:
c6503c2f4872c83ced315f795068cfb3  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.703
Oops! That tag isn't right. Please try again.
```
- SubSec records fractions of seconds and the subsec values could also be changed with `exiftool -SubSecCreateDate='1970:01:01 00:00:00.001' -SubSecDateTimeOriginal='1970:01:01 00:00:00.001' -SubSecModifyDate='1970:01:01 00:00:00.001' original_modified.jpg`. This was just changing the original `703` subsec to `001`.
```bash
MD5 of your picture:
e93c590c522cddc22aa5364bfc44cc70  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 7/7
Timezones do not have to match, as long as it's the equivalent time.
Looking at Samsung: TimeStamp
Looking for '1970:01:01 00:00:00.001+00:00'
Found: 2023:11:20 20:46:21.420+00:00
Oops! That tag isn't right. Please try again.
```
- The last task was to edit the TimeStamp. With the command `exiftool -time:all -v3 original.jpg`, I noticed that the Samsung tags were towards the end of hex data and was originally `Image_UTC_Data1700513181]`. The numbers are time in Unix timestamp format which is widely used in computing. 
- I used a website to convert this to `1970:01:01 00:00:00.001` and found it's just `0`, but for the format it's `0000000001` as there's 1 subsec. I edited this with the hex editor and put it again through the checker program to get the flag: 
```bash
MD5 of your picture:
29b424e2e78cd7d66fa69901a43434a6  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 7/7
Timezones do not have to match, as long as it's the equivalent time.
Looking at Samsung: TimeStamp
Looking for '1970:01:01 00:00:00.001+00:00'
Found: 1970:01:01 00:00:00.001+00:00
Great job, you got that one!

You did it!
picoCTF{71m3_7r4v311ng_p1c7ur3_12e0c36b}
```

**Concepts learnt:**
1. Editing and viewing data through ExifTool
2. Epoch unix timestamps

**Mistakes & other approaches:**
- Initially, I wasn't aware ExifTool could be used to edit metadata so I did it in the hex editor individually

**Resources:**
- https://hexed.it/
- https://www.epochconverter.com/
- https://stackoverflow.com/questions/78185037/how-to-edit-the-samsung-trailer-tag-timestamp

# endianness-v2

**Flag:** `picoCTF{cert!f1Ed_iNd!4n_s0rrY_3nDian_b039bc14}`

**Solution:**
- I opened `challengefile` in a hex editor and observed that the header was for a JPEG file, but the bytes weren't in the right order.

![endian1.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/endian1.JPG?raw=true)

- Here, every four bites had been reversed as the file is in little-endian & had to be converted to big-endian.
- I made a Python program to do this where it first read the file's binary data, reversed every 4 bytes and put it into a new file that is saved as JPEG.
```python
def fix_binary_endianness(input_file, output_file):
    with open(input_file, 'rb') as f:
        data = f.read()
    
    fixed_data = bytearray()
    for i in range(0, len(data), 4):
        chunk = data[i:i+4]
        fixed_data.extend(chunk[::-1])  
    
    with open(output_file, 'wb') as f:
        f.write(fixed_data)

input_file = '/mnt/c/users/admin/downloads/challengefile'
output_file = '/mnt/c/users/admin/downloads/out.jpeg'
fix_binary_endianness(input_file, output_file)

print("File processing complete. Fixed file saved as:", output_file)
```
- I ran this through my terminal and got the flag as an image.

![endian2.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/picoCTF/images/out.jpeg?raw=true)

**Concepts learnt:**
1. Little-endian and big-endian way of storing bytes

**Resources:**
- https://hexed.it/

# Eavesdrop

**Flag:** `picoCTF{nc_73115_411_dd54ab67}`

**Solution:**
- The given PCAP file can be opened on Wireshark. I followed one of the TCP streams and found the following conversation:
```
Hey, how do you decrypt this file again?

You're serious?

Yeah, I'm serious

*sigh* openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123

Ok, great, thanks.

Let's use Discord next time, it's more secure.

C'mon, no one knows we use this program like this!

Whatever.

Hey.

Yeah?

Could you transfer the file to me again?

Oh great. Ok, over 9002?

Yeah, listening.

Sent it

Got it.

You're unbelievable
```

- There seemed to be `file.des3` that's required to find the secret. Now the port 9002 could be filtered using `tcp.port == 9002`. 
- One of the packets had a string starting with `Salted` which was 48 byte hex data being transferred: `53616c7465645f5f0c160de825c4925b6543fa6c52dc91b4487b8252966d9de6aec8508b95522f879232bf89e3066440`. 
- I saved this as `data.txt` and then ran the command `xxd -r -p data.txt file.des3` to form the binary file.
- Now, I had the required file and ran the command `openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123`. The flag was now in `file.txt`.

**Concepts learnt:**
1. Following streams and filtering in Wireshark
2. The `xxd` tool that is used to convert binary files, but here making the hexadecimal dump into a raw binary file using `-r`.

**Mistakes & other approaches:**
- I tried saving the `Salted` string itself as the file but the data didn't match and it was better to convert from hex.

**Resources:**
- https://linux.die.net/man/1/xxd
