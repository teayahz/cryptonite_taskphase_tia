# Changing-File-Ownership

`chown` is a command used to *change ownership* of files which can only be invoked by the root user, and taking over the *root* user is a major hacking objective. Here, to change ownership of `/flag` to `hacker`, I had to run `chown hacker /flag` and then read it out using `cat /flag`.

Flag: **pwn.college{4r1vz4IvW1BkGg4dzNHaPl-FhLY.dFTM2QDL3YTO0czW}**

# Groups-and-Files

*Groups* can have multiple users in it and users can be members of multiple groups. Groups can be checked with the `id` command. `chgrp` (change group) is used to change the group ownerships and typically requires root access. Here, the group ownership of the flag file had to be changed by invoking `chgrp` as `hacker`, so I ran `chgrp hacker /flag` and then `cat /flag` to read the flag file. 

Flag: **pwn.college{As09F-o9K-t3xY2HmNWYfiWeGCr.dFzNyUDL3YTO0czW}**

# Fun-With-Groups-Names

Like mentioned before, `id` command can be used to find the groups that the user is present in, and I found the group `grp31776`. I then used `chgrp grp31776 /flag` to change the group and `cat /flag` to run.

Flag: **pwn.college{4S2upz_Sbm9oZa6zKCo0fzRLZYU.dJzNyUDL3YTO0czW}**

# Changing-Permissions

While running the `ls -l` command, we can see the permissions of the files/directories which are a set of 9 characters from **r**ead, **w**rite, e**x**ecute, - (nothing). The first three represent permissions of the user that owns the file, the next three for the group and the last three for other users.

File permissions can be changed with the `chmod` (change mode) command. The mode in chmod can be modifications of the existing permissions, as in it can add (+) or remove(-) permissions for a **u**ser, **g**roup or **o**ther users. To make the flag readable, I had to add the read permission to other users using `chmod o+r /flag`, and then `cat /flag` to read the flag.

Flag: **pwn.college{QXrY4HvKw7JIibhgAdyMAESyqCD.dNzNyUDL3YTO0czW}**

# Executable-Files

Executable permission ensures that you can execute the program, and is denoted by `x`. To make `/challenge/run` executable, I had to add the executable permission to the user by using `chmod u+x /challenge/run`, and then I executed the program.

Flag: **pwn.college{IzznprvLscIbdP9zP3qh8pO3Qcz.dJTM2QDL3YTO0czW}**

# Permission-Tweaking-Practice

This challenge required to change the permissions of `/challenge/pwn` as specified and began by running `/challenge/run`. It was then a series of 8 rounds of changing permissions, which I had to get all right to permissions to make the flag readable. Example: to add read permission to the user, remove execute permission from the group, and add read & write permission to world, I'd run `chmod u+r,g-x,o+rw /challenge/pwn`. After restarting the challenge several times, I cleared it and then did `chmod u+r /flag` to make it readable and read it with `cat /flag`.

Flag: **pwn.college{skwoCd2gpmY3gGoboQE1UMWY3cw.dBTM2QDL3YTO0czW}**

# Permissions-Setting-Practice

Instead of permissions being added or removed, they can be overwritten using `=`. Multiple modes' permissions can be set together by separating them with a `,` as in `chmod u=rx,g=r,o=r /file`  where the different modes get different permissions. The permissions can be cleared with `=-`.

In this challenge, I had to set permissions right eight times in a row using `=` & `,`, which was fairly easier as they are depicted with the 9 characters. So if `rwx---rwx` had to be set to `---r-xr--`, I ran `chmod u=-,g=rx,o=r /challenge/pwn`. After completing the rounds, I made `/flag` readable with `chmod u+r /flag` and then `cat /flag` to read it.

Flag: **pwn.college{IzrhixLea-OgNPuxsbgJ1E9d4ks.dNTM5QDL3YTO0czW}**

# The-SUID-Bit

*SUID* (Set User ID) permission allows a user to run a program as the owner of the program file, and is represented by `s` and can be set with `chmod`. In this challenge I had to add the SUID bit to `/challenge/getroot` and so I ran `chmod u+s /challenge/getroot` and executed the program which made it run as root. Then I did `cat /flag` to read the flag.
 
Flag: **pwn.college{8bsymOvr_5QwRBiCYjCavjaAOgN.dNTM2QDL3YTO0czW}**
