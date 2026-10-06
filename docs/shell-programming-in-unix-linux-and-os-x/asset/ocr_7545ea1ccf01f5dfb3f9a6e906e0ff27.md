# Chapter 7 Decisions, Decisions

Now the task of writing the greetings program is straightforward:

```
$ cat greetings
#
# Program to print a greeting
#
h=$(date | cut -c1-13)

if [ "$hour" -ge 0 -a "$hour" -le 11 ]
then
    echo "Good morning"
else
    if [ "$hour" -ge 12 -a "$hour" -le 17 ]
then
        echo "Good afternoon"
    else
        echo "Good evening"
    fi
fi
```

If hour is greater than or equal to 0 (midnight) and less than 11 (up to 11:59:59), Good morning is displayed. If hour is greater than or equal to 12 (noon) and less than or to 17 (up to 5:59:59 pm), Good afternoon is displayed. Neither of the preceding cases is satisfied, Good evening is displayed.

```
$ greetings
Good morning
$
```

Look at the program again, however, and you'll realize that the nested if command sequence used in greetings is rather clumsy. To streamline these sorts of if-then-else sequences, the shell also supports a special elif element that acts somewhat like else if condition, except it doesn't increase your nesting level. The general format is

```
command,
then
    command
    command
    ...
elif command2,
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