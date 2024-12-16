
# BackTrack

#### *Kenji is a nice guy who lives in Tokyo. He is in a dilemma. In 2017, he was late to an important meeting and is now facing repercussions. To defend himself, he needs to prove that it was not his fault. His evidence? The train he boarded that day, traveling between Omotesando and Suitengumae, was delayed. However, his boss is not providing the specific details of the accusation. Kenji vividly remembers one key fact: the train was around 61 minutes late. Flag Format: nite{time_date}, Example: nite{13:00_3January} Help him uncover the exact date of the incident and the start time of the delay. Justice for Kenji!*

**Category: Miscellaneous**

- I opened Google Maps, and searched the route for *Omotesando* to *Suitengumae* and found that it was the Hanzomon/Purple Line.
- I searched for Hanzomon delays and found their website that listed all delays of the past 35 days. 
- To get this data for 2017, I used Wayback Machine and found the snapshot that showed that there was a 61+ minutes delay on 20th February at 17:00. 

### Flag: `nite{17:00_20February}`

**Resources:**
- https://www.tokyometro.jp/lang_en/delay/history/hanzomon.html
- https://web.archive.org/web/20170525200358/http://www.tokyometro.jp/lang_en/delay/history/hanzomon.html

****
# Beyond A Display

#### *I took a metro from this location and I saw a shopping complex in the vicinity. I remembered that I saw a multidimensional billboard from a company over there. The same company held a concert on 26th October 2024, and a group performed there. However, I have forgotten what the information really was. Can you help me? Flag format: nite{Billboard_Company,Group_Name,Venue_Of_The_Performance}*

**Category: Miscellaneous**

![beyond_a_plane.png](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/beyond_a_plane.png?raw=true)
- I identified the image attached as being taken from outside the *Belvedere Towers* metro station in Gurgaon off clues like the word Towers being cut-off and Hindi on the sign on the right.
- I explored this area on Google Maps and found that the *DLF Cyber Hub* nearby was the shopping complex being referred to.
- I googled `3d billboard in gurgaon` and saw one of Vivo, but Hyundai turned out to be the company in question.
- I searched for `hyundai concert` which showed a list of Hyundai Spotlight concerts of the year & one of them was *Shankar Ehsaan Loy* at *KTPO, Bengaluru* on *October 26th, 2024*.

### Flag: `nite{Hyundai,Shankar_Ehsaan_Loy,KTPO}`

**Resources:**
- https://www.instagram.com/wysiwyg_events/p/Cf1kuQGJKH5
- https://hyundaispotlight.in/

****
# La Casa de Papel
#### *Word on the street is Bob's about to make a big withdrawal. Too bad you're the one holding his ID. Can you charm Alice into making the transfer before she catches on?* 

**Category: Cryptography**

