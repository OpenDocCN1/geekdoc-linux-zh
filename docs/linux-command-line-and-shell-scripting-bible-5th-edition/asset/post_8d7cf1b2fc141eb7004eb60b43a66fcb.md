
## Chapter 12: Using Structured Commands

### Using Single Parentheses

When testing a condition involving a single command within an `if` statement, you can use a process substitution or a single set of parentheses. The following script demonstrates how a command inside a single parenthesis creates a subshell.

```bash
$ cat SingleParentheses.sh
#!/bin/bash
# Testing a single parentheses condition
#
echo $BASH_SUBSHELL
#
if (echo $BASH_SUBSHELL)
then
    echo "The subshell command operated successfully."
else
    echo "The subshell command was NOT successful."
fi
$
$ ./SingleParentheses.sh
0
1
The subshell command operated successfully.
$
```

When the script runs the `echo $BASH_SUBSHELL` command the first time (prior to the `if` statement), it completes the operation within the current shell. The command displays a 0, indicating there is no subshell in use. (The `$BASH_SUBSHELL` environment variable is covered in Chapter 5.) Within the `if` statement, the script performs the command in a subshell and the `echo $BASH_SUBSHELL` command shows a 1, indicating a subshell was used. This subshell operation completes successfully, triggering the `then` command.

> **WARNING**
> While you can use process lists (covered in Chapter 5) within the `if` `test` statement, unexpected results may occur. If all the process list's commands fail except the *last* command, the subshell will set the *exit status* to 0, and the commands listed under the `then` section will run.

Modifying the script slightly, here’s an example of an unsuccessful command run in a subshell:

```bash
$ cat SingleParentheses.sh
#!/bin/bash
# Testing a single parentheses condition
#
#echo $BASH_SUBSHELL
#
if (cat /etc/PASSWORD)
then
    echo "The subshell command operated successfully."
else
    echo "The subshell command was NOT successful."
fi
```

```bash
$ ./SingleParentheses.sh
cat: /etc/PASSWORD: No such file or directory
The subshell command was NOT successful.
$
```

Because the subshell command contained an incorrect filename in its operation, the exit status was not set to 0. Thus, the `else` command was triggered instead of the `then` command.

![](img/0798d50a0e5dbf1265fbda3832b3e015_320_0.png)

### Using Double Parentheses

The `(( ))` command allows you to incorporate advanced mathematical formulas in your comparisons. The `test` command allows for only simple arithmetic operations in the comparison. The double parentheses command provides more mathematical symbols, which programmers who have used other programming languages may be familiar with using. Here's the format of the double parentheses command:

```bash
(( expression ))
```

The `expression` term can be any mathematical assignment or comparison expression. Besides the standard mathematical operators that the `test` command uses, the additional operators shown in Table 12.4 are available for use in the double parentheses command.

**TABLE 12.4 The Double Parentheses Command Symbols**

| Symbol | Description |
| :--- | :--- |
| val++ | Post-increment |
| val-- | Post-decrement |
| ++val | Pre-increment |
| --val | Pre-decrement |
| ! | Logical negation |
| ~ | Bitwise negation |
| ** | Exponentiation |
| << | Left bitwise shift |
| >> | Right bitwise shift |
| & | Bitwise Boolean AND |
| \| | Bitwise Boolean OR |
| && | Logical AND |
| \|\| | Logical OR |

You can use the double parentheses command in an `if` statement, as well as in a normal command in the script for assigning values:

```bash
$ cat DoubleParentheses.sh
#!/bin/bash
# Testing a double parentheses command
# 
val1=10
#
if (( $val1 ** 2 > 90 ))
then
 (( val2 = $val1 ** 2 ))
 echo "The square of $val1 is $val2,"
 echo "which is greater than 90."
#
fi
$
$ ./DoubleParentheses.sh
The square of 10 is 100,
which is greater than 90.
$
```

Notice that you don't need to escape the greater-than symbol in the expression within the double parentheses. This is yet another advanced feature besides the double parentheses command.

### Using Double Brackets

The *double bracket* command provides advanced features for string comparisons. Here's the double bracket command format:

```bash
[[ expression ]]
```

The double bracketed expression uses the standard string comparison used in the test evaluations. However, it provides an additional feature that the test evaluations don't—*pattern matching*.

> Double brackets work fine in the Bash shell. Be aware, however, that not all shells support double brackets.

