command is legal, too. It’s interpreted as another command in the list of commands that if will evaluate for an exit code. The else is encountered next, but it’s out of place since the shell recognizes it as a reserved word (a word that has special meaning to the shell) and not the name of a command, which is the reason for the error message.

# Unanticipated Expansions

It’s possible to have errors that occur only intermittently in a script. Sometimes the script will run fine, and other times it will fail because of the results of an expansion. If we return our missing semicolon and change the value of number to an empty variable, we can demonstrate.

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=

if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi
```

Running the script with this change results in the following output:

```
[me@linuxbox ~]$ trouble
/home/me/bin/trouble: line 7: [: =: unary operator expected
Number is not equal to 1.
```

We get this rather cryptic error message, followed by the output of the second echo command. The problem is the expansion of the number variable within the test command. When the following command:

```
[ $number = 1 ]
```

undergoes expansion with number being empty, the result is this:

```
[ = 1 ]
```