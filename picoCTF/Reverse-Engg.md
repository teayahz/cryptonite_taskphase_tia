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

**Flag:** `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}`

**Solution:**
- A Java source code is given and the password is to be found by analyzing it. 
```java
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18gb41_u_4_mfr340");
    }
}
```
- Here, the buffer is supposed to be equal to the string `jU5t_a_sna_3lpm18gb41_u_4_mfr340`, and the buffer string is put together based on the password entered which should be 32 characters long.
- To find the password, we have to work from the final string.
	- First 8 characters of the password is the same as that of the final string i.e. `jU5t_a_s`
	- Next 8 characters of the password are reverse of the next 8 characters of the final buffer i.e. `na_3lpm1` which gives `1mpl3_an`
	- The next few even places are filled accordingly:
	  password[30] = buffer[16], password[28] = buffer[18], password[26] = buffer[20], password[24] = buffer[22], password[22] = buffer[24], password[20] = buffer[26], password[18] = buffer[28], password[16] = buffer[30] 
	  which is `4[]r[]m[]4[]u[]1[]b[]8[]` and the remaining odd places are directly mapped from the buffer to finally give the last 16 characters: `4gr4m_4_u_1fb380`
- The final password is now `jU5t_a_s1mpl3_an4gr4m_4_u_1fb380`

**Concepts learnt:**
1. Analyzing Java code and converting to C

**Mistakes & other approaches:**
- Instead of reversing this process manually, I tried to do this in a C program:
```c
#include<stdio.h>
int main(){
    char *password = "jU5t_a_sna_3lpm18gb41_u_4_mfr340";
    char buffer[32];
    int i;
    for (i=0; i<8; i++) {
        buffer[i] = password[i];
    }
    for (; i<16; i++) {
        buffer[i] = password[23-i];
    }
    for (; i<32; i+=2) {
        buffer[i] = password[46-i];
    }
    for (i=31; i>=17; i-=2) {
        buffer[i] = password[i];
    }
    printf("%s",buffer);
}
```
This easily gave the output required which was `jU5t_a_s1mpl3_an4gr4m_4_u_1fb380`
