# I am Optimus Prime

The description, and title, of the challenge hinted that it had something to do with robots, and so I found that there's a file called robots.txt that can be accessed by adding `/robots.txt` to the url. This conveyed that the flag would be hidden on `/hiddenFlag`. I then sent a request for the PATCH method, which said I was on the right path, but it also seemed to work with OPTIONS & PUT. But when I ran the request once again, it gave me the flag. 

**OASIS{r0b0t5_4nd_m37h0d5_4r3_pr3tty_c00l!}**

# Comma Separated … Virus?

The CSV file in the challenge seemed to contain a few columns of random names of cats, random floating points under the SCORE & TUNE column, and also a few letters & numbers which seemed to be a part of the flag in the last column. I figured I'd have to sort the file in a certain way. After a few trial and errors, I sorted just the "TUNE" column, and the flag was formed in the last column.

**OASIS{TROJAN}**

# All that for a drop of blud

First, a custom User-Agent named OASISPlayer had to be added as the website's first page hinted. Then I had to send a POST request on /game, and with a parameter name that was the Cryptonite. So I added `/game?name=Cryptonite` while sending the request, and it asked for the rank of the project on CTFTime, which was 4 nationally, to `/givemetheFlag`. So I finally sent the POST request with `/givemetheFlag?name=Cryptonite&rank=4`.

**OASIS{G37_d035_n07_4lw4y5_G37_th1ng5}**

# Stairway to Heaven

The given game file was executable and only resulted in a bunch of color blocks that looked like pixels. I copied these and pasted it on a Google Doc as text. I then searched through the text for 'flag' and found a few numbers next to the word in the file, which were ASCII, and then decoded it for the flag.

**OASIS{v34y_f4ncy_AN5I}**

# Git Gud

After extracting the zip file and opening a file in the logs folder, I noticed individual characters that made up the flag, at the end of each line of the content. 

**OASIS{g3t_gu663r_4t_g!t!!}**

# Quence your thirst

The ciphertext seemed to be a direct alphabet substitution cipher after noticing DLLWB:// at the end that resembled HTTPS://. I decoded the rest and  of the alphabets & was left with 4 alphabets - y q z j, that could be used at 4 positions in the link after decoding it. I permuted & tried every combination and eventually figured out the one that worked. 

**OASIS{fr3qu3nt_j4!l_br34k1ng_m4k3s_!t_t00_3asy_fr}**

# Not Noice

Uploading the audio in Audacity and viewing it in spectogram view or using a Morse audio decoder displayed the flag.

**OASIS{5P3CT0GR4M_15_TH3_C00L35T}**

# Maze Runner

A reverse search of the image results in a Wikipedia page for the place that gave the information needed - Location & Surname of the Ideator.

**OASIS{Borges_Fontanellato}**

# Microsoft StrongEdge

In the given .pptx file, I noticed an image, minimized at the corner of the first slide. It was in ROT13 encryption and gave the flag upon decoding. 

**OASIS{r0t4t0r_0f_pp75}**

# Knock Knock

This was an image of an obscured QR code that could be cleared by using MSPaint or adjusted with other photo editing software.

**OASIS{qu3u3r_r3c0v3r3r}**