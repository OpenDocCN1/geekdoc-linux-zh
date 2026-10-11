
![](img/f28adb66a7398a382f0505e0ba74a872_328_0.png)

**Figure 9-1** Using chmod to make a shell script executable

The chmod utility changes the access privileges associated with a file. Figure 9-1 shows ls with the -l option displaying the access privileges of whoson before and after chmod gives execute permission to the file’s owner.

The first ls displays a hyphen (-) as the fourth character, indicating that the owner does not have permission to execute the file. Next chmod gives the owner execute permission: The u+x causes chmod to add (+) execute permission (x) for the owner (u). (The u stands for user, although it means the owner of the file who may be the user of the file at any given time.) The second argument is the name of the file. The second ls shows an x in the fourth position, indicating that the owner now has execute permission.

If other users will execute the file, you must also change group and/or public access permissions for the file. Any user must have execute access to use the file’s name as a command. If the file is a shell script, the user trying to execute the file must also have read access to the file. You do not need read access to execute a binary executable (compiled program).

The final command in Figure 9-1 shows the shell executing the file when its name is given as a command. For more information refer to “Access Permissions” on page 202, ls (page 203), and chmod (page 204).

## #! SPECIFIES A SHELL

You can put a special sequence of characters on the first line of a file to tell the operating system which shell should execute the file. Because the operating system checks the initial characters of a program before attempting to exec it, these characters save the system from making an unsuccessful attempt. If #! are the first two characters of a script, the system interprets the characters that follow as the absolute pathname of the utility that should execute the script. This can be the pathname of any program, not just a shell. The following example specifies that bash should run the script:

```
$ cat bash_script
#!/bin/bash
echo "This is a Bourne Again Shell script."
```

The #! characters are useful if you have a script that you want to run with a shell other than the shell you are running the script from. The following example shows a script that should be executed by tcsh:

```
$ cat tcsh_script
#!/bin/tcsh
echo "This is a tcsh script."
set person = Jenny
echo "person is $person"
```

Because of the #! line, the operating system ensures that tcsh executes the script no matter which shell you run it from.

You can use ps -f within a shell script to display the name of the shell that is executing the script. The three lines that ps displays in the following example show the process running the parent bash shell, the process running the tcsh script, and the process running the ps command:

```
$ cat tcsh_script2
#!/bin/tcsh
ps -f
```

```
$ tcsh_script2
UID PID PPID C STIME TTY TIME CMD
alex 3031 3030 0 Nov16 pts/4 00:00:00 -bash
alex 9358 3031 0 21:13 pts/4 00:00:00 /bin/tcsh ./tcsh_script2
alex 9375 9358 0 21:13 pts/4 00:00:00 ps -f
```

If you do not follow #! with the name of an executable program, the shell reports that it cannot find the command that you asked it to run. You can optionally follow #! with spaces. If you omit the #! line and try to run, for example, a tcsh script from bash, the shell may generate error messages or the script may not run properly.

### Begins A Comment

Comments make shell scripts and all code easier to read and maintain by you and others. If a pound sign (#) in the first character position of the first line of a script is not immediately followed by an exclamation point (!) or if a pound sign occurs in any other location in a script, the shell interprets it as the beginning of a comment. The shell then ignores everything between the pound sign and the end of the line (the next newline character).

### Running A Shell Script

A command on the command line causes the shell to fork a new process, creating a duplicate of the shell process (a subprocess). The new process attempts to exec (execute) the command. Like fork, the exec routine is executed by the operating system (a system call). If the command is a binary executable program, such as a compiled C program, **exec** succeeds and the system overlays the newly created subshell with the executable program. If the command is a shell script, **exec** fails. When **exec** fails, the command is assumed to be a shell script, and the subshell runs the commands in the script. Unlike a login shell, which expects input from the command line, the subshell takes its input from a file: the shell script.

As discussed earlier, if you have a shell script in a file that you do not have execute permission for, you can run the commands in the script by using a **bash** command to exec a shell to run the script directly. In the following example, **bash** creates a new shell that takes its input from the file named **whoson**:

$ **bash whoson**

Because the **bash** command expects to read a file containing commands, you do not need execute permission for **whoson**. (You do need read permission.) Even though **bash** reads and executes the commands in **whoson**, standard input, standard output, and standard error remain connected to the terminal.

Although you can use **bash** to execute a shell script, this technique causes the script to run more slowly than giving yourself execute permission and directly invoking the script. Users typically prefer to make the file executable and run the script by typing its name on the command line. It is also easier to type the name, and this practice is consistent with the way other kinds of programs are invoked (so you do not need to know whether you are running a shell script or another kind of program). However, if **bash** is not your interactive shell or if you want to see how the script runs with different shells, you may want to run a script as an argument to **bash** or **csh**.

## **sh does not call the original Bourne Shell**

> caution The original Bourne Shell was invoked with the command **sh**. Although you can call **bash** with an **sh** command, it is not the original Bourne Shell. The **sh** command (**/bin/sh**) is a symbolic link to **/bin/bash**, so it is simply another name for the **bash** command. When you call **bash** using the command **sh**, **bash** tries to mimic the behavior of the original Bourne Shell as closely as possible. It does not always succeed.

## SEPARATING AND GROUPING COMMANDS

Whether you give the shell commands interactively or write a shell script, you must separate commands from one another. This section reviews the ways to separate commands that were covered in Chapter 7 and introduces a few new ones.

### ; AND NEWLINE SEPARATE COMMANDS

The NEWLINE character is a unique command separator because it initiates execution of the command preceding it. You have seen this throughout this book each time you press the RETURN key at the end of a command line.

The semicolon (;) is a command separator that *does not* initiate execution of a command and *does not* change any aspect of how the command functions. You can execute a series of commands sequentially by entering them on a single command line and separating each from the next with a semicolon (;). You initiate execution of the sequence of commands by pressing RETURN.

```
$ x ; y ; z
```

If x, y, and z are commands, the preceding command line yields the same results as the next three commands. The difference is that in the next example the shell issues a prompt after each of the commands (x, y, and z) finishes executing, whereas the preceding command line causes the shell to issue a prompt only after z is complete:

```
$ x
$ y
$ z
```

- **Whitespace**: Although the whitespace around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACES or TABS.

## \ Continues a Command

When you enter a long command line and the cursor reaches the right side of the screen, you can use a backslash (\) character to continue the command on the next line. The backslash quotes, or escapes, the NEWLINE character that follows it so that the shell does not treat the NEWLINE as a command terminator. Enclosing a backslash within single quotation marks turns off the power of a backslash to quote special characters such as NEWLINE. Enclosing a backslash within double quotation marks has no effect on the power of the backslash.

Although you can break a line in the middle of a word (token), it is typically easier to break a line just before or after whitespace.

- **Optional**: You can enter a RETURN in the middle of a quoted string on a command line without using a backslash. The NEWLINE (RETURN) that you enter will then be part of the string:

```
$ echo "Please enter the three values
> required to complete the transaction."
Please enter the three values
required to complete the transaction.
```

In the three examples in this section, the shell does not interpret RETURN as a command terminator because it occurs within a quoted string. The > is a secondary prompt indicating that the shell is waiting for you to continue the unfinished command. In the next example, the first RETURN is quoted (escaped) so the shell treats it as a separator and does not interpret it literally.

```
$ echo "Please enter the three values \
> required to complete the transaction."
Please enter the three values required to complete the transaction.
```

Single quotation marks cause the shell to interpret a backslash literally:

```
$ echo 'Please enter the three values \
> required to complete the transaction.'
Please enter the three values \
required to complete the transaction.
```
