So, for example, if w1 and w2 are defined as unsigned int, and w3 is set equal to 2 and w4 is set equal to 7 , then the C statement

```
w4 = w3 & w1;
```

assigns the value 9 to w4 . This can be more easily seen by treating the values of w1 , w2 , and w4 as binary numbers. Assume that you are dealing with a 16-bit unsigned int of 16 bits.

Click here to view code image

```
w1 = 0001 0100 0000 0000;
w2 = 0010 1001 0000 0000;
```

If you think about the way the logical AND operator && works (true only if both operands are true), you will be able to more easily remember the way the bitwise AND operator works. Incidentally, make sure that you don't get these two operators confused! The logical AND operator && is used in logical expressions for producing a true/false result; it does not perform a bitwise AND. Bitwise ANDing is frequently used for masking operations. That is, this operator can be used to easily set specific bits of a data item to 0. For example, the statement

```
w5 = w1 & 3;
```

assigns to w5 the value of w1 bitwise ANDed with the constant 3. This has the effect of setting all of the bits in w1 , other than the rightmost two bits, to 0, and of preserving the rightmost two bits from w1 . As with all binary arithmetic operators in C, the binary bit operators can also be used as assignment operators by tacking on an equal sign. So the statement

```
w5 &= w1;
```

performs the same function as

```
w5 = w5 & w1;
```

and has the effect of setting all but the rightmost four bits of w5 to 0. When using constants in performing bitwise operations, it is usually more convenient to express the constants in either octal or hexadecimal notation. The choice as to which to use is usually influenced by the size of the data with which you are dealing. For example, when dealing with 32-bit computers, hexadecimal notation is often used because 32 is an even multiple of 4 (the number of bits in a hexadecimal digit). Program 11.1 is presented to illustrate the bitwise AND operator. Because you are dealing with only positive values in this program, all integers have been declared as unsigned int variables.

# Program 11.1 The Bitwise AND Operator

Click here to view code image

```
/
#
{

```