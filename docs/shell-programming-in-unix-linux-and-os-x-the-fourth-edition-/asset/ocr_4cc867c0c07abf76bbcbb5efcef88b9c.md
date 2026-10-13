precedes any other character inside double quotes, the backslash is ignored by the shell and passed on to the program:

```
```shell
$ echo "\$x"
$x
$ echo "\\ is the backslash character"
\\ is the backslash character
$ x=5
$ echo "The value of x is \"$x\""
The value of x is "5"
$
```
```

In the first example, the backslash precedes the dollar sign so the shell ignores the dollar sign, removes the backslash, and hands the result to echo. In the second example, the backslash precedes a space, not interpreted by the shell inside double quotes. So the shell ignores the backslash and passes it on to the echo command. The last example shows the backslash used to enclose double quotes inside a double-quoted string.

As an exercise in the use of quotes, let’s say that you want to display the following line at the terminal:

```
```shell
<<< echo $x >>> displays the value of x, which is $x
```
```

The intention here is to substitute the value of x in the second instance of $x, but not in the first. Let’s first assign a value to x:

```
```shell
$ x=1
$
```
```

Now try displaying the line without using any quotes:

```
```shell
$ echo <<< echo $x >>> displays the value of x, which is $x
syntax error: '<' unexpected
$
```
```

The < signals input redirection to the shell, which lacks a subsequent filename, hence the resultant error message.

If you put the entire message inside single quotes, the value of x won’t be substituted at the end. If you enclose the entire string in double quotes, both occurrences of $x will be substituted. Tricky!

Here are two different ways to properly quote the string so that everything works as desired:

```
```shell
$ echo "<<< echo \$x >>> displays the value of x, which is $x"
<<< echo $x >>> displays the value of x, which is 1
$ echo '<<< echo $x >>> displays the value of x, which is' $x
<<< echo $x >>> displays the value of x, which is 1
$
```
```

In the first case, everything is enclosed in double quotes, and the backslash is used to prevent the shell from performing variable substitution in the first instance of $x. In the second case, everything up to the last $x is enclosed in single quotes but the variable that should be substituted is added without quotes around it.