In pattern matching, you can define a regular expression (discussed in detail in Chapter 20, "Regular Expressions") that's matched against the string value:

```bash
$ cat DoubleBrackets.sh
#!/bin/bash
# Using double brackets for pattern matching
#
#
if [[ $BASH_VERSION == 5.* ]]
then
 echo "You are using the Bash Shell version 5 series."
fi
$ ./DoubleBrackets.sh
You are using the Bash Shell version 5 series.
$
```

Notice in the preceding script that double equals signs (==) are used. These double equals signs designate the string to the right (5.*) as a pattern, and pattern matching rules are applied. The double bracket command matches the `$BASH_VERSION` environment variable to see whether it starts with a `5.` string. If so, the comparison succeeds, and the shell executes the `then` section commands.

### Considering the Case Command

Often, you'll find yourself trying to evaluate a variable's value, looking for a specific value within a set of possible values. In this scenario, you end up having to write a lengthy `if-then-else` statement, like this:

```bash
$ cat LongIf.sh
#!/bin/bash
# Using a tedious and long if statement
#
if [ $USER == "rich" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit."
elif [ $USER == "barbara" ]
then
    echo "Hi there, $USER"
    echo "We're glad you could join us."
elif [ $USER == "christine" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit."
elif [ $USER == "tim" ]
then
    echo "Hi there, $USER"
    echo "We're glad you could join us."
elif [ $USER == "testing" ]
then
    echo "Please log out when done with test."
else
    echo "Sorry, you are not allowed here."
fi
$ ./LongIf.sh
Welcome christine
Please enjoy your visit.
$
```

The `elif` statements continue the `if-then` checking, looking for a specific value for the single comparison variable.

Instead of having to write all the `elif` statements to continue checking the same variable value, you can use the `case` command. The `case` command checks multiple values of a single variable in a list-oriented format:

```bash
case variable in
    pattern1 | pattern2) commands1;;
    pattern3) commands2;;
    *) default_commands;;
esac
```

The `case` command compares the variable specified against the different patterns. If the variable matches the pattern, the shell executes the commands specified for the pattern. You can list more than one pattern on a line, using the bar operator to separate each pattern. The asterisk symbol is the catch all for values that don't match any of the listed patterns. Here's an example of converting the `if-then-else` program to using the `case` command:

```bash
$ cat ShortCase.sh
#!/bin/bash
# Using a short case statement
#
case $USER in
    rich | christine)
        echo "Welcome $USER"
        echo "Please enjoy your visit.";;
    barbara | tim)
        echo "Hi there, $USER"
        echo "We're glad you could join us.";;
    testing)
        echo "Please log out when done with test.";;
    *)
        echo "Sorry, you are not allowed here."
esac
$
$ ./ShortCase.sh
Welcome christine
Please enjoy your visit.
$
```

The `case` command provides a much cleaner way of specifying the various options for each possible variable value.

## Summary

Structured commands allow you to alter the normal flow of shell script execution. The most basic structured command is the `if-then` statement. This statement provides a command evaluation and performs other commands based on the evaluated command's output.

You can expand the `if-then` statement to include a set of commands the Bash shell executes if the specified command fails as well. The `if-then-else` statement executes commands only if the command being evaluated returns a non-0 exit status code.

You can also link `if-then-else` statements together, using the `elif` statement. The `elif` is equivalent to using an `else if` statement, providing for additional checking of whether the original command that was evaluated failed.

In most scripts, instead of evaluating a command, you'll want to evaluate a condition, such as a numeric value, the contents of a string, or the status of a file or directory. The `test` command provides an easy way for you to evaluate all these conditions. If the condition evaluates to a TRUE condition, the `test` command produces a 0 exit status code for the `if-then` statement. If the condition evaluates to a FALSE condition, the `test` command produces a non-0 exit status code for the `if-then` statement.

The square bracket is a special Bash command that is a synonym for the `test` command. You can enclose a test condition in square brackets in the `if-then` statement to test for numeric, string, and file conditions.

The double parentheses command provides advanced mathematical evaluations using additional operators. The double square bracket command allows you to perform advanced string pattern-matching evaluations.

Finally, this chapter discussed the `case` command, which is a shorthand way of performing multiple `if-then-else` commands, checking the value of a single variable against a list of values.

The next chapter continues the discussion of structured commands by examining the shell looping commands. The `for` and `while` commands let you create loops that iterate through commands for a given period of time.
