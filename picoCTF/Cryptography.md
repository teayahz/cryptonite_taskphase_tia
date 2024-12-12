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

**Resources:** 
- https://sudorem.dev/posts/pico24-c3/

# Custom encryption

**Flag:** `picoCTF{custom_d2cr0pt6d_dc499538}`

**Solution:** 
- The first thing I had to do in this challenge was analyse the encryption code. It had a few steps such as using *Diffie-Hellman key exchange*, XOR & reversing and changing characters by multiplying them with a key and constant.
- There's also a text file given with values for `a` & `b` and the cipher. The `a` & `b` values are used for the Diffie-Hellman key exchange algorithm, where  a common secret shared key is created.
- During encryption, the text is first XORed with a message (here, "trudeau") and then multiplied with the key obtained from the key exchange and a constant 311. 
- Similarly, to decrypt this, the cipher would have to be divided by the key & constant, and then XORed with the same common message to give the original text, which is the flag.
- I reversed these encryption algorithms and created functions for it, supplied the values given to us, and this is the final decryption program:
```python
import sys

def generator(g, x, p):
    return pow(g, x, p)

def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(ord(char) * key * 311)
    return cipher

def decrypt(cipher, key): #Reverse of encrypt
    plaintext_chars = []
    for num in cipher:
        if num != 0:
            char_code = num // (key * 311)
            plaintext_chars.append(chr(char_code))
        else:
            plaintext_chars.append('\0') 
    return ''.join(plaintext_chars)

def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char #adding char to the end
    return cipher_text

def dynamic_xor_decrypt(cipher_text, text_key): #XOR decryption
    decrypted_text = ""
    key_length = len(text_key)
    for i, char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decrypted_text = decrypted_char + decrypted_text  #adding char to the beginning
    return decrypted_text

def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True

def decryption(cipher, text_key, a, b):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers.")
        return
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    if key != b_key:
        print("Invalid key")
        return
    semi_cipher = decrypt(cipher, key)
    decrypted_text = dynamic_xor_decrypt(semi_cipher, text)
    print(f"Decrypted text: {decrypted_text}")

#Assigning given values
cipher = [33588, 276168, 261240, 302292, 343344, 328416, 242580, 85836, 82104, 156744, 0, 309756, 78372, 18660, 253776, 0, 82104, 320952, 3732, 231384, 89568, 100764, 22392, 22392, 63444, 22392, 97032, 190332, 119424, 182868, 97032, 26124, 44784, 63444]
a = 89
b = 27
text = "trudeau"
decryption(cipher, text, a, b)

```

The output: 
```
Decrypted text: picoCTF{custom_d2cr0pt6d_dc499538}
```
 
**Concepts learnt:**
1. Diffie-Hellman key exchange which is a method used to create a common shared secret key and its implementation in the code.
2. Certain syntaxes of Python such as `if __name__ == "__main__":` to ensure the file runs as a script than when imported as a module, `''.join()` used to join characters without a separator, `[::-1]` used to reverse, `sys.argv[1]` which checks for the first argument entered with the command.
3. Implementation of XOR in code using the `^` operator, `chr()` & `ord()` to convert the characters/integers.

**Mistakes & other approaches:**
- Initially I executed the code as it is with the given information and didn't understand the use of `randint` and the `a` & `b` values.
- I tried to compile all the decryption methods into one function, which made it likely to have more errors and so it was easier to split them into different functions.

**Resources:** 
- https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange

# miniRSA

**Flag:** `picoCTF{n33d_a_lArg3r_e_606ce004}`

**Solution:**
- The `ciphertext` file consists of three integers which had to be used to decrypt the message encrypted in RSA.
```
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125 
```
- After looking up the significance of a small e value, I found that it could make decoding much more simpler and thus the encryption much less strong. I found that the original message m could now be found with the formula m = **$\sqrt[3]{C}$**  as C seems to be much lesser than N and e here is 3. 
- Now I made a Python program to calculate the the cube root of this large integer C, and also to convert the integer m obtained to the original message M by converting to hex and then to ASCII.
```python
def cube_root(n):
    # Using integer arithmetic to calculate the cube root
    low, high = 0, n
    while low < high:
        mid = (low + high + 1) // 2
        if mid ** 3 <= n:
            low = mid
        else:
            high = mid - 1
    return low

def int_to_ascii(num_str):
    num = int(num_str)
    root = cube_root(num)
    hexa = hex(root)[2:]  # removes the '0x' prefix
    text = ''
    for i in range(0, len(hexa), 2):
        hex_pair = hexa[i:i+2]
        if len(hex_pair) == 2:
            text += chr(int(hex_pair, 16))
    
    return text

C = "2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125"
flag = int_to_ascii(C)
print(f"Flag: {flag}")

```

  
**Concepts learnt:**
1. RSA and the working of its encryption and significance of numbers m, e, C, N, p, q & d
2. The significance of the public encryption exponent e & the 2048-bit key N (617 digits) as when e is small and $m^e$ is less than N, m is simply $\sqrt[e]{C}$ but when $m^n$ > N, the padding constant k is to be found and m = $\sqrt[e]{C+k.N}$
3. Also learnt that the value `65537` is often used as e which is a Fermat number.
   
**Mistakes & other approaches:**
- While calculating cube root for such large integers, the answer gets printed in an exponent form and loses precision which didn't help me in this case.
- The answer was also retrieved by putting in the values in https://www.dcode.fr/rsa-cipher.
  
**Resources:**
- https://www.javatpoint.com/rsa-encryption-algorithm
- https://ir0nstone.gitbook.io/crypto/rsa/public-exponent-attacks/small-e
- https://en.wikipedia.org/wiki/RSA_(cryptosystem)#Decryption
  