- In this challenge, I had to fool Alice into thinking I was Bob, so the message I sent to be encrypted was 'Bob' in option 1.
```bash
 _             ____                      _        ____                  _
| |    __ _   / ___|__ _ ___  __ _    __| | ___  |  _ \ __ _ _ __   ___| |
| |   / _` | | |   / _` / __|/ _` |  / _` |/ _ \ | |_) / _` | '_ \ / _ \ |
| |__| (_| | | |__| (_| \__ \ (_| | | (_| |  __/ |  __/ (_| | |_) |  __/ |
|_____\__,_|  \____\__,_|___/\__,_|  \__,_|\___| |_|   \__,_| .__/ \___|_|
                                                            |_|


1. Practice Convo
2. Let's Fool Alice!
3. Crack the Vault
4. Exit
Choose an option: 1
Send a message: Bob
Here is your encrypted message: YjRlMGE4MDI0MjhjYjM1ZjY5YzBlOTUyZDk2MTcyZDY=
```
- I converted this string from base64, and got the hash `b4e0a802428cb35f69c0e952d96172d6` (HMAC) for option 2.
```bash
1. Practice Convo
2. Let's Fool Alice!
3. Crack the Vault
4. Exit
Choose an option: 2

Bot: Okay, let's see if you're the real deal. What's your name?
Your name: Bob

Bot: Please provide your HMAC
Your HMAC: b4e0a802428cb35f69c0e952d96172d6

Alice: Oh hey Bob! Here is the vault code you wanted:
G0t_Th3_G0ld_B3rl1nale
```
- This is the password required for the vault for option 3.
```bash
1. Practice Convo
2. Let's Fool Alice!
3. Crack the Vault
4. Exit
Choose an option: 3

Vault Person: Enter password
Password: G0t_Th3_G0ld_B3rl1nale

Vault Unlocked! The flag is: nite{El_Pr0f3_0f_Prec1s10n_Pl4ns}

1. Practice Convo
2. Let's Fool Alice!
3. Crack the Vault
4. Exit
```

### Flag: `nite{El_Pr0f3_0f_Prec1s10n_Pl4ns}`

****
# freakada 3301

**Category: Miscellaneous**

![freakada_3301_message.PNG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freakada_3301_message.png?raw=true)
- The image given seems to be inspired by *Cicada 3301*. To find the hidden message, I uploaded it on *Aperi'Solve* and found a ciphertext in the Strings: `ZIT HQZI OL GWLEXKTR, WXZ ZIT ZKXZI SOTL OF ZIT LIQRGVL. LTTA ZIT HQZZTKFL. QDGFU ZIT EIQGL, Q WTQEGF QVQOZL: izzhl://woz.sn/yktqatlztof0. GFSN ZIT VGKZIN VOSS LTT ZIT XFLTTF. ZIT PGXKFTN IQL PXLZ WTUXF`. This is mono-alphabetic substitution which decodes to:
  `THE PATH IS OBSCURED, BUT THE TRUTH LIES IN THE SHADOWS. SEEK THE PATTERNS. AMONG THE CHAOS, A BEACON AWAITS: HTTPS://BIT.LY/FREAKESTEIN0. ONLY THE WORTHY WILL SEE THE UNSEEN. THE JOURNEY HAS JUST BEGUN`. 
- On opening `bit.ly/freakestein0`, I got another image `ducky.jpg` which I again thought had to be extracted and so uploaded it onto *Aperi'Solve*. I extracted the files using *binwalk* and they all pointed to the GitHub link: `github.com/freakada-3301`.
- The `Salvation-in-Decay` repository had 3 files: `README.md`, `Code of decay` & `Whispers of the forgotten`. README contained `1sk3vr3d_qw5yvvc}` which was the second part of the flag and was encoded with a cipher, I saved it for later. The other two files had text encoded in Alien cipher which translated to `SOMEHOW FORGOTTEN` & `WE WERE HERE`. These were hints for the next step.
- I opened the commit history of these other two files in the repository and found the following:
![freak1.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freak1.JPG?raw=true)
![freak2.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freak2.JPG?raw=true)
![freak3.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freak3.JPG?raw=true)
- The numbers represent line : word : character of the poem and on doing that, I get `httpsdiscordggAHj7R2Qd` which when tweaked to fit the format, is an invite link to the freakada-3301 Discord server. 
- Apart from a voice channel that played a song (worse than rick-roll) on loop, there was a Discord bot asking for its *prime*. This was 3301. It then asked for the result of `3301*x*y` where x and y were integral parts of the original image (dimensions 449x503), which was 745520947. 
- After sending that, the bot gave 2 values `13.34508015959565, 74.79629600750295` that could only mean coordinates. This was one of the photos under the reviews of the location.

![freak4.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freak4.JPG?raw=true)
- The QR code led to a WAV file and so I opened it in Audacity in Spectrogram view.
![freak5.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/freak5.JPG?raw=true)
- So, `nite{4_wannabe_` is the first part of the flag. But we still had to decipher the second part. 
- Under the first part of the flag in the WAV file in Audacity, is beeps for Morse code. This decoded to `FREEKEY`. This seemed to be the key to a cipher and my best bet was the _Vigenère_ cipher. So, the second half turned out to be `1nt3rn3t_my5tery}`.

### Flag: `nite{4_wannabe_1nt3rn3t_my5tery}`

****
# BuckSpeak

#### *Buckbeak is trying to say something deep but is frustrated as nobody bücking understands him. Can you help him out?*

**Category: Forensics**

- The challenge begins with a 1m 16s long *WAV* file. I opened it in *Audacity* with Spectrogram view to check for any patterns. All I noticed was music notes and my intuition was to transcribe those. 
- I also tried opening the file in *DeepSound* and it asked for the password, so I had to find that.
- I searched for `Bücking music cipher`, and found a website to encrypt letters into the said cipher. I saw the sheet of music notes that corresponded to alphabets and started putting in the alphabets according to what I heard in the WAV file. 
- This was a lengthy process and after multiple checks by comparing the .midi I got from the website to the given file in Audacity, I ended up with the string `usephrasetruefansreadthebookstohearsomethingdeep`.
![buck1.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/buck1.JPG?raw=true)
![buck2.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/buck2.JPG?raw=true)
- I put `truefansreadthebooks` as the password for the file in DeepSound. This let me extract 2 secret files - `disclaimer.txt` and `screech.mkv`. 
![buck3.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/buck3.JPG?raw=true)
- Now, `screech.mkv` was just a 9 second clip from Harry Potter, but Matroska video files can store a lot of content. I searched for tools for mkv file forensics and installed `mkvtoolnix`.
- I searched for the possible content in the file using `mkvinfo screech.mkv` and got this:
```bash
+ EBML head
|+ EBML version: 1
|+ EBML read version: 1
|+ Maximum EBML ID length: 4
|+ Maximum EBML size length: 8
|+ Document type: matroska
|+ Document type version: 4
|+ Document type read version: 2
+ Segment: size 1302091
|+ Seek head (subentries will be skipped)
|+ EBML void: size 66
|+ Segment information
| + Timestamp scale: 1000000
| + Multiplexing application: Lavf58.76.100
| + Writing application: Lavf58.76.100
| + Segment UID: 0xeb 0xa7 0x96 0xbd 0x3e 0xca 0x21 0xe5 0xa5 0x38 0x5a 0xe7 0xe2 0xb7 0x29 0xe2
| + Duration: 00:00:08.912000000
|+ Tracks
| + Track
|  + Track number: 1 (track ID for mkvmerge & mkvextract: 0)
|  + Track UID: 8614043760464067728
|  + "Lacing" flag: 0
|  + Language: und
|  + Codec ID: V_MPEG4/ISO/AVC
|  + Track type: video
|  + Default duration: 00:00:00.033333333 (30.000 frames/fields per second for a video track)
|  + Video track
|   + Pixel width: 640
|   + Pixel height: 360
|   + Interlaced: 2
|   + Display unit: 4
|   + Video color information
|    + Color transfer: 6
|    + Color matrix coefficients: 6
|    + Color primaries: 5
|    + Color range: 1
|    + Horizontal chroma siting: 1
|    + Vertical chroma siting: 2
|  + Codec's private data: size 50 (H.264 profile: High @L3.0)
| + Track
|  + Track number: 2 (track ID for mkvmerge & mkvextract: 1)
|  + Track UID: 1472920706463544447
|  + "Lacing" flag: 0
|  + Language: eng
|  + Codec ID: A_AAC
|  + Track type: audio
|  + Audio track
|   + Channels: 2
|   + Sampling frequency: 44100
|   + Bit depth: 32
|  + Codec's private data: size 2
| + Track
|  + Track number: 3 (track ID for mkvmerge & mkvextract: 2)
|  + Track UID: 6103239035697966766
|  + "Lacing" flag: 0
|  + Language: und
|  + Codec ID: S_TEXT/ASS
|  + Track type: subtitles
|  + Codec's private data: size 939
|+ Attachments
| + Attached
|  + File name: Buckbeak.otf
|  + MIME type: application/x-truetype-font
|  + File data: size 109032
|  + File UID: 17636095151199042832
| + Attached
|  + File name: Mechanical-g5Y5.otf
|  + MIME type: application/x-truetype-font
|  + File data: size 112136
|  + File UID: 4317686372283026958
|+ Tags
| + Tag
|  + Targets
|  + Simple
|   + Name: COMPATIBLE_BRANDS
|   + String: 3gp43gp53g2a
|  + Simple
|   + Name: MAJOR_BRAND
|   + String: 3gp4
|  + Simple
|   + Name: MINOR_VERSION
|   + String: 512
|  + Simple
|   + Name: ENCODER
|   + String: Lavf58.76.100
| + Tag
|  + Targets
|   + Track UID: 8614043760464067728
|  + Simple
|   + Name: ENCODER
|   + String: Lavc60.3.100 libx264
|  + Simple
|   + Name: DURATION
|   + String: 00:00:08.912000000
| + Tag
|  + Targets
|   + Track UID: 1472920706463544447
|  + Simple
|   + Name: HANDLER_NAME
|   + String: soun
|  + Simple
|   + Name: VENDOR_ID
|   + String: [0][0][0][0]
|  + Simple
|   + Name: ENCODER
|   + String: Lavc60.3.100 libfdk_aac
|  + Simple
|   + Name: DURATION
|   + String: 00:00:08.892000000
| + Tag
|  + Targets
|   + Track UID: 6103239035697966766
|  + Simple
|   + Name: ENCODER
|   + String: Lavc58.134.100 ass
|  + Simple
|   + Name: DURATION
|   + String: 00:00:08.890000000
|+ Cluster
```
- The main contents to be extracted here were the attachments and the tracks. I exported track 3 into a .txt file since it said subtitles using `mkvextract screech.mkv tracks 2:./track.txt`. The important content in the file, which was the subtitle, was: `UnderstaNDAblE Buckbēaĸ SCRéècHiɳg-ɲoǐşēЅz`
- I extracted the attachments using the command `mkvextract screech.mkv attachments 1:./buckbeat.otf 2:./mechanical.otf`. Mechanical was a normal typeface but Buckbeak was altered. 
![buck4.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/buck4.JPG?raw=true)
- So, I installed the Buckbeak font into my system, opened a Word file, and I copy pasted the subtitle with this font.
![buck5.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/niteCTF24/files/buck5.JPG?raw=true)
This had to be tweaked a bit to get the correct flag.

### Flag: `nite{w3_b0th_kn0w_wh0_i5_ug1y_h3r3_ma1f0y}`

**Resources:**
- https://legacy.wmich.edu/mus-theo/ciphers/bucking.html
- https://ctftime.org/writeup/10507
- https://mkvtoolnix.download/doc/mkvextract.html
