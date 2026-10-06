Although this seems to violate our rule about always quoting shell variables that are arguments to test, it's better to omit the quotes if you're sure that the variable is not null (and not composed entirely of whitespaces characters).

You can test to see whether a shell variable has a null value with the third operator listed in Table 7.1:

```
test $day*
```

This returns TRUE if day is not null and FALSE if it is. Quotes are not necessary here because test doesn't care whether it sees an argument in the shell case. Nevertheless, you are better off using them as well if the variable consists entirely of whitespaces characters, the shell will get rid of the argument if it's not enclosed in quotes.

```
$ blanks "  "
$ test $blanks          Is it not null?
$ echo ?               False—it's null
1
$ test "$blanks"      And now?
$ echo ?               0
$                       True—it's not null
```

In the first case, test was not passed any arguments because the shell ate up the four spaces in blanks. In the second case, test got one argument consisting of four space characters which is not null.

In case we seem to be elaborating the point about blanks and quotes, realize that this is a frequent source of shell programming errors. It's good to really understand the principles to save yourself a lot of programming headaches in the future.

There is another way to test whether a string is null, and with either of the last two operators listed previously in Table 7.1. The -n operator returns an exit status of zero if the argument is not null. Think of this operator as testing for nonzero length.

The -z operator tests the argument that follows to see whether it is null and returns an exit status of zero if it is true. Think of this operator as testing to see whether the following argument has zero length.

So the command

```
test -n $day*
```

returns an exit status of 0 if day contains at least one character. The command

```
test -z $dataflag
```

returns an exit status of 0 if dataflag doesn't contain any characters. That is, -n and -z are the opposite of each other, and both exist to make it easier to clear, readable conditional statements.