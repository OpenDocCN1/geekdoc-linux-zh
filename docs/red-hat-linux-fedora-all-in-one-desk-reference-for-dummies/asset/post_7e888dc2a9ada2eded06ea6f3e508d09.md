
The last line of the example shows how a shell function is called with arguments. In this case, the hello function is being called with two arguments: Jane and Doe. The hello function takes these two arguments and prints out a line that says Hello, Jane Doe.

## Controlling the flow

In Bash scripts, you can control the flow of execution — the order in which the commands are executed — by using special commands such as if, case, for, and while. These control statements use the exit status of a command to decide what to do next. When any command executes, it returns an exit status — a numeric value that indicates whether or not the command has succeeded. By convention, an exit status of zero means the command has succeeded. (Yes, you read it right: Zero indicates success!) A nonzero exit status indicates that something has gone wrong with the command.

For example, suppose you want to make a backup copy of a file before editing it with the vi editor. More importantly, you want to avoid editing the file if a backup can't be made. Here's a Bash script that takes care of this task:

```
#!/bin/sh
if cp "$1" "#$1"
then
    vi "$1"
else
    echo "Failed to create backup copy"
fi
```

This script illustrates the syntax of the if-then-else structure and shows how the exit status of the cp command is used by the if command to determine the next action. If cp returns zero, the script uses vi to edit the file; otherwise, the script displays an error message and exits. By the way, the script saves the backup in a file whose name is the same as that of the original, except for a hash mark (#) added at the beginning of the filename.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_801_0.png)

Don't forget the final fi that terminates the if command. Forgetting fi is a common source of errors in Bash scripts.

You can use the test command to evaluate any expression and to use the expression's value as the exit status of the command. Suppose you want a script that edits a file only if it already exists. Using test, you can write such a script as follows:

```
#!/bin/sh
if test -f "$1"
then
    vi "$1"
else
    echo "No such file"
fi
```

A shorter form of the test command is to place the expression in square brackets ([ ... ]). Using this shorthand notation, you can rewrite the preceding script like this:

```
#!/bin/sh
if [ -f "$1" ]
then
    vi "$1"
else
    echo "No such file"
fi
```

Note: You must have spaces around the two square brackets.

Another common control structure is the for loop. The following script adds the numbers 1 through 10:

```
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
    sum=`expr $sum + $i`
done
echo "Sum = $sum"
```

This example also illustrates the use of the expr command to evaluate an expression.

The case statement is used to execute a group of commands based on the value of a variable. For example, consider the following script, based on the confirm() function in the /etc/init.d/functions file in your Red Hat Linux system:

```
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [Y] "
read answer
case $answer in
y|Y|*)
    echo "YES"
    ;;
c|C)
    echo "CONTINUE"
    ;;
n|N)
    echo "NO"
    ;;
*) echo "UNKNOWN"
;;
esac
```

Save this in a file named `confirm` and type `chmod +x confirm` to make it executable. Then try it out like this:

```
./confirm
```

When the script prompts you, type one of the characters y, n, or c and then press Enter. The script should display YES, NO, or CONTINUE. For example, here's what happens when I type c (and then press Enter):

```
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

The script displays a prompt and reads the input you type. Your input is stored in a variable named `answer`. Then the `case` statement executes a block of code based on the value of the `answer` variable. For example, when I type c, the following block of commands is executed:

```
c|C)
  echo "CONTINUE"
;;
```

The `echo` command causes the script to display CONTINUE.

From this example, you can see that the general syntax of the `case` command is as follows:

```
case $variable in
  value1 | value2)
    command1
    command2
    ...other commands...
  ;;
  value3)
    command3
    command4
    ...other commands...
  ;;
esac
```

Essentially, the `case` command begins with the word `case` and ends with `esac`. Separate blocks of code are enclosed between the values of the variable, followed by a closing parenthesis and terminated by a pair of semicolons (;;).

## Exploring Bash's built-in commands

Bash has more than 50 built-in commands, including common commands such as cd and pwd, as well as many others that are used infrequently. You can use these built-in commands in any Bash script or at the shell prompt. Table 3-1 describes most of the Bash built-in commands and their arguments. After looking through this information, type help cmd to read more about a specific built-in command. For example, to learn more about the built-in command test, type the following:

```
help test
```

Doing so displays the following information on my Red Hat Linux system:

```
test: test [expr]
Exits with a status of 0 (true) or 1 (false) depending on
the evaluation of EXPR. Expressions may be unary or binary. Unary
expressions are often used to examine the status of a file. There
are string operators as well, and numeric comparison operators.

File operators:
-a FILE True if file exists.
-b FILE True if file is block special.
-c FILE True if file is character special.
-d FILE True if file is a directory.
-e FILE True if file exists.
-f FILE True if file exists and is a regular file.
-g FILE True if file is set-group-id.
-h FILE True if file is a symbolic link.
-L FILE True if file is a symbolic link.
-k FILE True if file has its 'sticky' bit set.
-p FILE True if file is a named pipe.
-r FILE True if file is readable by you.
-s FILE True if file exists and is not empty.
-S FILE True if file is a socket.
-t FD True if FD is opened on a terminal.
-u FILE True if the file is set-user-id.
-w FILE True if the file is writable by you.
-x FILE True if the file is executable by you.
-O FILE True if the file is effectively owned by you.
-G FILE True if the file is effectively owned by your group.
(... Lines deleted ...)
```

Where necessary, the online help from the help command includes a considerable amount of detail.

Some external programs may have the same name as Bash built-in commands. If you want to run any such external program, you have to specify explicitly the full pathname of that program. Otherwise, Bash executes the built-in command of the same name.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_804_0.png)

### Table 3-1 Summary of Built-in Commands in Bash Shell

| This Function | Does the Following |
|---|---|
| `. filename [arguments]` | Reads and executes commands from the specified file using the optional arguments (works the same way as the source command). |
| `: [arguments]` | Expands the arguments but does not process them. |
| `[ expr ]` | Evaluates the expression expr and returns zero status if expr is true. |
| `alias [name=value] ...` | Defines an alias. |
| `bg [job]` | Puts the specified job in the background. If no job is specified, it puts the currently executing command in the background. |
| `bind [-m keymap] [-lvd] [-q name]` | Binds a key sequence to a macro. |
| `break [n]` | Exits from a for, while, or until loop. If n is specified, the n-th enclosing loop is exited. |
| `builtin builtin_command [arguments]` | Executes a shell built-in command. |
| `cd [dir]` | Changes the current directory to dir. |
| `command [-pVv] cmd [arg ...]` | Runs the command cmd with the specified arguments (ignoring any shell function named cmd). |
| `continue [n]` | Starts the next iteration of the for, while, or until loop. If n is specified, the next iteration of the n-th enclosing loop is started. |
| `declare [-frxi] [name=value]` | Declares a variable with the specified name and, optionally, assigns it a value. |
| `dirs [-l] [-/+n]` | Displays the list of currently remembered directories. |
| `echo [-neE] [arg ...]` | Displays the arguments on standard output. |
| `enable [-n] [-all] [name ...]` | Enables or disables the specified built-in commands. |
| `eval [arg ...]` | Concatenates the arguments and executes them as a command. |
| `exec [command [arguments]]` | Replaces the current instance of the shell with a new process that runs the specified command. |
| `exit [n]` | Exits the shell with the status code n. |
| `export [-nf] [name=word] ...` | Defines a specified environment variable and exports it to future processes. |
