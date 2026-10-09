Table 27-8 Arithmetic operators (continued)

| Type of operator/operator | Function |
| :--- | :--- |
| Boolean (logical) | && Boolean AND | | | Boolean OR |
| Conditional evaluation | ?: Ternary operator |
| Assignment | =, *=, /=, %=, +=, -=, <<, >>, &=, |=, ^= |
| Comma | , Comma |

# Pipeline symbol

The | control operator has higher precedence than arithmetic operators. For example, the command line

```
$ cmd1 | cmd2 | | cmd3 | cmd4 && cmd5 | cmd6
```

is interpreted as if you had typed

```
$ ((cmd1 | cmd2) | | (cmd3 | cmd4)) && (cmd5 | cmd6)
```

# Do not rely on rules of precedence: use parentheses

Do not rely on the precedence rules when you use command lists (page 162). Instead, use parentheses to explicitly specify the order in which you want the shell to interpret the commands.

# Increment and decrement

The postincrement, postdecrement, preincrement, and predecrement operators work with variables. The pre- operators, which appear in front of the variable name (as in ++COUNT and --VALUE), first change the value of the variable (++ adds 1; -- subtracts 1) and then provide the result for use in the expression. The post- operators appear after the variable name (as in COUNT++ and VALUE--); they first provide the unchanged value of the variable for use in the expression and then change the value of the variable.

```
$ N=10
$ echo $N
10
$ echo $(--N+3))
12
$ echo $N
9
$ echo $((N++ - 3))
6
$ echo $N
10
```