# Coding for Linux

```
pop ecx ; Pop stashed shift value back ecx
shr eax,cl ; Shift the random value by the chosen factor
; keeping in mind that we want is in cl
ret ; Go home with random number in eax
```

To pull a 16-bit random number, call pull16. To pull an 8-bit random number, call pull8, and so on. I did discover that the smaller numbers are not random as the larger numbers, and the numbers returned by pull4 are probably not random enough to be useful. (I left the pull4 code in so you could see for yourself by running RANDTEST.)

The logic here should be easy to follow: Select a shift value, put it in ECX, push ECX on the stack, call rand, pop ECX from the stack, and shift the random number (which rand returns in EAX) by the value in CL—which, of course, is the lowest 8 bits of ECX.

Why does ECX go onto the stack? ECX is not one of the registers in the C calling conventions, and virtually all C library routines use ECX and trash it. If you want to keep a value in a cross to a library function, you have to save your value somewhere before the call, and restore it after the call is complete. The stack is the best place to do this.

I used the pull6 routine to pull random 6-bit numbers to select characters from a character table, thus creating a string of random characters. I padded the table to 64 elements with two additional characters (- and @ so that I wouldn't have to test each pulled number to see if it was less than 62. If you need to limit random values to some range that is not a power of 2—but to design your program so that you don't have to choose randoms in a range like 0 to 65. Much has been written on random numbers in the algorithm books, so if the concept fascinates you, I direct you there for further study.

# Calls to Addresses in Registers

I use a technique in RANDTEST.ASM that sometimes gets forgotten by assembly newcomers: You can execute a CALL instruction to a subroutine address held in a register. You don't always have to use CALL with an immediate label. In other words, the following two CALL instructions are both completely legal and equivalent:

```
mov ebx, dword pull8
call pull8
call ebx
```