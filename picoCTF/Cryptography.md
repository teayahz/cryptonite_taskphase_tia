# C3

**Flag:** `picoCTF{adlibs}` 

**Solution:** 
- Since the challenge mentioned that it's a cyclical cipher, I opened the code and saw two strings of text that were used for the substitution - `lookup1` & `lookup2`. But these had to be swapped or else the characters would be mismatched. 
- The decoding function also had to be edited from `cur-prev` to `cur+prev` as else it cycles backwards, and I added a variable to determine this index, and changed the `prev` value to this. 
```c
for char in chars:
  cur = lookup1.index(char)
  index = (cur+prev)%40
  out += lookup2[index]
  prev = index 
``` 
- I ran the code on shell using `python3 convert.py ciphertext` as the code had a line to read text from the cipher file. The output was: 
```
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```
This is the new code I had to work with. The comments give clues such as - it's compatible with python2 & *selfinput*, which referred to using this output as the input itself for the new code.

- So I replaced the old code with this output, and made edits such as `print chars[i]` to `print (chars[i])` as the latter is python3 format. I replaced the `chars = ""` string with this exact output code using `""" """` and deleted the file input reading command. The final code is: 
```c
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = """#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1"""

b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print (chars[i]) #prints
        b += 1 / 1
```

Output:
```
a
d
l
i
b
s
```

**Concepts learnt:**
1. The cyclical cipher, which works on substitution.
2. The difference between some syntax like print in python2 & python3 
3. Executing python code with a file and using the file's contents as input for the code.

**Mistakes & other approaches:**
- I had to change `(cur-prev)%40` to `(cur+prev)%40`.
- Initially, I put the original ciphertext into the second code's `chars` string, and got confused from the misleading output, then the first code which still didn't give the required output, and then used the new code.
- Forgetting to change `print chars[i]` to `print (chars[i])`
- Instead of creating a new .txt file of the first ouput, to run it with the new code in shell, I directly pasted it into the `chars = ""` string. This could be done with the first code too.

**References:** 
- https://sudorem.dev/posts/pico24-c3/

# Custom encryption


# miniRSA


