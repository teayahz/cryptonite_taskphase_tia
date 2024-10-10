# The-Root

An *absolute path* is one that starts with the *root directory*. The example used here, `/pwn`, was the program I had to invoke for the flag.

Flag: **pwn.college{MKUkBdWZ1ms6YpxakUAwxt4I22k.dhzN5QDL3YTO0czW}**

# Program-and-absolute-paths

Here, I had to invoke the *run* file which was in the *challenge* directory which was in the root directory with its absolute path, which was `/challenge/run`.

Flag: **pwn.college{YlMdxbGtWFQ3tL0_pRJ27CM8_N-.dVDN1QDL3YTO0czW}**

# Position-thy-self

`cd` (*change directory*) is a command used to navigate to different directories by passing the directory as an argument. 
The challenge required me to run `/challenge/run` to find the path of the directory (which was `/proc/67`) that was required to re-run the program. So, `cd /proc/run` changed my *current working directory*, then I did `/challenge/run`.

Flag: **pwn.college{EB_OBbcMeCum-6RCA_9PMBv7FmX.dZDN1QDL3YTO0czW}**

# Position-elsewhere

In the same way as the previous challenge, I had to change my directory to a different one for the flag, which was `/tmp` and so I did `cd /tmp` and then, `/challenge/run`.

Flag: **pwn.college{8CbX6GJn_IxEAAbT0yiej9iSpgY.ddDN1QDL3YTO0czW}**

# Position-yet-elsewhere

In the same way as the previous challenge, I had to change my directory to a different one for the flag, which was `/home` and so I did `cd /home` and then, `/challenge/run`.

Flag: **pwn.college{8JxluH5EtI64-6kVQbsRsNrWNQ2.dhDN1QDL3YTO0czW}**

# implicit-relative-paths,-from-/

For this challenge, I had to change my working directory to `/`, and then execute `/challenge/run` as a *relative path*. a relative path is one without '/' at the start. So I first did `cd /`, and then I did `challenge/run`.

Flag: **pwn.college{4HM1cNPN9n0IjuS520cPPPvHpFq.dlDN1QDL3YTO0czW}**


# explicit-relative-paths,-from-/

First, we have to go to `/`. This is now the current working directory and here, absolute paths are equivalent to relative paths. Since `./` refers to the same directory, I ran `cd /` and then `./challenge/run`.

Flag: **pwn.college{Yojf1o6fikEImim5NHsIsuWjYFM.dBTN1QDL3YTO0czW}**

# implicit-relative-path

First, go to the `/challenge` directory using `cd /challenge`. Now, since we can't directly run the program by using `run`, we need to use `.`. Therefore, I then ran `./run`.

Flag: **pwn.college{wX-2xTSu-Qw6jTYmnhEGxvGsVpl.dFTN1QDL3YTO0czW}**

# home-sweet-home

Here, I learnt that the home directory, in this case `/home/hacker`, can be shortened to `~`. Since a file is needed as an argument which is 3 characters long, is in our home directory and is an absolute path, I ran `/challenge/run ~/c`. It works with any number or letter in place of c.

Flag: **pwn.college{khi7nEBVdOtIr-V6osVmDlEC0rc.dNzM4QDL3YTO0czW}**
