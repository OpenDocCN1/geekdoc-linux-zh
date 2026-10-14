```
[me@linuxbox ~]$ ul-param aBc
abc
aBc
ABC
ABc
```

Again, we process the first command line argument and output the four variations supported by the parameter expansions. While this script uses the first positional parameter, parameter may be any string, variable, or string expression.

# Arithmetic Evaluation and Expansion

We looked at arithmetic expansion in Chapter 7. It is used to perform various arithmetic operations on integers. Its basic form is as follows:

```
$((expression))
```

where expression is a valid arithmetic expression.

This is related to the compound command (( )) used for arithmetic evaluation (truth tests) we encountered in Chapter 27.

In previous chapters, we saw some of the common types of expressions and operators. Here, we will look at a more complete list.

# Number Bases

In Chapter 9, we got a look at octal (base 8) and hexadecimal (base 16) numbers. In arithmetic expressions, the shell supports integer constants in any base. Table 34-2 shows the notations used to specify the bases.

Table 34-2: Specifying Different Number Bases

| Notation | Description |
|---|---|
| number | By default, numbers without any notation are treated as decimal (base 10) integers. |
| 0number | In arithmetic expressions, numbers with a leading zero are considered octal. |