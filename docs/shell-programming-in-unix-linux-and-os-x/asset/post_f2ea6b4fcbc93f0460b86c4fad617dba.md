
# The test Command

Be warned that both of the preceding operators expect an argument to follow, so get into the habit of enclosing the argument within double quotes.

```
$ nullvar=
$ nonnullvar=abc
$ test -n "$nullvar"
$ echo $?
```

Does nullvar have nonzero length?

```
1
$ test -n "$nonnullvar"
$ echo $?
```

No
And what about nonnull?

```
0
$ test -z "$nonnullvar"
$ echo $?
```

Yes
Does nullvar have zero length?

```
1
$ test -z "$nonnullvar"
$ echo $?
```

Yes
And nonnull?
No

Note that test can also be picky about its arguments. For example, if the shell variable $symbol contains an equals sign, look at what happens if you try to test it for length:
$ echo $symbol

```
$ test -z "$symbol"
sh: test: argument expected
$
```

The operator has higher precedence than the -z operator, so test attempts to process the command as an equality test, and expects an argument to follow the =. To avoid this sort of problem, many shell programmers write their test commands as

test X"$symbol" = X

which will be true if symbol is null, and if it's not. The X in front of symbol prevents test from interpreting the characters stored in symbol as an operator.

# An Alternate Format for test

The test command is used so often by shell programmers that an alternative format of the command is available and can make your programs a lot cleaner. This improves the readability of if statements and other conditional tests throughout your shell scripts.

You'll recall the general format of the test command is

```
test expression
```

This can also be expressed in the alternative format as

```
[ expression ]
```

The [ is actually the name of the command (who said anything about command names having to be alphanumeric characters?). It initiates execution of the same test command, but when used this way it expects a closing ] at the end of the expression. Spaces must appear after the [ and before the ].

You can rewrite the test command in a previous example with this alternative format as:

```
$ -z "$nullvar" 
$ echo $?
1
$
```

When used in an if command, the alternative format looks like this:

```
if ["name" = julio ]
then
echo "Would you like to play a game"
fi
```

Which format of the if command you use is up to you; we prefer the [...] format, which coaxes shell programming into a syntax much more similar to other popular programming languages, so that's what we'll use throughout the remainder of the book.

# Integer Operators

test has a large assortment of operators for performing integer comparisons. Table 7.2 summarizes these operators.

| Operator | Returns TRUE (exit status of 0) if |
| --- | --- |
| int₁ -eq int₂ | int₁ is equal to int₂ |
| int₁ -ge int₂ | int₁ is greater than or equal to int₂ |
| int₁ -gt int₂ | int₁ is greater than int₂ |
| int₁ -le int₂ | int₁ is less than or equal to int₂ |
| int₁ -lt int₂ | int₁ is less than int₂ |
| int₁ -ne int₂ | int₁ is not equal to int₂ |

For example, the operator -eq tests to whether two integers are equal. So if you had a shell variable called count and you wanted to see whether its value was equal to zero, you would write

```
[ "$count" -eq 0 ]
```

# The test Command

Other integer operators behave similarly, so

```
[ "$choice -lt 5 ]
```

tests to see whether the variable choice is less than 5.

The command

```
[ "$index -ne "$max" ]
```

tests to see the value of index is not equal to the value of max.

Finally

```
[ "$# -ne 0 ]
```

tests to see the number of arguments passed to the command is not equal to zero.

It's important to note that the test command, not the itself, interprets the variable's value as an integer when an integer operator is used, so these comparisons regardless of the shell's type.

Let's have a closer look at the difference between test's string and integer operators with a few examples.

```
$ x1="005"
$ x2="10"
[ "$x1 = 5 ]
$ echo $?
```

String comparison

False

Integer comparison

```
$ [ "$x1" -eq 5 ]
$ echo $?
```

True

String comparison

```
$ [ "$x2" -eq 10 ]
$ echo $?
```

False

Integer comparison

True

The first test

```
[ "$x1" = 5 ]
```

uses the string comparison operator = to test the two strings are identical. They're not, because the first string is composed of the three characters 005, and the second single character 5.

In the second test, the integer comparison operator -eq is used. Treating the two values as integers (numbers), 005 is equal to 5, as verified by the test exit status.

The third and fourth tests are similar, but in these cases you can see how even a leading space stored in the variable x2 can influence a test made with a string operator versus one made with an integer operator.

# File Operators

Virtually every shell program deals with one or more files. For this reason, a wide assortment of operators are provided by test to enable you to ask questions about files. Each of these operators is unary in nature, meaning they expect a single argument to follow. In all cases, the second argument is the name of a file (and that includes a directory name, as appropriate).

Table 7.3 lists the file operators.

Table 7.3 Commonly Used test File Operators

| Operator | Returns TRUE (exit status of 0) if |
| --- | --- |
| -d file | file is a directory |
| -e file | file exists |
| -f file | file is an ordinary file |
| -r file | file is readable by the process |
| -s file | file has nonzero length |
| -w file | file is writable by the process |
| -x file | file is executable |
| -L file | file is a symbolic link |

The command

```
[ -f /users/steve/phonebook ]
```

tests whether the file /users/steve/phonebook exists and is an ordinary file (that is, not a directory or special file).

The command

```
[ -r /users/steve/phonebook ]
```

tests whether the indicated file exists and is also readable by you.

The command

```
[ -s /users/steve/phonebook ]
```

tests whether the indicated file has non-zero content (that is, isn't an empty file). This is useful if you create an error file and later want to see whether anything was written to it:

```
if [ -s $ERRFILE ]
then
echo "Errors found:"
cat $ERRFILE
fi
```

A few more test operators, when combined with the previously described operators, enable you to specify more conditional expressions.

# The Logical Negation Operator

The unary negation operator ! can be placed in front of any other test expression to negate the result of that evaluation. For example,

```
[ ! -r /users/steve/phonebook ]
```

returns a zero status (true) if /users/steve/phonebook is readable, and

```
[ ! -f "mailfile" ]
```

returns true if the file specified by $mailfile does not exist or is not an ordinary file. Finally,

```
[ ! "$x1" != "$x2" ]
```

returns true if $x1 is not identical to $x2 and is obviously equivalent to (the more confusing cousin of) the clearer conditional expression

```
[ "$x1" != "$x2" ]
```

# The Logical AND Operator -a

The operator -a performs a logical AND of two expressions and returns TRUE only if the joined expressions are both true.

```
[ -f "$mailfile" -a "$mailfile" ]
```

returns TRUE if the file specified by $mailfile is an ordinary file and is readable by you.(An extra space was placed around the -a operator to aid in the expression's readability and has no effect on its execution).

The command

```
[ "$count" -ge 0 -a "$count" -lt 10 ]
```

will be true if the variable contains an integer greater than or equal to zero but less than 10. The -a operator has lower precedence than the integer comparison operators (and the string and file operators, for that matter), meaning that the preceding expression evaluates as

```
("$count" -ge 0) -a ("$count" -lt 10)
```

as you would expect.

In some cases, it's important to know that test immediately stops evaluating an AND expression as soon as something is proven to be false, so a statement like

```
[ ! "$file" -a $(who > $file) ]
```
