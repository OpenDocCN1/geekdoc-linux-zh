programmer’s convenience. A common convention is to use uppercase letters to designate constants and lowercase letters for true variables. We will modify our script to comply with this convention:

```
```bash
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

echo "<HTML>
        <HEAD>
                <TITLE>$TITLE</TITLE>
        </HEAD>
        <BODY>
                <H1>$TITLE</H1>
        </BODY>
</HTML>"
```

We also took the opportunity to jazz up our title by adding the value of the shell variable `HOSTNAME`. This is the network name of the machine.

> **Note:** *The shell actually does provide a way to enforce the immutability of constants, through the use of the `declare` built-in command with the `-r` (read-only) option. Had we assigned `TITLE` this way:*
> 
>     declare -r TITLE="Page Title"
> 
> *the shell would prevent any subsequent assignment to `TITLE`. This feature is rarely used, but it exists for very formal scripts.*

# Assigning Values to Variables and Constants

Here is where our knowledge of expansion really starts to pay off. As we have seen, variables are assigned values this way:

`variable=value`

where `variable` is the name of the variable and `value` is a string. Unlike some other programming languages, the shell does not care about the type of data assigned to a variable; it treats them all as strings. You can force the shell to restrict the assignment to integers by using the `declare` command with the `-i` option, but, like setting variables as read-only, this is rarely done. Note that in an assignment, there must be no spaces between the variable name, the equal sign, and the value. So what can the value consist of? Anything that we can expand into a string.

```
```bash
a=z                         # Assign the string "z" to variable a.
b="a string"                # Embedded spaces must be within quotes.
c="a string and $b"         # Other expansions such as variables can be
                            # expanded into the assignment.
d=$(ls -l foo.txt)           # Results of a command.
```
```