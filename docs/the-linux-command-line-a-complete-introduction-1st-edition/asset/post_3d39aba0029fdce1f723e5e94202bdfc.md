
In this script, we determine if the value of integer INT lies between the values of MIN_VAL and MAX_VAL. This is performed by a single use of [[ ]], which includes two expressions separated by the && operator. We could have also coded this using test:

```
if [ $INT -ge $MIN_VAL -a $INT -le $MAX_VAL ]; then
    echo "$INT is within $MIN_VAL to $MAX_VAL."
else
    echo "$INT is out of range."
fi
```

The ! negation operator reverses the outcome of an expression. It returns true if an expression is false, and it returns false if an expression is true. In the following script, we modify the logic of our evaluation to find values of INT that are outside the specified range:

```
#!/bin/bash

# test-integer4: determine if an integer is outside a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^[-0-9]+$ ]]; then
    if [[ ! ( $INT -ge $MIN_VAL && $INT -le $MAX_VAL ) ]]; then
        echo "$INT is outside $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is in range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

We also include parentheses around the expression for grouping. If these were not included, the negation would apply to only the first expression and not the combination of the two. Coding this with test would be done this way:

```
if [ ! \( $INT -ge $MIN_VAL -a $INT -le $MAX_VAL \ ) ]; then
    echo "$INT is outside $MIN_VAL to $MAX_VAL."
else
    echo "$INT is in range."
fi
```

Since all expressions and operators used by test are treated as command arguments by the shell (unlike [[ ]] and (( )), characters that have special meaning to bash, such as <, >, (, and ), must be quoted or escaped.

Seeing that test and [[ ]] do roughly the same thing, which is preferable? test is traditional (and part of POSIX), whereas [[ ]] is specific to bash. It’s important to know how to use test, since it is very widely used, but [[ ]] is clearly more useful and is easier to code.

## PORTABILITY IS THE HOBGOBLIN OF LITTLE MINDS

If you talk to “real” Unix people, you quickly discover that many of them don’t like Linux very much. They regard it as impure and unclean. One tenet of Unix followers is that everything should be portable. This means that any script you write should be able to run, unchanged, on any Unix-like system.

Unix people have good reason to believe this. Having seen what proprietary extensions to commands and shells did to the Unix world before POSIX, they are naturally wary of the effect of Linux on their beloved OS.

But portability has a serious downside. It prevents progress. It requires that things are always done using “lowest common denominator” techniques. In the case of shell programming, it means making everything compatible with sh, the original Bourne shell.

This downside is the excuse that proprietary vendors use to justify their proprietary extensions, only they call them “innovations.” But they are really just lock-in devices for their customers.

The GNU tools, such as bash, have no such restrictions. They encourage portability by supporting standards and by being universally available. You can install bash and the other GNU tools on almost any kind of system, even Windows, without cost. So feel free to use all the features of bash. It’s really portable.

## Control Operators: Another Way to Branch

bash provides two control operators that can perform branching. The && (AND) and || (OR) operators work like the logical operators in the [[ ]] compound command. This is the syntax:

```
command1 && command2
```

and

```
command1 || command2
```

It is important to understand the behavior of these. With the && operator, command1 is executed and command2 is executed if, and only if, command1 is successful. With the || operator, command1 is executed and command2 is executed if, and only if, command1 is unsuccessful.

In practical terms, it means that we can do something like this:

```
[me@linuxbox ~]$ mkdir temp && cd temp
```

This will create a directory named temp, and if it succeeds, the current working directory will be changed to temp. The second command is attempted only if the mkdir command is successful. Likewise, a command like

```
[me@linuxbox ~]$ [ -d temp ] || mkdir temp
```

will test for the existence of the directory temp, and only if the test fails will the directory be created. This type of construct is very handy for handling errors in scripts, a subject we will discuss more in later chapters. For example, we could do this in a script:

```
[ -d temp ] || exit 1
```

If the script requires the directory temp, and it does not exist, then the script will terminate with an exit status of 1.

## Final Note

We started this chapter with a question. How could we make our sys_info_page script detect whether or not the user had permission to read all the home directories? With our knowledge of if, we can solve the problem by adding this code to the report_home_space function:

```
report_home_space () {
    if [[ $(id -u) -eq 0 ]]; then
        cat << _EOF_
<H2>Home Space Utilization (All Users)</H2>
<PRE>$ (du -sh /home/*)</PRE>
_EOF_
    else
        cat << _EOF_
<H2>Home Space Utilization ($USER)</H2>
<PRE>$ (du -sh $HOME)</PRE>
_EOF_
    fi
    return
}
```

We evaluate the output of the id command. With the -u option, id outputs the numeric user ID number of the effective user. The superuser is always zero, and every other user is a number greater than zero. Knowing this, we can construct two different here documents, one taking advantage of superuser privileges and the other restricted to the user's own home directory.
