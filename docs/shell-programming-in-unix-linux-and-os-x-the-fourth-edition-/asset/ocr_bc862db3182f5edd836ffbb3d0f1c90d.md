```
```sh
else
    echo "$line"
fi
```
```

In the preceding example, if line has zero length, the echo command that displays the message I couldn't find $name is executed; otherwise, the echo command that displays the value of line is executed.

A final format of the if command is useful when more than a two-way decision has to be made. Its general format is

```
```sh
if command_1
then
        command
        command
        ...
elif command_2
then
        command
        command
        ...
elif command_n
then
        command
        command
        ...
else
        command
        command
        ...
fi
```
```

command₁, command₂, ..., commandₙ are evaluated in order until one of the commands returns an exit status of zero, at which point the commands that immediately follow the then (up to another elif, else, or fi) are executed. If none of the commands returns an exit status of zero, the commands listed after the else (if present) are executed.

*Example*

```
```sh
if [ "$choice" = a ] ; then
        add $*
elif [ "$choice" = d ] ; then
        delete $*
elif [ "$choice" = l ] ; then
        list
else
        echo "Bad choice!"
        error=TRUE
fi
```
```