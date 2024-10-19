# Listing-Processes

Processes are listed using the `ps` command. There are two ways to specify arguments in it: *Standard* & *BSD* syntax. The first one has arguments `-e` to print *every* process, `-f` for a *full format* output and can be combined into `-ef`. The latter has arguments `a` to list processes for *all users*, `u` for *user-readable* output & `x` for processes that *aren't running*, which can again be combined into the single argument, `aux`. Both result in a similar output that consists of user ID, start time, time, command name, process ID & TTY. 

In this challenge, the flag command was renamed and I had to find it by listing out processes with `ps aux`. I found it in the CMD column and then ran it which was with the name `/challenge/5213-run-6739`.

Flag: **pwn.college{E-BVcT2NO3Icip_IoxmgTZKTE60.dhzM4QDL3YTO0czW}**

# Killing-Processes

Processes can be *terminated* using the `kill` command by attaching the `PID` as its argument. To kill `/challenge/dont_run` so that `/challenge/run` can run, I found the PID of it using `ps -e | grep /challenge/dont_run`, which was 73, and then did `kill 73`, and finally `/challenge/run` for the flag. 

Flag: **pwn.college{YCD5TBX4_qL-NL0PWuOnTF5KwXO.dJDN4QDL3YTO0czW}**

# Interrupting-Processes

Instead of killing processes, you can interrupt them using the `Ctrl+C` hotkey so that the process that the command is waiting on is interrupted and cleanly exits. To get the flag, I ran `/challenge/run` & interrupted it with `Ctrl-C`.

Flag: **pwn.college{Enec-d8jgw1SW-x5BGs4Ux8KgKc.dNDN4QDL3YTO0czW}**

# Suspending-Processes

Processes can also be suspended in the background with the `Ctrl+Z` hotkey, and resumed later. In this challenge I had to suspend `run`, and again run a copy of it so I entered `/challenge/run`, hit `Ctrl-Z`, and then ran `/challenge/run` again.

Flag: **pwn.college{kOjK2APhGiE6jVcwvG1O92WusyY.dVDN4QDL3YTO0czW}**

# Resuming-Processes

The `fg` (*foreground*) command is used to resume suspended processes. Here I ran `/challenge/run`, pressed `Ctrl+Z` which suspended the process. Then I ran `fg /challenge/run` to resume it.

Flag: **pwn.college{kvsdql89IYtNnCGYmz4UmPTv0rj.dZDN4QDL3YTO0czW}**

# Backgrounding-Processes

Similar to `fg` resuming processes in the *foreground*, suspended processes can be resumed in the *background* using `bg`. To clear this challenge I had to suspend `run`. I did this by running `/challenge/run`, followed by `Ctrl+Z`. Then resumed it in the background with `bg /challenge/run`, and then launched a copy with `/challenge/run`. Also, the + sign in the STAT column while listing processes indicates that the process is in the foreground.

Flag: **pwn.college{QQyaPTWS3YDWdbHy38Iw7DvT6Oc.ddDN4QDL3YTO0czW}**

# Foregrounding-Processes

This challenge required me to first suspend the `/challenge/run` with `Ctrl-Z`, then resume it in the background with `bg /challenge/run` and again bring it to foreground with `fg /challenge/run`.

Flag: **pwn.college{oDQFLSbnnB-ksOXw7sKUpPqURQ4.dhDN4QDL3YTO0czW}**

# Starting-Background-Processes

The processes don't have to be suspended to background them, it can be done by appending `&` to the `bg` command. To background `run` to get the flag, I just had to run `bg /challenge/run &`. 

Flag: **pwn.college{E0iE1IU8gTdhcoqASzuwCTfop3n.dlDN4QDL3YTO0czW}**

# Process-Exit-Codes

Every command in the shell, exits with an *exit* code when it terminates. Exit code of the most recently terminated command can be accessed with `?`, prepended by `$`. Successful commands typically return 0, while errors return non-zero values, usually 1. 

To access the exit code of `/challenge/get-code`, I ran it and it exited with an error code, and then ran `echo $?`, which resulted in 8. Then I passed it as an argument as `/challenge/submit-code 8` and got the flag.

Flag: **pwn.college{QqHyxj0e_cv7O8vAkWyID8yIpZT.dljN4UDL3YTO0czW}**
