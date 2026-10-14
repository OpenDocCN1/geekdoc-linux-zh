
character to uppercase (capitalization).

Here is a script that demonstrates these expansions:

```
#!/bin/bash

# ul-param - demonstrate case conversion via parameter expansion
if [[ $1 ]]; then
    echo ${1,,}
    echo ${1,}
    echo ${1^^}
    echo ${1^}
fi
```

Here is the script in action:

```
[me@linuxbox ~]$ ul-param aBc
abc
aBc
ABC
ABc
```

Again, we process the first command line argument and output the four variations supported by the parameter expansions. While this script uses the first positional parameter, parameter my be any string, variable, or string expression.

## Arithmetic Evaluation And Expansion

We looked at arithmetic expansion in Chapter 7. It is used to perform various arithmetic operations on integers. Its basic form is:

$((expression))

where expression is a valid arithmetic expression.

This is related to the compound command (( )) used for arithmetic evaluation (truth tests) we encountered in Chapter 27.

In previous chapters, we saw some of the common types of expressions and operators. Here, we will look at a more complete list.

## Number Bases

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

## Unary Operators

There are two unary operators, the + and -, which are used to indicate if a number is positive or negative, respectively. For example, -5.

## Simple Arithmetic

The ordinary arithmetic operators are listed in the table below:

Table 34-3: Arithmetic Operators

| Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Integer division |
| ** | Exponentiation |
| % | Modulo (remainder) |

Most of these are self-explanatory, but integer division and modulo require further discussion.

Since the shell's arithmetic only operates on integers, the results of division are always whole numbers:

```
[me@linuxbox ~]$ echo $(( 5 / 2 ))
2
```

This makes the determination of a remainder in a division operation more important:

```
[me@linuxbox ~]$ echo $(( 5 % 2 ))
1
```

By using the division and modulo operators, we can determine that 5 divided by 2 results in 2, with a remainder of 1.

Calculating the remainder is useful in loops. It allows an operation to be performed at specified intervals during the loop's execution. In the example below, we display a line of numbers, highlighting each multiple of 5:

```
#!/bin/bash

# modulo : demonstrate the modulo operator

for ((i = 0; i <= 20; i = i + 1)); do
    remainder=$((i % 5))
    if (( remainder == 0 )); then
        printf "\e[d" $i
    else
        printf "%d " $i
    fi
done
printf "\n"
```

| Operator | Description |
|---|---|
| `parameter = value` | Simple assignment. Assigns *value* to *parameter*. |
| `parameter += value` | Addition. Equivalent to `parameter = parameter + value`. |
| `parameter -= value` | Subtraction. Equivalent to `parameter = parameter − value`. |
| `parameter *= value` | Multiplication. Equivalent to `parameter = parameter * value`. |
| `parameter /= value` | Integer division. Equivalent to `parameter = parameter / value`. |
| `parameter %= value` | Modulo. Equivalent to `parameter = parameter % value`. |
| `parameter++` | Variable post-increment. Equivalent to `parameter = parameter + 1` (however, see discussion below). |
| `parameter--` | Variable post-decrement. Equivalent to `parameter = parameter − 1`. |
| `++parameter` | Variable pre-increment. Equivalent to `parameter = parameter + 1`. |
| `--parameter` | Variable pre-decrement. Equivalent to `parameter = parameter − 1`. |

These assignment operators provide a convenient shorthand for many common arithmetic tasks. Of special interest are the increment (++) and decrement (−−) operators, which increase or decrease the value of their parameters by one. This style of notation is taken from the C programming language and has been incorporated by several other programming languages, including bash.

The operators may appear either at the front of a parameter or at the end. While they both either increment or decrement the parameter by one, the two placements have a subtle difference. If placed at the front of the parameter, the parameter is incremented (or decremented) before the parameter is returned. If placed after, the operation is performed after the parameter is returned. This is rather strange, but it is the intended behavior. Here is a demonstration:

```
```bash
[me@linuxbox ~]$ foo=1
[me@linuxbox ~]$ echo $((foo++))
1
[me@linuxbox ~]$ echo $foo
2
```
```
