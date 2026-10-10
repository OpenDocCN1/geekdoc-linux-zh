# **Part II: Shell Scripting Basics**

```
$ ls -d /home/NoSuchUser/
/home/NoSuchUser/
$
$ ./test5.sh
The user NoSuchUser does not exist on this system.
/home/NoSuchUser/
However, NoSuchUser has a directory.
We are outside the nested if statements.
$
```

The script correctly finds that although the login name has been removed from the /etc/
passwd file, the user's directory is still on the system. The problem with using this manner
of nested if-then statements in a script is that the code can get hard to read, and the logic
flow becomes difficult to follow.

> **Note**
> 
> The `ls` command has some additional useful command options (and option combinations) used in this chapter:
> 
> *   -d shows only the directory information, not the directory's contents.
> *   -sh displays the file's size in a human-readable format.
> *   -g shows the file's long listing minus the owner name.
> *   -o display the file's long listing minus the group name.
> 
> The `ls` command was first covered in Chapter 3, “Basic Bash Shell Commands.”

Instead of having to write separate `if-then` statements, you can use an alternative version
of the `else` section, called `elif`. The `elif` continues an `else` section with another
`if-then` statement:

```
if command1
then
commands
elif command2
then
more commands
fi
```

The `elif` statement line provides another command to evaluate, similar to the original
`if` statement line. If the exit status code from the `elif` command is 0, Bash executes the
commands in the second `then` statement section. Using this method of nesting provides
cleaner code with an easier-to-follow logic flow:

```
$ cat test5.sh
#!/bin/bash
# testing nested ifs - using elif
#
testuser=NoSuchUser
#
if grep $testuser /etc/passwd
```