# Redirecting-output

`>` is used to redirect output of the first argument into the second, here it was to redirect `PWN` to `COLLEGE` and so I ran `echo PWN>COLLEGE`.

Flag: **pwn.college{U5ivIcI9D2zqWj0zsvyZtWledMF.dRjN1QDL3YTO0czW}**

# Redirecting-more-output

Apart from using `echo` to redirect output, the output of a command can directly by redirected too. In this challenge, the output of `/challenge/run` had to be redirected to `myflag`, and so I ran `/challenge/run > myflag`, and then `cat myflag`, as the output was now in the `myflag` file.

Flag: **pwn.college{Uq2w0YnDXpH0Dc8MQMuA_8lT1ms.dVjN1QDL3YTO0czW}**

# Appending-output

`>>` redirects output in *append* mode while `>` *truncates*, as in it creates a new output file and deletes the old one, but `>>` adds on output to the same file. For this challenge, I had to redirect the output of `/challenge/run` to `/home/hacker/not-the-flag` in append mode, else it gets overwritten. So I ran `/challenge/run >> /home/hacker/not-the-flag` and `cat /home/hacker/not-the-flag` to get the flag. 

Flag: **pwn.college{0zWevbs0xypbNZWCN4D8IvKetAf.ddDM5QDL3YTO0czW}**

# Redirecting-errors

A *File Descriptor (FD)* number describes a communication channel in Linux. 0 is for *standard input*, 1 for *standard output* & 2 for *errors*. `>` is by default the same as `1>`. In this challenge, I had to redirect the standard output to the `myflag` file and errors to the `instructions` file, so I ran `/challenge/run > myflag 2> instructions`, and `cat myflag` to read the flag.

Flag: **pwn.college{0kzyvoW4WAZsjKZxacymLrEZH7T.ddjN1QDL3YTO0czW}**

# Redirecting-input

Input can be redirected using `<`. In this challenge, I had to redirect the output of `COLLEGE` to `PWN` using `echo COLLEGE > PWN`, and then input of `PWN` to `/challenge/run` using `/challenge/run < PWN`, which gave the flag.

Flag: **pwn.college{oGUGAXcThlrGItUd04miCsLuTFV.dBzN1QDL3YTO0czW}**

# Grepping-stored-results

For this challenge, I had to go back to my knowledge of `grep`. Firstly, I redirected output with `/challenge/run > /tmp/data.txt`, and then `grep pwn.college /tmp/data.txt` to find the flag.

Flag: **pwn.college{wcUlxPiMWN-BRVQqnwuPElMeR1t.dhTM4QDL3YTO0czW}**

# Grepping-live-output

The *pipe operator* (`|`) is used to connect standard output and input and skip the need to store it in a file. In this challenge, I had to *grep* through the output of the `/challenge/run` command using `|` and so I did `/challenge/run pwn.college | grep pwn.college`.

Flag: **pwn.college{89ZuN9kHgUmH5t6iG7epCvGZ1vW.dlTM4QDL3YTO0czW}**

# Grepping-errors

`>&`operator links a *file descriptor* to another one. Here, I had to redirect standard error to standard output and then pipe them with the grep command to find the flag. So I ran `/challenge/run 2>&1 | grep pwn.college`.

Flag: **pwn.college{kE0XsgtdAa0Ow8C7OQvMJuYocs2.dVDM5QDL3YTO0czW}**

# Duplicating-piped-data-with-tee

The `tee` command duplicates data in pipes to other files provided as arguments. This challenge first required me to check the contents of `pwn` for what is needed and so I did `cat pwn` and got the secret code. Then I piped `/challenge/pwn` to `/challenge/college` with the secret code as: `/challenge/pwn --secret YL2AygY7 | /challenge/college`.

Flag: **pwn.college{YL2AygY7awLHqmQ0A696yE3rueY.dFjM5QDL3YTO0czW}**

# Writing-to-multiple-programs

`>()` runs the command inside, reads the standard input, and writes to output. In this challenge, I had to duplicate the output of `/challenge/hack` to `/challenge/the` & `/challenge/planet` using `/challenge/hack | tee >(/challenge/the) >(/challenge/planet)`.

Flag: **pwn.college{g7ym2mT4UxXKOz1Q5ODYR4hZ4yd.dBDO0UDL3YTO0czW}**

# Split-piping-stderr-and-stdout

In this challenge, I had to redirect `/challenge/hack`'s errors to `/challenge/the` & standard output to `/challenge/planet/` using `>()`, `>` & `|`. So, I ran `/challenge/hack > >(/challenge/planet) 2> >(/challenge/the)`.

Flag: **pwn.college{02jRYnNVKhk10PtKCOypPwaLw0B.dFDNwYDL3YTO0czW}**
