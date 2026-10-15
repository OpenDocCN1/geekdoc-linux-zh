# 8.8.5 Debugging

By using the -n option to the sh command, you can check the syntax of your scripts without really executing any of the commands. If there is a syntax error in the script, the shell will report the error. If there are no errors, nothing is displayed.

The most commonly used method for debugging scripts is to use the set command with the -x option, or to use the -x option as an argument to the sh command, followed by the script name. See Table 8.6 for a list of debugging options. These options allow an execution trace of your script. Each command from your script is displayed after substitution has been performed, and then the command is executed. When a line from your script is displayed, it is preceded with a plus (+) sign.

With the verbose option turned on, or by invoking the Bourne shell with the -v option (sh -v pathname), each line of the script will be displayed just as it was typed in the script, and then executed.

# Table 8.6 Debugging Options

| Command | Option | What It Does |
|---|---|---|
| sh -x scriptname | Echo option | Displays each line of script after variable substitutions and before execution |
| sh -v scriptname | Verbose option | Displays each line of script before execution, just as you typed it |
| sh -n scriptname | Noexec option | Interprets but does not execute commands |
| set -x | Turns on echo | Traces execution in a script |
| set +x | Turns off echo | Turns off tracing |

# EXAMPLE 8.58

```
(The Script)
#!/bin/sh
1 # Scriptname: codedebug
name="Joe Blow"
if [ "$name" = "Joe Blow" ]
then
    echo "Hi $name"
fi
num=1
while [ $num -lt 5 ]
do
    num=`expr $num + 1`
done
echo The grand total is $num
```