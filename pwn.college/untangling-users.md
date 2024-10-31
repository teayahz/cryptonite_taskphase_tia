# Becoming-root-with-su

`su` (switch user) command has the SUID bit set and can run as root and start a root shell, after checking for root password. Modern systems don't have root passwords, but this challenge did which was `hack-the-planet`, so I entered it after running `su`, then read the flag with `cat /flag`.

Flag: **pwn.college{8AHAerLYj9ZAX034xet9NWL4biR.dVTN0UDL3YTO0czW}**

# Other-users-with-su

When `su`, is entered without arguments, it starts a root shell. But, a username can be given as the argument, to switch to that user. In this challenge, I had to switch to the user *zardus* with `su zardus`, enter its password and then run `/challenge/run` for the flag.

Flag: **pwn.college{8Aw6owsFfdz23hlog4pGsgbDdCE.dZTN0UDL3YTO0czW}**

# Cracking-passwords

Passwords used to be stored in `/etc/passwd` but since it's globally readable, it was moved to `/etc/shadow`. Passwords are stored as *hashes* and it can be cracked with *John the Ripper* or the `john` command. Here, I ran `john /challenge/shadow-leak` to find the password of *zardus*, and then ran `su zardus` with the password I got which was *aardvark* to switch to *zardus*, and ran `/challenge/run` to get the flag.

Flag: **pwn.college{snjK3S-IP3R07KEUzLhz6ThAsoI.ddTN0UDL3YTO0czW}**

# Using-sudo

`su` requires root passwords, and they are hard to maintain & can leak. So `sudo` (superuser do) is used to directly run a command as root. In this challenge, we are given `sudo` access which is used to read the flag this time, so I ran `sudo cat /flag`.

Flag: **pwn.college{owp6lMhrS_At5-inncQj-f0Te5l.dhTN0UDL3YTO0czW}**
