
# Table 3.10. Four-Bit Two's Complement Representation

| Decimal | Binary |
| :--- | :--- |
| -1 | 1111 |
| -2 | 1110 |
| -3 | 1101 |
| -4 | 1100 |
| -5 | 1011 |
| -6 | 1010 |
| -7 | 1001 |
| -8 | 1000 |
| 7 | 0111 |
| 6 | 0110 |
| 5 | 0101 |
| 4 | 0100 |
| 3 | 0011 |
| 2 | 0010 |
| 1 | 0001 |

Notice that although the first bit in a two’s complement system is a sign bit, it is not just a sign bit. For example, if we change the sign bit on 1011, we get 0011. This changes -5 to 3, not 5.

# 3.6.5 Signed vs. Unsigned Numbers

If all arithmetic done on computers were done using two’s complement representation, there would never be any problem interpreting the contents of a numerical register. But unfortunately this is not the case. Sometimes arithmetic is done and it is assumed that the numbers are represented using the plain binary system. So when a four-bit register has a 1011 in it, does this mean -5 or 11? If we are using two’s complement, then we know it is -5. But we could be using just plain binary! Then we have 11. Computing practice is not consistent about this. Both systems are used. It could be either one. It is up to the software to make the distinction. The terminology *signed* vs. *unsigned* is often used. Signed integers are two’s complement integers. Unsigned integers are plain binary integers.

Although when we are adding numbers, it doesn’t matter if the numbers are signed or unsigned — the adding hardware works either way — many other operations require different implementations depending on whether the operand is intended as a signed or an unsigned number. Consider inequality testing. Suppose four-bit hardware is asked to determine whether 1011 < 0010 is true or not. While 0010 represents 2 in both the signed and the unsigned systems, 1011 is -5 as a signed number and 11 as an unsigned number. The signed interpretation, -5 < 2, yields a true, whereas the unsigned interpretation, 11 < 2, yields a false. The hardware must make a different response in the two cases. This means that a single "less than" command can’t work. Two are needed, one for signed numbers and one for unsigned numbers. This issue comes up over and over again in assembly language.

In the C language, integers may be declared as *unsigned int* or as *signed int*. The unspecified *int* declaration means the same as *signed int*.

# 3.7 Subtraction Using Negation

This section explains how subtraction may be done using the circuits described so far.

## 3.7.1 Two's Complementation

Since we have an adder that works with negatives, we should be able to use it to do subtractions, such as 5 - 3, since

5 − 3 = 5 + (−3)

But there is a problem. Converting 3 to -3 is not as easy as just sticking on a minus sign or flipping a bit. If it were, tables such as Table 3.8 and Table 3.9 would not be necessary. Although we do have a formula which explains these tables, it is unfortunately based on subtraction. For example, according to the formula for the four-bit table, to get the negative of 3, you subtract 3 from 16. But since our goal is to find a way to do subtraction, we appear to be trapped in a vicious circle. The situation is not as bad as it seems, however. Subtracting 3 from 16 in binary can be done even if we don't know how to subtract and even though the binary representation of 16 requires one more bit than our four-bit registers can hold. We are saved by two facts.

- 16 − x = (15 − x) + 1.
- Subtracting from 15 can be done by just flipping the bits. Notice what happens when we subtract 3 from 15 in binary.

```
  1111
- 0011
------
  1100
```

The bits in 0011 are flipped and we get 1100. We have hardware that can flip bits. We can feed each bit into a NOT gate. Adding 1 then gives the result.

```
  1100
+    1
------
  1101
```

The unused input carry on the addition circuit comes into its own here. (See section 3.4.) It's just what's needed to add 1 to a total. The process of flipping the bits and adding one is called two's complementation. It subtracts a number from the turnover value. The turnover value for an n-bit two's complement number is $2^n$. If n = 4, this value is 16.

So we may do 5 - 3 as an addition

```
  0101
+ 1101
------
  0010
```

or to really see how the computer does it,

```
     1
  0101
+ 1100
-------
  0010
```

The final carry bit is ignored. That is how a computer subtracts 3 from 5.

