# Number Bases

Back in Chapter 9, we got a look at octal (base 8) and hexadecimal (base 16) numbers. In arithmetic expressions, the shell supports integer constants in any base.

Table 34-2: Specifying Different Number Bases

| Notation | Description |
|---|---|
| *number* | By default, numbers without any notation are treated as decimal (base 10) integers. |
| *0number* | In arithmetic expressions, numbers with a leading zero are considered octal. |
| *0xnumber* | Hexadecimal notation |
| *base#number* | *number* is in *base* |

Some examples:

```
[me@linuxbox ~]$ echo $((0xff))
255
[me@linuxbox ~]$ echo $((2#11111111))
255
```

In the examples above, we print the value of the hexadecimal number ff (the largest two-digit number) and the largest eight-digit binary (base 2) number.

# Unary Operators

There are two unary operators, the + and -, which are used to indicate if a number is positive or negative, respectively. For example, -5.

# Simple Arithmetic

The ordinary arithmetic operators are listed in the table below:

Table 34-3: Arithmetic Operators

| Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |