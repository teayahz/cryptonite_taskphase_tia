# Chaining-with-Semicolons

`;` is used to separate commands while running them in a single line together, it chains the commands. To run `/challenge/pwn` & `/challenge/college` together in one line, I ran `/challenge/pwn; /challenge/college`.

Flag: **pwn.college{wDeWrxJoAT9raaGHK2wKHKTHoKy.dVTN4QDL3YTO0czW}**

# Your-First-Shell-Script

*Shell scripts* can be created by creating a file with a `.sh` suffix and can be run with the `bash` command. They can contain many commands and can be executed all at once. To get the flag, I had to create a shell script named `x.sh` that contained the output of both `/challenge/pwn` & `/challenge/college`. So I ran `echo "/challenge/pwn;/challenge/college>x.sh` and then `bash x.sh`.

Flag: **pwn.college{EUti9EYz0pQEV6z9I0g2LYC_AZV.dFzN4QDL3YTO0czW}**

# Redirecting-Script-Ouput

Scripts can be used as commands, and its output or input can be redirected and piped out. In this challenge, I had to create a shell script using `touch x.sh`, and then redirect the output of two programs into it using `echo "/challenge/pwn;/challenge/college">x.sh`. Now I had to pipe the script's output to `/challenge/solve` using `bash x.sh | /challenge/solve`, which gave the flag. 

Flag: **pwn.college{UCrYi5vb-3cyZnFYPdicM6e_ksA.dhTM5QDL3YTO0czW}**

# Executable-Shell-Scripts

Instead of executing shell scripts with the `bash` command, the work can be done by giving it the execute permissions and running it through its relative or absolute path. In this challenge, I had to create a script that invoked `/challenge/solve`, so I first did `touch x.sh` and then `echo /challenge/solve>x.sh`. Now to give it executable permissions, I ran `chmod u+x x.sh`, and finally `./x.sh` to get the flag.

Flag: **pwn.college{0Lf1p9gtlC8-NCCpsfQA9ocg1Kz.dRzNyUDL3YTO0czW}**
