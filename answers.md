1. challenge is a 64-bit ELF executable for the x86-64 architecture. The disassembly header shows “file format elf64-x86-64”. I also ran file challenge to check its details.

2. The constant is 0x2a, found in movl $0x2a,-0x8(%rbp)

Its decimal value is 2 × 16 + 10 = 42.

3. The constant is stored at -0x8(%rbp), which is 8 bytes below rbp. It is stored as a 32-bit value.

4. The constant is first loaded into edx and copied into eax. Then these arithmetic instructions run:

shl $0x3,%eax shifts the value left by 3 bits, multiplying it by 8.
sub %edx,%eax subtracts the original constant, 42, from eax.
add $0xd,%eax adds 13 to eax.

5. The final calculated number is 307:

42 × 8 = 336
336 − 42 = 294
294 + 13 = 307

6. The calculated number is stored at -0x4(%rbp), which is 4 bytes below rbp. The entered number is stored at -0x14(%rbp), which is 20 bytes below rbp.

7. The instruction cmp -0x4(%rbp),%eax compares the entered number in eax with the calculated number stored on the stack. It updates the CPU flags without changing either value.

sete %al sets al to 1 if the numbers are equal, or 0 otherwise. movzbl %al,%eax then zero-extends that byte into eax, giving a return value of 1 for a match or 0 for a mismatch.

8. I ran ./challenge and entered 307.

got access granted
