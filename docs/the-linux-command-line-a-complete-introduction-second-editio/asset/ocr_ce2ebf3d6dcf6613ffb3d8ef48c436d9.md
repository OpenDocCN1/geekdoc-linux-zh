| Notation | Description |
|---|---|
| 0xnumber | Hexadecimal notation. |
| base#number | number is in base. |

Here are some examples:

```
[me@linuxbox ~]$ echo $((0xff))
255
[me@linuxbox ~]$ echo $((2#11111111))
255
```

In the previous examples, we print the value of the hexadecimal number ff (the largest two-digit number) and the largest eight-digit binary (base 2) number.

# Unary Operators

There are two unary operators, + and -, which are used to indicate whether a number is positive or negative, respectively. An example is -5.

# Simple Arithmetic

Table 34-3 lists the ordinary arithmetic operators.

Table 34-3: Arithmetic Operators

| Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Integer division |
| ** | Exponentiation |
| % | Modulo (remainder) |