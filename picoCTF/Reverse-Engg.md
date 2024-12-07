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

**Flag:** `picoCTF{00000d2a}`

**Solution:**
- The challenge gives an assembly code and asks for the input required to win. 
```
	.arch armv8-a
	.file	"chall_1.c"
	.text
	.align	2
	.global	func
	.type	func, %function
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 79
	str	w0, [sp, 16]
	mov	w0, 7
	str	w0, [sp, 20]
	mov	w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 20]
	ldr	w1, [sp, 16]
	lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
	sdiv	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	sub	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
.LC0:
	.string	"You win!"
	.align	3
.LC1:
	.string	"You Lose :("
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func
	cmp	w0, 0
	bne	.L4
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6
.L4:
	adrp	x0, .LC1
	add	x0, x0, :lo12:.LC1
	bl	puts
.L6:
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
``` 
  - In the first part of the function, commands `str` & `mov` are used which do the following:
	- space is made on the stack using `sp` (stack pointer)
	- stack + 12 stores w0
	- stack + 16 stores 29
	- stack + 20 stores 7 
	- stack + 24 stores 3
- Now:
	- 79 is loaded into w1 and 7 into w0 and `lsl w0,w1,w0` performs logical shift left which means 79<<7 = 10112 (79 * 2^7) which is now stored in \*(stack+28).
	- 3 is loaded into w0 and the previous answer into w1 and `sdiv w0,w1,w0` performs signed division which means floor of 10112/3 =3370 again stored at \*(stack+28).
- Finally:
	- 3370 is loaded to w1, input x into w0 and `sub w0,w1,w0` does w0 = 3370-x.
	- To win, this answer should be = 0 as `cmp w0,0` compares w0 and 0 and wins only if it's 0.
	- So the input x = 3370
- The flag is in hexadecimal format. 3370 from decimal to hexadecimal is 0d2a and in flag format is equal to 00000d2a.

**Concepts learnt:**
1. Commands such as `str`, `ldr`, `sub`, `sdiv`, `lsl` and `mov` in assembly and a basic idea of format and syntax in ARM assembly for such integer operations

**Resources:**
- https://www.rapidtables.com/convert/number/decimal-to-hex.html?x=3370
- https://iitd-plos.github.io/col718/ref/arm-instructionset.pdf

# vault-door-3

