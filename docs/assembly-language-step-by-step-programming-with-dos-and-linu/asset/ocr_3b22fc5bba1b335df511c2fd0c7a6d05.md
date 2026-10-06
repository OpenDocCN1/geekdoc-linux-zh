six instructions: SHL, SHR, ROL, ROR, RCL and RCR. (The instru-
t SAL and SAR are just duplicate names for SHL and SHR.) I dealt
with the shift instructions in Chapter 10, as they exist on the 8088 and
8086. For those ancient CPUs, you can express the number of bits by
which to shift in one of only two ways:

```
shl AX,1    ; Shift left by 1
shl AX,CL   ; Shift left by number in CL
```

(Note that this discussion applies to any of the shift/rotate instructions,
and not just SHL.) To shift an operand of 1 bit, you could specify the lit-
eral value 1. To shift by any greater number of bits greater than 1, you
ad to first load a count into the CL register, and then use CL as
the second operand. Well, that was the 16-bit world. In 32-protected
mode you can drop the use of CL and use an immediate value for any
legal shift values, 1 or whatever up to 31. It becomes legal to use instru-
 that look like this:

```
shl eax,17
```

Note that the shift count is limited to 31. If you shift a 32-bit operand by
32 or more bits in either direction, you're left with nothing but zeros in
t operand, because all significant bits will be shifted completely out
of the operand into nothing. So, for the shift instructions, at least,
shifting by more than 31 bits is meaningless.

It's less obviously true for the rotate instructions, but here, too, there's no
advantage to rotating a value by more than 31 bits. The rotate instru-
ctions, if you recall, rotate bits off one end of the operand and then find
them back into the opposite end of the operand, to begin the trip again. If
you mentally follow a single bit through the rotation process, you'll real-
ize after 32 rotations, any given bit is where it was when you started
rotating the value. What's true of one bit is true of all them, so 30 rotations
is as much as will be useful on a 32-bit value. This is why, in protected
mode programming (and on the 286 as well), the shift-count by trun-
cated to 5 bits: The largest value expressible in 5 bits is . . .32

# Looking for 0 Bits with BT

Back in Chapter 10 I introduced the TEST instruction, which allows you
to determine whether any given bit in a byte or word is set to 1. As I
explained, TEST has its limits: It's not cut out for determining when a
bit is set to 0.