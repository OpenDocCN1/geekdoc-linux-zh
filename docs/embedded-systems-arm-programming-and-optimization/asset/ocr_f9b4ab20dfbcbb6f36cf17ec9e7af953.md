# 3.6 Fixed-Point Arithmetic 129

![](bbox=[0.147, 0.115, 0.651, 0.303])

**FIGURE 3.3** two (32,16) values multiplied to produce (64,32) product. To convert the product to a (32,16) value, the lower 16 bits of r5 and the upper 16 bits of r4 need to be combined into a single register. To do this, the compiler uses shift operations to isolate the bits and uses an OR instruction to combine them into a single register.

4 addhs r2, r2, #1

To implement a general macro for fixed-point multiply of operands having an arbitrary radix point position, the code must decide where to place the radix point of the product.

A common method is to set the radix point of the product to match the operand and having the rightmost point. To do this, the code will shift the product to the right by the position of the left-most radix point.

The macro has the same arguments as the fixed-point addition: a result, to which the product is assigned, two operands, and the corresponding radix point positions of each operand. By this code assumes that the product and both operands are allocated as 32-bit variables. This code also assumes that both radix points are non-negative and only one can be zero.

```
#define MULTFP(res,op1,op2,rp1,rp2)
```

First, compare the radix point positions. The cmp instruction sets the flag bits as a subtract instruction; if the first value is greater or equal to the second value, then the carry flag will be set to one and zero otherwise. This is because all subarrays produce a carry out except when resulting in a difference that would result in an underflow.

```
asm("cmp %%[rplval],%%[rpval]\n\t"
```

Compute the left-shift value, which is the difference between 32 and the position of the left-most radix point position. Since calculation depends on which radix point position is further left, use conditional instructions.

```
rsbt r0,%%[rplval],%%#32\n\t"
```