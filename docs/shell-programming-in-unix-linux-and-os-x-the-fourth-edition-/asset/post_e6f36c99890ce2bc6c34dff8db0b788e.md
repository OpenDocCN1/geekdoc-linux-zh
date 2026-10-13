
```text
$ value1=10
$ value2=$value1
$ echo $value2
10
$
```

*Didn't do that right*

*That's better*

Remember that a dollar sign must always be placed before the variable name whenever you want to use the value stored in that variable.

## Undefined Variables Have the Null Value

What do you think happens when you try to display the value of a variable that has no value assigned to it? Try it and see:

```text
$ echo $nosuch
$
```

*Never assigned a value*

You don't get an error message. Did the `echo` command display anything at all? Let's see whether we can more precisely determine that:

```text
$ echo :$nosuch:
::
$
```

*Surround its value with colons*

So you see no characters were substituted by the shell for the unspecified value of `nosuch`.

A variable that contains no value is said to be undefined and contain the null value. It is the default case for variables that you never store values in. When the shell performs its variable substitution, any values that are null are effectively just removed from the command line (which makes sense if they have the null value):

```text
$ wc -l $nosuch names
      7 names
$
```

The shell scans the command line substituting the null value for the variable `nosuch`. After the scan is completed, the line effectively looks like this:

```text
wc -l names
```

which explains why it works.

Sometimes you may want to initialize the value of a variable to be the value null. This can be done by simply assigning no value to the variable, as in

```text
dataflag=
```

Alternatively, and as a better practice, you can list two adjacent pairs of quotes after the `=`. So

```text
dataflag=""
```

and

```text
dataflag=''
```

both have the same effect of assigning the null value to `dataflag` and have the added benefit that it looks like it's deliberate, rather than in the first instance where it might be perceived later as a mistake or typo.

Be advised that the assignment

```text
dataflag=" "
```

is not equivalent to the three previous ones because it assigns a single space character to `dataflag`; that's different from assigning *no* characters to it.

## Filename Substitution and Variables

Here's a puzzle for you: If you type

```text
x=*
```

will the shell store the character `*` into the variable `x`, or will it store the names of all the files in your current directory into the variable `x`? Let's try it out and see:

> *What files do we have?*

```text
$ ls
addresses
intro
logspaces
names
nu
numbers
phonebook
stat
$ x=*
$ echo $x
addresses intro logspaces names nu numbers phonebook stat
$
```

There's a lot to be learned from this simple example. Was the list of files stored into the variable `x` when

```text
x=*
```

was executed, or did the shell do the substitution when

```text
echo $x
```

was executed?

It turns out that the shell does not perform filename substitution when assigning values to variables. Therefore,

```text
x=*
```

assigns the single character `*` to `x`. This means that given the output shown, the shell must have done the filename substitution when executing the `echo` command. In fact, the precise sequence of steps that occurred when

```text
echo $x
```

was executed is as follows:

1. The shell scanned the line, substituting `*` as the value of `x`.
2. The shell rescanned the line, encountered the `*`, and then substituted the names of all files in the current directory.
3. The shell initiated execution of `echo`, passing it the file list as arguments (see Figure 4.3).

![](img/29b87b4d3daf7eb41fe5066130730f4c_121_0.png)

Figure 4.3  *echo $x*

This order of evaluation is important. Remember, first the shell does variable substitution, then does filename substitution, and then parses the line into arguments.

## The `${variable}` Construct

Suppose that you have the name of a file stored in the variable `filename`. If you wanted to rename that file so that the new name was the same as the old, except with an X added to the end, your first impulse would be to type

```text
mv $filename $filenameX
```

When the shell scans this command line, however, it substitutes the value of the variable `filename` and also the value of the variable `filenameX`. The shell thinks `filenameX` is the full name of the variable because it's composed entirely of valid characters.

To avoid this problem, delimit the variable by enclosing the entire name (but not the leading dollar sign) in curly braces, as in

```text
${filename}X
```

This removes any ambiguity, and the `mv` command then works as desired:

```text
mv $filename ${filename}X
```

Remember that the braces are necessary only if the last character of the variable name is followed by an alphanumeric character or an underscore.

There are also quite a few other functions applicable to variables within this curly brace notation, including extracting subsets, assigning values if the variable is currently unassigned, and more. Stay tuned for those!

## Built-in Integer Arithmetic

The POSIX standard shell as included with all modern Unix and Linux variants (including Mac OS X's command shell) provides a mechanism for performing integer arithmetic on shell variables called *arithmetic expansion*. Note that some older shells do not support this feature.

The format for arithmetic expansion is

```text
$((expression))
```

where *expression* is an arithmetic expression using shell variables and operators. Valid shell variables are those that contain numeric values (leading and trailing whitespace is allowed). Valid operators are taken from the C programming language and are listed in Appendix A, "Shell Summary."

> **$(( )) Operators**
>
> There is a surprisingly extensive list of operators, including the basic six: `+`, `-`, `*`, `/`, `%` and `**`, along with more sophisticated notations including `+=`, `-=`, `*=`, `/=`, easy increment and decrement with `variable++` and `variable--`, and more.
>
> Our favorite? You can work with different numerical bases and even convert from one number base to another. For example, here are the answers to what 100 octal (base 8) and 10101010101010101010 binary (base 2) are in decimal:
>
> ```sh
> $ echo $(( 8#100 ))
> 64
> $ echo $(( 2#10101010101010101010 ))
> 174762
> ```

The result of computing *expression* is substituted on the command line. For example,

```text
echo $((i+1))
```

adds one to the value in the shell variable `i` and prints the result. Notice that the variable `i` doesn't have to be preceded by a dollar sign because the shell knows that the only valid elements that can appear in arithmetic expansions are operators, numbers, and variables. If the variable is not defined or contains a NULL string, its value is assumed to be zero. So if we have not assigned any value yet to the variable `a`, we can still use it in an integer expression:

```text
$ echo $a                         Variable a not set
$ echo $(( a = a + 1 ))           Equivalent to a = 0 + 1
1
$ echo $a                         Now a contains 1
$
```

Note that assignment is a valid operator, and the value of the assignment is substituted in the second `echo` command in the preceding example.

Parentheses are frequently useful inside expressions to force grouping, as in

```text
echo $((i = (i + 10) * 3))
```

If you want to perform an assignment without `echo` or some other command, you can move the assignment before the arithmetic expression.

So to multiply the variable `i` by 5 and assign the result back to `i` you can write

```text
i=$(( i * 5 ))
```

Note that spaces are optional inside the double parentheses, but are not allowed when the assignment is outside them.

A more succinct way to multiply `$i` by 5 is the following common notation, which would appear within another statement:

```text
$(( i *= 5 ))
```

If you're just adding 1 to the value, you can be even more succinct:

```text
$(( i++ ))
```

Finally, to test to see whether `i` is greater than or equal to 0 and less than or equal to 100, you can write

```text
result=$(( i >= 0  &&  i <= 100 ))
```

which assigns `result` the value of 1 (true) if the expression is true or 0 (false) if it's false:

```text
$ i=$(( 100 * 200 / 10 ))       If i is < 1000, set j = 0; otherwise 1
$ j=$(( i < 1000 ))              i is 2000, so j was set to 0
$ echo $i $j
2000 0
$
```

That concludes our introduction to writing commands and using variables. The next chapter goes into detail on the various quoting mechanisms in the shell.
