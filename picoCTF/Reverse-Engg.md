# GDB baby step 1 

**Flag:** `picoCTF{549698}`

**Solution:**
- For this challenge, I first installed *GDB* (GNU Debugger) which is a debugger along with *GEF* (GDB Enhanced Features).
- The challenge gave us an executable file named `debugger0_a` and I executed it with gdb using `gdb ./debugger0_a`.
- The challenge said to disassemble, which is a command used to view assembly level details and so I ran `disassemble main`. 
```
gef➤  disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   rbp
   0x000000000000112e <+5>:     mov    rbp,rsp
   0x0000000000001131 <+8>:     mov    DWORD PTR [rbp-0x4],edi
   0x0000000000001134 <+11>:    mov    QWORD PTR [rbp-0x10],rsi
   0x0000000000001138 <+15>:    mov    eax,0x86342
   0x000000000000113d <+20>:    pop    rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
```
 
- The challenge also asked to look out for the contents in the `eax` register. Here, we can see a hex code beside eax, which when converted from hex to decimal (0x86342 to 549698) and wrapped with `picoCTF{}` gives the flag.
  
**Concepts learnt:**
1. About GDB and what it's used for 
2. The disassemble command

**Mistakes & other approaches:**
- When I first executed the file, it said there were no debugging symbols, and when I ran `run` after `break main` to set a breakpoint, the processes weren't getting listed - so I installed GEF. I was able to view a similar output on this command too now.

**Resources:** 
- https://hugsy.github.io/gef/install/
- https://www.rapidtables.com/convert/number/hex-to-decimal.html?x=86342
# ARMssembly 1


# vault-door-3

