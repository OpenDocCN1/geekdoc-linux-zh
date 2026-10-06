# CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

```
4 rsble r0,%[rp2val],#32

```

Perform the multiply, storing the upper portion of the product in r5 and
lower portion of the product in r4.

```
5 smull r4, r5,%[op1val],%[op2val]

```

Shift the lower half of the product using conditional shift instructions,
shifting by the greater of the radix point positions. Use the s-suffix to retain
t last bit shifted—the round bit—in the carry flag. This behavior is
supported when using shift instructions or using the flexible second
operand with the movs, mvns, andrs, eors, bics, teq, or tst
instructions.

```
6 lsrgts r2, r4,%[rp1val]

```

```
7 lsles r2, r4,%[rp2val]

```

Using the flexible second operand, left-shift the upper half of the product
the distance previously calculated in r0, and using a bitwise OR to merge
with the previously shifted value.

```
8 or r2, r5,lsl0

```

Round up the last shifted-off bit from the lower half of the product.
t carry flag is not changed if the shift amount is zero, in which case
t carry flag would remain in the state that resulted from the cmp instru-
ions. As a result this macro will not produce results if both radix point
positions are zero.

```
9 addhs r2, r2,#1

```

Line 6 sets the value of r1 to −1 when the radix point positions are equal
t to cancel the result of operation. Apply this correction now.

```
10 mov %[resval],r1

11 [resval]="res)

12 [op1val]="r(op1),[op2val]="r(op2)

13 [rp1val]="r(rp1),[rp2val]="r(rp2):

14 "r0","r1","r2","r4","r5",
```

# 3.6.7 Determining radix point position

The radix point should be placed to accommodate the range and the accu-
racy requirements of the application. The range is determined by the number
bits to the left of the radix point. The accuracy is determined by the num-
ber bits to the right of the radix point.