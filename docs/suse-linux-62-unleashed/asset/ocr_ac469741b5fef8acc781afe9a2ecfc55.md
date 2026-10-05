# SuSE Linux Programming Tools
CHAPTER 25 803

You could, of course, do them separately, but setting multiple values often saves time during coding.

> Note
In Python, a variable's type is set by the operations performed on it. In any mathematical operation, if any of the variables are floating point, all variables are converted to floating point automatically.

If you are typing a compound expression, such as an if or for loop, the command-line interpreter switches the prompt to a set of three dots, allowing you to complete the expression:

```
>>> if b < 10:
```

... After the three dots, you can complete the compound expression. Be sure to indent the compound expression.

To start Python executing a file, supply the name as an argument. If the program needs any arguments, they can be specified on the command line too. For example, the following command starts the Python executable running the program big_prog, using the three arguments following the program name in the program:

```
python big_prog 12 24 36
```

You'll see how these arguments are read later in this section.

Python supports unlimited precision numbers. By default, numbers are tracked only to a considerable number of significant digits, appending an L to the number switches to unlimited precision mode, as the following example shows:

```
>>> 123456789 * 123456789
Traceback (innermost last):
File "interactive input", line 0, in ?
OverflowError: integer multiplication
>>> 123456789L * 123456789L
1524157875190521L
>>>
```

The first multiplication overflowed the allowed number of digits and generated an error message. By appending the L to the end of the numbers (with no spaces between the number and the L), you can impose unlimited precision. .py (such as primes.py and

![](bbox=[0.885, 0.693, 0.973, 0.943])