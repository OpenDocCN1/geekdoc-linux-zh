variable is not defined or contains a NULL string, its value is assumed to be zero. So if we have
not assigned any value yet to the variable a, we can still use it in an integer expression:

```
$ echo $a
$ echo $(( a = a + 1 ))
$ 1
$ echo $a
```

Variable a not set
Equivalent to a = 0 + 1
Now a contains 1

```
1
$
```

Note that assignment is a value operator, and the value of the assignment is substituted in the
second echo command in the preceding example.

Parentheses may be freely used inside expressions to force grouping, as in

```
$ echo $(( (i + 10) * j ))
```

If you want to perform an assignment without echo or some other command, you can
assignment before the arithmetic expansion.

To multiply the variable i by 5 and assign the result back to i you can

```
i=$(( i * 5 ))
```

Note that spaces are optional inside the double parentheses, but are not allowed when the
assignment is outside them.

A more succinct way to multiply i by 5 is the following common notation, which would
appear within another statement:

```
$(( i * 5 ))
```

If you're just adding 1 to the value, you can be even more succinct:

```
$(( i++ ))
```

Finally, to see whether i is greater than 0 or less than 0 and equal to or 100, you can
write

```
result=$(( i >= 0 && i <= 100 ))
```

which assigns result the value of 1 (true) if the expression is true or (false) if it's:

```
$ i=$(( 100 * 200 / 10 ))
$ j=$(( i < 1000 ))
$ echo $j
```

If i < 1000, set j = 0; otherwise

```
2000 0
$
i is 2000, so j was set to
```

This concludes our introduction to writing commands and using variables. The next chapter
goes into detail on the various quoting mechanisms in the shell.