# The -x Option for Debugging Programs

A bug. Not uncommon at all in the process of developing programs, whether they're 5 lines or\500 lines long. In this instance, it appears that the letter counting portion of our program isn't
working properly. But how do you figure what's not working?

This is a good point to introduce the shell's -x option. To debug any shell program—or learn
more about how it works—trace the sequence of its execution by typing in sh -x followed
by the regular invocation (name and arguments). This starts up a new shell to execute the
indicated program with the -x option enabled.

In this mode, commands are printed at the terminal as they are executed, preceded by a plus
Let's try to it out!

```
$ sh -x ctype a           Trace execution
+ [ 1 -ne 1 ]               $ equals 1
+ char=                      Assignment of $1 to char
+ echo
+ wc -c                       returned ???
+ [ 2 -ne 1 ]               That's why this test succeeded
+ echo type a single character
please type a single character
+ exit 1
$
```

The trace output indicates that wc returned 2 when this command was executed:

```
echo "$char" | wc -c
```

But why the value 2 if the command was given the single letter a? It turns out that two
characters were actually given to wc: the single character a and the "invisible" newline
character that echo automatically prints at the end of each line. Oops. So instead of testing for
a single character by comparing it to 1, the conditional expressions should be comparing the
user input to 2: the character typed plus the newline added by echo.

Go back to the ctype program and update the if command that reads

```
if [ "numchars" -ne 1 ]
```

```
echo Please type a single character
exit 1
```

```
fi
```

to look like this

```
if [ "numchars" -ne 2 ]
```

```
echo Please type a single character
exit 1
```

```
fi
```