The use of the word *complement* is justified by the fact that

$$ 16 - (16 - x) = x $$

Note that this faithfully reflects the fact that

$$ -(-x) = x $$

## 3.7.2 Two's Complementation in Hex

The two's complement process is done by flipping the bits and adding one. If we think of flipping the bits of a hex digit, we see that this can be done by subtracting from 15. To do the two's complement of a number in hex then, we can subtract each of its digits from fifteen and then add one. For example, given an eight-bit number 23H,

```
 FF    DC
 - 23  and then  +1
------     -----
  DC    DD
```

Hence the two's complement of 23H is DDH. On the other hand if we use the fact that finding the two's complement is really subtraction from the turnover value, we can just do the subtraction.

```
 100
-  23
------
  DD
```

## 3.7.3 Conversions

When debuggers display register contents for us, negatives will be shown to us in hex. Consequently, it is worthwhile to become handy with two's complement values in hex. Suppose we are shown the 16-bit value FF42H, and we would like to know what value it represents. First we observe that if we take this to be a signed number, then it is negative since its first bit is 1 — if the first hex digit is any of the hex digits 8, 9, A, B, C, D, E, or F, then the first binary digit is 1. To find the corresponding positive number, we can perform the two's complement in hex.

```
 10000
- FF42
------
   BE
```

And BEH is $11 \times 16 + 14 = 190$. Consequently, the represented value is -190.

You could also convert everything to binary, take the two's complement, and then convert to decimal. Of course you could also convert FF42H to decimal and subtract the result from 65,536! Probably working in hex as much as you can is the easiest.

# 3.8 Placeholdering Two's Complement

Two's complement can be thought of as a placeholdering system. If the place value of the most significant bit is thought of as standing for the negative of its ordinary binary value, then this yields a place value interpretation for two's complement numbering. Table 3.11 shows the place values in the four-bit two's complement system. Using the table, we see that -5 can be expressed as (-8) + 2 + 1.

Table 3.11. Four-Bit Two's Complement Place Values

| -8s | 4s | 2s | 1s | Binary | Decimal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 1 | 1 | 1111 | -1 |
| 1 | 1 | 1 | 0 | 1110 | -2 |
| 1 | 1 | 0 | 1 | 1101 | -3 |
| 1 | 1 | 0 | 0 | 1100 | -4 |
| 1 | 0 | 1 | 1 | 1011 | -5 |
| 1 | 0 | 1 | 0 | 1010 | -6 |
| 1 | 0 | 0 | 1 | 1001 | -7 |
| 1 | 0 | 0 | 0 | 1000 | -8 |
| 0 | 1 | 1 | 1 | 0111 | 7 |
| 0 | 1 | 1 | 0 | 0110 | 6 |
| 0 | 1 | 0 | 1 | 0101 | 5 |
| 0 | 1 | 0 | 0 | 0100 | 4 |
| 0 | 0 | 1 | 1 | 0011 | 3 |
| 0 | 0 | 1 | 0 | 0010 | 2 |
| 0 | 0 | 0 | 1 | 0001 | 1 |

# 3.9 Memory Circuits

The latch circuit shown in Figure 3-7 has the property that if a logic 0 is applied to the Freeze/Copy# line, then the value on the Input propagates through to the Output. On the other hand, if a logic 1 is applied to the Freeze/Copy# line, then the Output signal is held to whatever value it had at the time of the “freeze.” This value is in storage and the input is ignored.

![](img/a3d6758e6e21b80b35e1b981ecbc1234_44_0.png)

To see how this circuit might serve as one bit of a memory circuit, imagine many of these circuits arranged in a rectangle, each row forming a word of memory. Each row would respond to a selection signal picking that row out from all the other rows in memory. The memory would be required to remain dormant whenever the selection signal was not present. To use this circuit as one bit of a memory, let us suppose we have a W/R# control signal and a selection signal, Sel. W stands for write, which means that the processor wants to write to the memory circuit. R stands for read and means that the processor wants to read from the memory circuit. All the circuits in the entire memory will be connected to the same W/R# signal, but only the circuits in the same word are connected to a single Sel signal.
