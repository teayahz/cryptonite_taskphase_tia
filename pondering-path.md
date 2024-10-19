
# The-PATH-Variable

`PATH` is a special shell variable that stores directory paths to search for. If it's run with a *blank string* (""), it won't have directories to search for executable files. In this challenge, the flag was only given if `rm` command was not found. So I ran `PATH=""` , `rm /challenge/run` to check, and then `/challenge/run`.

Flag: **pwn.college{ch-bf8INRpVK530jY5lL4-VYdT3.dZzNwUDL3YTO0czW}**
# Setting-PATH

`PATH`s can take in the path of a file or directory as its value, and then the file or directory can be called with its bare name. In this challenge, I had to run `win` with its bare name. So I specified its path in PATH using `PATH=/challenge/more_commands` and then ran `/challenge/run` to check it.

Flag: **pwn.college{UdhZQTmH_JqAhTQQMGrysbEDroi.dVzNyUDL3YTO0czW}**
# Adding-Commands

In this challenge, I had to create a `win` file that contained the flag, and add its location to PATH. So I ran `touch win` & then `echo 'cat /flag'>win` to create the file and have it have the flag. The path was set using `PATH="/home/hacker:$PATH"` where the home directory is appended to the existing paths. I made the *win* file executable using `chmod +x win` (where all users are given executable permissions) and proceeded with `/challenge/run`.

Flag: **pwn.college{whCK-m9jwXla29sLdhDn9N1u8Qc.dZzNyUDL3YTO0czW}**
# Hijacking-Commands

In this challenge, `rm` command attempts to delete the flag. But, by running the same commands as the last challenge by creating an *rm* file of my own, the original intention of *rm*, that is to delete the flag, can be overridden to get the flag instead. So I ran `touch rm`, proceeded by `echo 'cat /flag'>rm`, `PATH="/home/hacker:$PATH"`, `chmod +x rm` and finally `/challenge/run`. 

Flag: **pwn.college{AFYHDQGog9VEzjHmfO8PSG4HAK8.ddzNyUDL3YTO0czW}**