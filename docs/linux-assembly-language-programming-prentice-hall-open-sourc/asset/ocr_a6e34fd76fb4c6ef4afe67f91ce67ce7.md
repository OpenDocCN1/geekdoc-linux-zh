This section explains how subtraction may be done using the circuits described so far.

# 3.7.1 Two's Complementation

Since we have an adder that works with negatives, we should be able to use it to do subtractions, such as 5 - 3, since

5 − 3 = 5 + (−3)

But there is a problem. Converting 3 to -3 is not as easy as just sticking on a minus sign or flipping a bit. If it were, tables such as Table 3.8 and Table 3.9 would not be necessary. Although we do have a formula which explains these tables, it is unfortunately based on subtraction. For example, according to the formula for the four-bit table, to get the negative of 3, you subtract 3 from 16. But since our goal is to find a way to do subtraction, we appear to be trapped in a vicious circle. The situation is not as bad as it seems, however. Subtracting 3 from 16 in binary can be done even if we don't know how to subtract and even though the binary representation of 16 requires one more bit than our four-bit registers can hold. We are saved by two facts.

+   i. 16-x = (15-x) + 1.

i) 16 − x = (15 − x) + 1.

+   ii. Subtracting from 15 can be done by just flipping the bits. Notice what happens when we subtract 3 from 15 in binary.

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