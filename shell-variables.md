# Printing-Variables

The `echo` command that can be used to print out its arguments also prints out variables entered that are prefixed with `$`. For this challenge, I had to print out the `FLAG` variable, so I ran `echo $FLAG`.

Flag: **pwn.college{86G3Y9zs0QFKBRmnzyOgFPp992Q.ddTN1QDL3YTO0czW}**

# Setting-Variables

Values can be set to variables using the `=` operator, without spaces between the name and the sign. `$` is not needed like the previous case as it is only used before the variable to access it. Here, I had to set PWN to the value COLLEGE, so I simply ran `PWN=COLLEGE`.

Flag: **pwn.college{Ev2RfCpDQEUDpM0IVCCn3LzBiCO.dlTN1QDL3YTO0czW}**

# Multi-word-Variables

Spaces present in the value o variable's name can cause the shell to interpret the word after the space as a new command. To bypass this, the variable name can be put in `" "`. To assign `PWN` to `COLLEGE YEAH`, I used `PWN="COLLEGE YEAH"`.

Flag: **pwn.college{8XV-LbNj_qW6cvfD0yxencVFYJx.dBjN1QDL3YTO0czW}**

# Exporting-Variables

While assigning variables, they are local to the current shell process, as in they can't be accessed by invoking another shell process using `sh` as a *child process*. But it can be exported using the `export` command. First to export the value of PWN to COLLEGE, I ran `export PWN=COLLEGE` and then to assign COLLEGE to PWN without exporting, I ran `COLLEGE=PWN`. Now to check if just PWN was exported, I ran `sh` and then `/challenge/run` to get the flag.

Flag: **pwn.college{4PILn27N0gdMcmGslbGFZitNUS3.dJjN1QDL3YTO0czW}**

# Printing-Exported-Variables

The `env` command is another command to access variables. It prints our every *exported* variable in the shell and so by running it, I found the value to the `FLAG` variable.

Flag: **pwn.college{oY7wkJNAIXYVZqZlCdubG_HTyOs.dhTN1QDL3YTO0czW}**

# Storing-Command-Output

*Command Substitution* is used to store the output of a command into a variable. It can be done with the format `[VARIABLE]=$(command)` or ```$(): VARIABLE=`command` ```, which is an older version and it has disadvantages while nesting command substitutions. In this challenge I stored the output of `/challenge/run` into `PWN` using `PWN=$(/challenge/run)` and then read it out using `echo "$PWN"`.

Flag: **pwn.college{cARu3_fgZDvoLtGyonYQuAowc3X.dVzN0UDL3YTO0czW}**

# Reading-Input

The `read` command is to read input from the user. It's often used with the `-p` argument to take in a prompt. In this challenge, I had to set the value `COLLEGE` to the `PWN` variable, but using `read`. So I did `read -p "Input: " PWN` and entered `COLLEGE` as input, and got the flag. `"Input: "` here is being used as a statement to be printed before input is entered by the user. 

Flag: **pwn.college{YqWWZY9K-rHlsUd_igp3cctDE_m.dhzN1QDL3YTO0czW}**

# Reading-Files

Files can be read in shell by reading it into a variable by redirecting the file into the input of the `read` command as a variable, using `<`. To read `/challenge/read_me` into the variable `PWN`, I ran `read PWN < /challenge/read_me`.

Flag: **pwn.college{AuSXnbXso9Mh4XjJ0ETILybFLHh.dBjM4QDL3YTO0czW}**

