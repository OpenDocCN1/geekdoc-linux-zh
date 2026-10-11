```
_latinl 0x61 = 'A' → 1
CONVERT(0x61 USING latinl) = 'A' → 1
```

Some operators force conversion of the operands to the type expected by the operator, no matter what the type of the operands is. Arithmetic operators are an example of this. They expect numbers, and the operands are converted accordingly:

```
3 + 4 → 7
'3' + 4 → 7
'3' + '4' → 7
```

In a string-to-number conversion, it's not enough for a string simply to contain a number somewhere. MySQL doesn't look through the entire string hoping to find a number; it looks only at the beginning; if the string has no leading numeric part, the conversion result is 0.

```
'1973-2-4' + 0 → 1973
'12:14:01' + 0 → 12
'23-skidoo' + 0 → 23
'-23-skidoo' + 0 → -23
'carbon-14' + 0 → 0
```

MySQL's string-to-number conversion rule converts numeric-looking strings to floating-point values:

```
'-428.9' + 0 → -428.9
'3E-4' + 0 → 0.0003
```

This conversion does not work for hexadecimal-looking constants, though. Only the leading zero is used:

```
'0xE' + 0 → 0
```

The bit operators are even stricter than the arithmetic operators. They want the operators to be not just numeric, but integers, and type conversion is performed accordingly. This means that a fractional number such as 0.3 is not considered true, even though it's non-zero; that's because when it's converted to an integer, the result is 0. In the following expressions, the operands are not considered true until they have a value of at least 1:

```
0.3 | .04 → 0
1.3 | .04 → 1
0.3 & .04 → 0
1.3 & .04 → 0
1.3 & 1.04 → 1
```

Pattern matching operators expect to operate on strings. This means you can use MySQL's pattern matching operators on numbers because it will convert them to strings in the attempt to find a match!

```
12345 LIKE '1%' → 1
12345 REGEXP '1.*5' → 1
```