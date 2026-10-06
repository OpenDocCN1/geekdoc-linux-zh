
All of these arguments from the macro header. So what's that assembler complaining about? The problem here is that on the simpler CPUs, the IMUL instruction cannot work with immediate operands. (Starting with the 386, a separate form of *IMUL* can take an immediate operand.) And this isn't just a problem with *IMUL*; *all* instructions that cannot work with immediate operands will reject a macro argument under these circumstances.

And "these circumstances" involve the way that the macro is invoked. In an early test version of the Ruler macro that used the IMUL %3 instruction shown previously, I tried to use the following line, which invokes the macro to display a ruler:

```
Ruler Vidorigen,20,80,50,10 ; Draw ruler
```

It didn't work! Except for the video origin address argument, all of these arguments are numeric literals. A numeric literal, when used in assembly language instruction, is called *immediate data*. When the macro is expanded, the argument you pass to the macro is substituted into the actual instruction that uses a macro argument, just as you passed it to the macro.

In other words, if you pass the value 10 in the %5 argument (ScreenY), the instruction `MOV AL,%5` becomes `MOV AL,10` once the macro is expanded by the assembler. Now, `MOV AL,10` is a completely legal instruction. But if you pass the literal value 80 in the %3 argument (ScreenW), you cannot use IMUL %3, because after expansion this becomes IMUL 80, which is not a legal instruction on anything older than the 386.

