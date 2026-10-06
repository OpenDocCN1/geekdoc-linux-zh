# CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

In order to align the radix point before adding, the code must first identify operand's radix point is further to the left and shift this to the right by the difference in radix point positions. Afterward, the values are added and sum will have a radix point at the same position as the operand having the highest radix point.

For example, assume the following values:

```
op1=0110.011 (rp=3) (=6.375_{10})
op2=01.01111 (rp=5) (=1.46875_{10})
```

In order to align the radix points, shift op0 one to the right:

```
op1=0110.011 (rp=3) (=6.375_{10})
op2=0001.011 (rp=3) (=1.375_{10},2bitsshiffedoff=11)
sumwithinf.precision=0111.11011 (=7.84375_{10})
computedsum(round down)=0111.11102 (=7.09375_{10})
computedsum(roundup)=0111.11111 (=7.875_{10}) error=0.03125
```

The sum with infinite precision is 7.750_{10} but assuming a difference of the value having the rounded is dropped as a result of shifting off (0.000112=0.09375_{10}).

When the most significant (left-most) bit shifted out is 1, the result should be rounded up by adding one into the rightmost bit position once the radix point has been repositioned.

The following preprocessor macro performs this behavior. The macro assumes that the sum and both operands are allocated 32-bit variables.

```
#define ADDDF(res,op1,op2,rp1,rp2)
res = (rp1 > rp2) ? \
((op1>>(rp1-rp2)) + (op2>>(rp1-rp2-1))) : \
(op1+(op2>>(rp2-rp1)) + (op2>>(rp2-rp1-1)));
```

Shifting one of the operands right prior to adding is a natural usage of ARM's flexible second operand. As shown in the compiler-generated code below, the compiler takes advantage of this feature.

The compiler's code begins with rp1 and rp2 loaded into registers r0 and r5. It compares these values and the resulting status to calculate the difference as rp1–rp2 or rp2–rp1. After this shifts the operand with the greatest radix point twice—once to align the radix point and to align the round bit—and calculates the final sum.