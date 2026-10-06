# ASSEMBLY LANGUAGE STEP-BY-STEP

the instruction makes. And once CX gets decremented down to 0, REP STOSW detects that CX is now 0 and stops firing into memory. Control then passes to the next instruction in line. But take away REP, and the automatic decrementing of CX stops. So, also does the automatic detection of CX has been counted down to 0.

Obviously, something has to decrement CX, since CX governs how many times the string instruction accesses memory. If STOSW doesn't do it—you guessed it—you have to do it somewhere else, with another instruction.

The obvious way to decrement CX is to use DEC CX. And the obvious way to determine if CX has been decremented to 0 is to follow the DEC instruction with a JNZ (Jump if Not Zero). JNZ tests the Zero flag ZF and jumps back to the STOSW instruction until ZF becomes true. And ZF becomes true when a DEC causes its operand (here, CX) to become 0.

# The LOOP Instructions

With all in mind, consider the following assembly instruction loop. Note that I've split it into three parts by inserting blank lines:

DoChar: stos    ; Note that there's no REP prefix!

```
add AL, '1'      ; Bump the character value in AL up by 1
aaa             ; Adjust AX to make this BCD addition
add AL, '0'      ; Basically, put binary 3 in AL's high nibble
mov AH, 07       ; Make sure our attribute is still 7
dec CX           ; Decrement the count by 1..
jnz DoChar      ...and loop again if CX > 0
```

Ignore the block of instructions in the middle for the time being. What it does is I suggested could do a little earlier: change each store of AX into memory. I'll explain in detail shortly. Look inside (for now) to see how the loop runs. STOSW fires, AX is modified, and then CX is decremented. The JNZ instruction tests to see if the DEC has forced CX to zero. If so, the Zero flag ZF is set, and the loop will terminate. But until ZF is set, the jump is made to the label DoChar, where STOSW fires yet again.

There is a simpler way, using an instruction I haven't discussed until now: LOOP. The LOOP instruction combines the decrementing of CX with a test and jump based on ZF. It looks like this: