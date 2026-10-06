# The test Command 141

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