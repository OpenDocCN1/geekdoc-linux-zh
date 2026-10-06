# Part II Shell Scripting Basics

To solve this problem, you need to use the shell character (the backslash) to identify any characters that may be misinterpreted by the shell before being passed to the expr command:

```
$ expr 5 \* 2
10\$
```

Now that's really starting to get ugly! Using the expr command in a shell script is equally cumbersome:

```
#!/bin/bash
# An example of using the expr command
var1=10
var2=20
var3=`expr $var2 / $var1"
echo The result is $var3
```

To assign the result of a mathematical equation to a variable, you have to use the backtick character to extract the output from the expr command:

```
$ ./test6
The result is 2
$
```

Fortunately, the bash shell has an improvement for processing mathematical operators.

# Using brackets

The bash shell includes the expr command to stay compatible with the Bourne shell; however, it provides a much easier way of performing mathematical equations. In bash, when assigning a mathematical value to a variable, you can enclose the mathematical equation using a dollar sign and square brackets [$ operation ]]:

```
$ var=$[1 + 5]
echo $var
$ var2 = {$var * 2}
echo $var2
12
$
```

Using brackets makes math much easier than with the expr command. This same technique also works in shell scripts:

```
$ cat test7
#!//bin/bash
var1=100
```

218