# Matching-with-*

`*` is treated as a *wildcard* and replaces files that match the pattern as in out of `file_a, file_b & file_c`, `file_*` would return all three. For this challenge, I had to navigate to the *challenge* directory by using atmost 4 characters. So I ran `cd /c*e`, and then /challenge/run.

Flag: **pwn.college{4_rdyAyEzqNlgKeGG-0oygq2cR4.dFjM4QDL3YTO0czW}**

# Matching-with-?

`?` is treated as a *single character wildcard* where it just replaces one character. Here, I had to again navigate to the *challenge* directory, by using `?` for c & l, and without using *. So I ran `cd /?ha??enge` and then `/challenge/run`.

Flag: **pwn.college{knZutl56lVOxAaurjXG3BYskhDI.dJjM4QDL3YTO0czW}**

# Matching-with-[]

[] matches a set of characters specified inside it. For this challenge, I had to bracket-glob `file_b, file_a, file_s & file_h`, so I first went to the required directory with `cd /challenge/files` and then ran `/challenge/run file[bash]`.

Flag: **pwn.college{kd0M1_jk00ofLsUN7dMW9-HDZTT.dNjM4QDL3YTO0czW}**

# Matching-paths-with-[]

The files were placed in `/challenge/files` and had to be globbed with its absolute paths, from the home directory. So a single command - which was `/challenge/run /challenge/files/file_[bash]`, was enough to get the flag.

Flag: **pwn.college{QQYip5IryneE18MGRYVvCedIpqL.dRjM4QDL3YTO0czW}**

# Mixing-globs

This challenge required to match files named *challenging*, *educational* & *pwning*. First, I had to `cd` into `/challenge/files`, then run `/challenge/run [cep]*` as the argument had to be 6 characters or less, and `[cep]*` matches all three required files.

Flag: **pwn.college{kxuvToU_mGwfQIvPfUrb8dLdAqA.dVjM4QDL3YTO0czW}**

# Exclusionary-globbing

In this challenge, I had to filter out files that do NOT start with p, w or n with either a `!` or `^`. First, I did `cd /challenge/files` & then `/challenge/run [^pwn]*` which gave us the flag.

Flag: **pwn.college{EIkmDQ3JeWaYQqqvb5hiM2ICn_m.dZjM4QDL3YTO0czW}**