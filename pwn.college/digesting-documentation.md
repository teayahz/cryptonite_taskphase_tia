# Learning-From-Documentation

For this challenge, `/challenge/challenge` had to be run with the argument of `--giveflag` and so I ran `/challenge/challenge --giveflag`.

Flag: **pwn.college{Q5Ubb9VNaVe2iR4PpnNH9Mp5DkQ.dRjM5QDL3YTO0czW}**

# Learning-Complex-Usage

In this challenge I had to run `/challenge/challenge` with another argument named `--printfile` with another argument for the flag file which was `/flag`, and so altogether it was `/challenge/challenge --printfile /flag`.

Flag: **pwn.college{oorHrFCKy7qiCE9J5IuY_NeIAOh.dVjM5QDL3YTO0czW}**

# Reading-Manuals

`man` displays the manual of the command passed as an argument. By running `man challenge`, I found that there's an argument that can be passed for the flag and so I ran `/challenge/challenge -bzzaxd 403`.

Flag: **pwn.college{4HJb0Q_zzS36Va5xGMdTC0yiJRU.dRTM4QDL3YTO0czW}**

# Searching-Manuals

By running `man challenge` and searching through the manual page with `/`, and using `n` to go to the next page of the manual, I found the argument required to run the flag. So I ran `/challenge/challenge -f.`

Flag: **pwn.college{oGId8MHgMOQHCsLxaX06_1Z2b7i.dVTM4QDL3YTO0czW}**

# Searching-For-Manuals

First, I had to read through the `man man` page. I found the `-k --global-apropos` command which searches through text in manual pages, and ran it with the argument `challenge`. This gave the *man* page for *challenge* and showed the argument that's used to get the flag. So finally, I ran `/challenge/challenge --kvfbkb 344`.

Flag: **pwn.college{kTXHESK_vfb-kCWSbBX3OhMHu4L.dZTM4QDL3YTO0czW}**

# Helpful-Programs

Sometimes, instead of a man page, an argument like `--help` or `-h` helps us find what we need. Here I ran `/challenge/challenge --help` and found two arguments - one to display the secret value and the other for the flag. So first I ran the same program with the argument `-p` to print the value for the `-g` command that has the flag. Finally, I ran `/challenge/challenge -g 924`.

Flag: **pwn.college{QXkT-TMLs9Spdp2M43YfzGZ60_x.ddjM4QDL3YTO0czW}**

# Help-for-Builtins

Here, I used the `help` *builtin* to lookup help on other *builtins* such as `challenge`. `help challenge` returned the name of the argument used to get the flag, along with a secret value. With this information, I ran `challenge --secret MPxDnCd7` to get the flag.

Flag: **pwn.college{MPxDnCd7_ZXGLd9tOpGz4AOMdeZ.dRTM5QDL3YTO0czW}**
