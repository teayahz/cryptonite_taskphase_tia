# Trivial Flag Transfer Protocol


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
