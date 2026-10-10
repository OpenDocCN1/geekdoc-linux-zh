```
if IamNotaCommand
then    echo "It worked"
fi
echo "We are outside the if statement"
$
./test2.sh
./test2.sh: line 3: IamNotaCommand: command not found
We are outside the if statement
$
```

In this example, we deliberately used a nonexistent command, IamNotaCommand, in the `if` statement line. Because this is an incorrect command, it produces an exit status that's non-zero. Thus, the Bash shell skips the `echo` statement in the `then` section. Also notice that the error message generated from running the command in the `if` statement still appears in the script's output. There may be times when you don't want an error statement to appear. Chapter 15, “Presenting Data,” discusses how this can be avoided.

> ### NOTE
> 
> You might see an alternative form of the `if-then` statement used in some scripts:
> 
> if command; then
>    commands
> fi
> 
> By putting a semicolon (`;`) at the end of the command to evaluate, you can include the `then` statement on the same line, which looks closer to how `if-then` statements are handled in some other programming languages.

You are not limited to just one command in the `then` section. You can list commands just as you do in the rest of the shell script. The Bash shell treats the commands as a block, executing all of them when the command in the `if` statement line returns a zero exit status or skipping all of them when the command returns a non-zero exit status:

```
$ cat test3.sh
```