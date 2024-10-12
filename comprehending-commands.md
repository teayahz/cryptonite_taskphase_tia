# cat-not-the-pet-but-the-command!

`cat` is used to read out files and can also con*cat*enate and read out multiple files. For this challenge, the flag was a file in the home directory and simply could be read out with `cat flag`.

Flag: **pwn.college{0WBLg10oKrKeCoYMmEEQAPUwTgb.dFzN1QDL3YTO0czW}**

# catting-absolute-paths

`cat` also takes absolute paths of files as arguments, and so the flag this time could be obtained with `cat /flag`.

Flag: **pwn.college{0fp794YCgmqvocCDajp4Gg671JD.dlTM5QDL3YTO0czW}**

# more-catting-practice

For this challenge, `cd` could not be used but the flag file could still be read by using its absolute path, which was provided, and so I ran `cat /lib/terminfo/t/flag`

Flag: **pwn.college{4IVzm3RmrmVd3mQo13PxV3XBTzq.dBjM5QDL3YTO0czW}**

# grepping-for-a-needle-in-a-haystack

`grep` is a command used to search for content in files. The flag was hidden in `/challenge/data.txt` and since flags start with the line *pwn.college*, I executed `grep pwn.college /challenge/data.txt` and obtained the flag.

Flag: **pwn.college{AkGI_UYGy-khtusee34s3HSQEVN.ddTM4QDL3YTO0czW}**

# listing-files

`ls` is a command used to list all files in the directories provided, or in the current one. By listing files under `/challenge`, I found that the *run* file was renamed to *7638-renamed-run-20789*, and so I `/challenge/7638-renamed-run-20789` to get the flag.

Flag: **pwn.college{QuiGnetNR6NNQc4kny5JYYl9hBC.dhjM4QDL3YTO0czW}**

# touching-files

The 'touch' command is used to create a new file. To clear this challenge I had to create the files `/tmp/pwn` and `/tmp/challenge` and then run `/challenge/run`.

Flag: **pwn.college{sFj9wo0UMj9kYtg2Se0VZt7L02X.dBzM4QDL3YTO0czW}**

# removing-files

The `rm` command is used to remove files. For this challenge, I had to remove the 'delete_me' file by using `rm delete_me`, and then run '/challenge/check' to obtain the flag. 

Flag: **pwn.college{U3KnMRGGPIeX80jgoz060Je1Pth.dZTOwUDL3YTO0czW}**

# hidden-files

The `ls -a` command can be used to show up files starting with a *.* that were hidden automatically. The flag here was hidden in the / directory so I had to do `cd /` and then `ls -a` to find a file named `.flag-20471261975398`. I did `cat .flag-20471261975398` to read out the file & find the flag.

Flag: **pwn.college{gYoZXC7sQIjE_5lk5VKWlPHfph5.dBTN4QDL3YTO0czW}**

# An-Epic-Filesystem-Quest

By using my knowledge of the commands, `cd`, `ls` & `cat`, I had to start from `cd /` & navigate through a bunch of directories, some which I couldn't use `cd` for directly but instead `ls <absolute path>`, and some on which I had to use `ls -a` to find the hidden clues and the paths to them, and `cat` to read them all out.

Flag: **pwn.college{8p_TAX5P214H_D7k0x2TlKIV1nk.dljM4QDL3YTO0czW}**

# making-directories

`mkdir` is used to make directories. In this challenge, I had to create a `/tmp/pwn` directory and a file named `college` in it. So I ran `mkdir /tmp/pwn`, then `cd /tmp/pwn`, and then `touch college`, and finally `/challenge/run`.

Flag: **pwn.college{4YpY65_rjHg3fvyOMj6JlWGuL26.dFzM4QDL3YTO0czW}**

# finding-files

`find` is used to search for files or directories with a name in the current working directory. Depending on the arguments entered, it can search for the file location, or the name of the file & in the entire filesystem too by entering `find / -name [search_query]`. For this, I had to find the flag file in the filesystem, so I ran `find / -name flag`, where a lot of files popped up. I tried `cat` for each of them and found the flag in a certain file.

Flag: **pwn.college{ERzIdBDkwJYsJ--Hg_pEPIyjIDi.dJzM4QDL3YTO0czW}**

# linking-files

*Symbolic links* link to the original file name and access contents of that file, and are created with the `ls` command along with the argument `a`. In this challenge, running `/challenge/catflag` reads out `/home/hacker/not-the-flag`, so I deleted `/home/hacker/not-the-flag` with `rm ~/not-the-flag`, & then created a symbolic link: `ln -s /flag ~/not-the-flag`, and then did `/challenge/catflag` to finally obtain the flag.

Flag: **pwn.college{YxieWttL4OeQPC9F3aNhKCTXpUT.dlTM1UDL3YTO0czW}**