The problem is *not* that you're using macro arguments with IMUL. The problem is that you're passing a numeric literal in a macro argument to an instruction that (in the form we're using it) cannot accept immediate data.

The version of *Ruler* given in MYLIB.MAC loads the %3 (ScreenW) argument into AH using a MOV instruction. This means that you can use numeric literals when invoking *Ruler*. Using literals saves memory by making memory variables unnecessary, and if you'd prefer to define a meaningful name for the screen width rather than coding the value 80 in the source (which is unwise), you can define a symbol called *ScreenWidth* as an *equate*. I explained equates at the end of Chapter 10. The SHOWCHAR.ASM routine defines a *ScreenWidth* value as an equate.

# Adding ASCII Digits

Once the offset within the buffer for the ruler’s beginning is calculated in DI (and once we set up initial values for CX and AX), we’re ready to start making rulers.

Immediately before the STOSW instruction, we load the ASCII digit ‘1’ into AL. Note that the instruction MOV AL,'1’ does not move the numeric value 01 into AL! The ‘1’ is an ASCII character, and the character ‘1’ (the “one” digit) has a numeric value of 31H, or 49 decimal.

This becomes a problem immediately after we store the digit ‘1’ in video memory with STOSW. After digit ‘1’, we need to display digit ‘2’ and to do that we need to change the digit stored in AL from ‘1’ to ‘2’.

Ordinarily, we can’t add ‘1’ to ‘1’ and get ‘2’; 31H + 31H will give us 62H, which (when seen as an ASCII character) is lowercase *b*, not ‘2’! However, in this case the x86 instruction set comes to rescue, in the form of some peculiar instruction called AAA, Adjust AL after BCD Addition.

What AAA allows us, in fact, to add ASCII digits rather than numeric values. AAA is one of a group of instructions called the BCD instructions, so because they support arithmetic with Binary Coded Decimal (BCD) values. BCD is just another way of expressing a numeric value, somewhere between a pure binary value like 01 and ASCII digit like ‘1’. A BCD value is a 4-bit value, occupying the low nibble of a byte. It expresses between 0 and 9 only. (That’s the “decimal” part of “Binary Coded Decimal” indicates.) It’s possible to express values greater than 9 (from 9 to 15, actually) in 4 bits, but those additional values are not valid BCD values. See Figure 11.1.

The value 31H is a valid BCD value, because the low nibble contains 1. BCD is a 4-numbering system, and the high nibble (which in the case of 31H contains a 3) is ignored. In fact, all of the ASCII digits from ‘0’ through ‘9’ may be considered legal BCD values, because in each case the characters’ low 4 bits contain a valid BCD value. The 3 stored in the high four bits of each digit is ignored.

So, if there were a way to perform BCD addition on the 86-family CPUs, adding ‘1’ and ‘1’ would indeed give us ‘2’ because ‘1’ and ‘2’ can be manipulated as legal BCD values.

AAA (and other instructions I do not have room to discuss here) gives us that ability to perform BCD math. The particular technique may

# The x86 CPUs work with chunks of data no smaller than a byte. A BCD digit, however, occupies only half a byte, or "nibble."

| High Nyble | Low Nyble |
|---|---|
| | 1111 |
| | 1111 |
| | 1110 |
| | 1101 |
| | 1010 |
| | 1001 |
| | 0111 |
| | 0110 |
| | 0101 |
| | 0100 |
| | 0011 |
| | 0000 |

The value 31H is a valid BCD value, because the low nibble contains 1. BCD is a 4-numbering system, and the high nibble (which in the case of 31H contains a 3) is ignored. In fact, all of the ASCII digits from ‘0’ through ‘9’ may be considered legal BCD values, because in each case the characters’ low 4 bits contain a valid BCD value. The 3 stored in the high four bits of each digit is ignored.

So, if there were a way to perform BCD addition on the 86-family CPUs, adding ‘1’ and ‘1’ would indeed give us ‘2’ because ‘1’ and ‘2’ can be manipulated as legal BCD values.

AAA (and other instructions I do not have room to discuss here) gives us that ability to perform BCD math. The particular technique may

The x86 CPUs work with chunks of data no smaller than a byte. A BCD digit, however, occupies only half a byte, or "nibble."

Figure 11.1 BCD Digits

| High Nyble | Low Nyble | Value |
|---|---|---|
| 0000 | 0000 | 0 |
| 0000 | 0001 | 1 |
| 0000 | 0010 | 2 |
| 0000 | 0011 | 3 |
| 0000 | 0100 | 4 |
| 0000 | 0101 | 5 |
| 0000 | 0110 | 6 |
| 0000 | 0111 | 7 |
| 0000 | 1000 | 8 |
| 0000 | 1001 | 9 |
| 0001 | 0000 | A |
| 0001 | 0001 | B |
| 0001 | 0010 | C |
| 0001 | 0011 | D |
| 0001 | 0100 | E |
| 0001 | 0101 | F |

The value 31H is a valid BCD value, because the low nibble contains 1. BCD is a 4-numbering system, and the high nibble (which in the case of 31H contains a 3) is ignored. In fact, all of the ASCII digits from ‘0’ through ‘9’ may be considered legal BCD values, because in each case the characters’ low 4 bits contain a valid BCD value. The 3 stored in the high four bits of each digit is ignored.

So, if there were a way to perform BCD addition on the 86-family CPUs, adding ‘1’ and ‘1’ would indeed give us ‘2’ because ‘1’ and ‘2’ can be manipulated as legal BCD values.

AAA (and other instructions I do not have room to discuss here) gives us that ability to perform BCD math. The particular technique may

The x86 CPUs work with chunks of data no smaller than a byte. A BCD digit, however, occupies only half a byte, or "nibble."

The value 31H is a valid BCD value, because the low nibble contains 1. BCD is a 4-numbering system, and the high nibble (which in the case of 31H contains a 3) is ignored. In fact, all of the ASCII digits from ‘0’ through ‘9’ may be considered legal BCD values, because in each case the characters’ low 4 bits contain a valid BCD value. The 3 stored in the high four bits of each digit is ignored.

So, if there were a way to perform BCD addition on the 86-family CPUs, adding ‘1’ and ‘1’ would indeed give us ‘2’ because ‘1’ and ‘2’ can be manipulated as legal BCD values.

AAA (and other instructions I do not have room to discuss here) gives us that ability to perform BCD math. The particular technique may

The x86 CPUs work with chunks of data no smaller than a byte. A BCD digit, however, occupies only half a byte, or "nibble."

The value 31H is a valid BCD value, because the low nibble contains 1. BCD is a 4-numbering system, and the high nibble (which in the case of 31H contains a 3) is ignored. In fact, all of the ASCII digits from ‘0’ through ‘9’ may be considered legal BCD values, because in each case the characters’ low 4 bits contain a valid BCD value. The 3 stored in the high four bits of each digit is ignored.

The x86 CPUs work with chunks of data no smaller than a byte. A BCD digit, however, occupies only half a byte, or "nibble."

Wait, because ‘1’ and ‘2’ can be manipulated as legal BCD values.

AAA (and other instructions I do not have room to discuss here) gives us that ability to perform BCD math. The particular technique may

... Also, AH would have been incremented by 1.

... and CF is set to 1, as is the Auxiliary flag.

# Adjusting AAA’s Adjustments

There is one problem: AAA clears the high nibble to 0. This means that adding ‘1’ and ‘1’ doesn’t equal ‘2’, the displayable digit. Instead, AL becomes 02, which in ASCII is the dark ‘smiley face’ character. Make AL a displayable ASCII digit again, we have to add 30H to AL. This is easy to: Just add ‘0’ to AL, which has a numeric value of 30H. So, adding ‘0’ takes 02H back to 32H, which is the numeric equivalent of the ASCII digit character ‘2’. This is the reason for the AL/0’ instruction that immediately follows AAA.

There’s a lot more to BCD math than what I’ve explained here. When you want to perform multiple-column BCD math, you have to take carries
