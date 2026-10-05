
# COMMANDS THAT ARE SYMBOLS

The Bourne Again Shell uses the symbols (, ), [ ], and $ in a variety of ways. To minimize confusion, Table 9-1 lists the most common use of each of these symbols, even though some of them are not introduced until later in this book.

Table 9-1 Builtin commands that are symbols

| Symbol | Command |
| --- | --- |
| () | Subshell (page 306) |
| $() | Command substitution (page 362) |
| (()) | Arithmetic evaluation; a synonym for let (use when the enclosed value contains an equal sign; page 1016) |
| ($()) | Arithmetic expansion (not for use with an enclosed equal sign; page 360) |
| [] | The test command (page 955 and 957) |
| [[] | Conditional expression; similar to [ ] but adds string comparisons (page 1017) |

# REDIRECTING STANDARD ERROR

Chapter 7 covers the concept of standard output and explained how to redirect standard output of a command. In addition to standard output, commands can send output to *standard error*. A command can send error messages to standard error to keep them from getting mixed up with the information it sends to standard output.

Just as it does with standard output, by default the shell directs standard error to the screen. Unless you redirect one or the other, you may not know the difference between the output a command sends to standard output and the output it sends to standard error. This section describes the syntax used by the Bourne Again Shell to redirect standard error and to distinguish between standard output and standard error.

A file descriptor is the place a program sends its output to and gets its input from. When you execute a program, Linux opens three descriptors for the program: 0 (standard input), 1 (standard output), and 2 (standard error). The redirect output (> [page 246]) is shorthand for 1>, which tells the shell to redirect standard output. < (page 247) is shorthand for 0<, which redirects standard input. The symbols 2> redirect standard error. For more information refer to "File Descriptors" on page 987.

The following examples demonstrate how to redirect standard output and standard error to different files and to the same file. When you run the cat utility with the name of a file that does not exist and the name of a file that does exist, cat can send an error message to standard error and copies the file that does exist to standard output. Unless you redirect them, both messages appear on the screen.

```
$ cat y
This is y.
$ cat x
cat: x: No such file or directory
```

```
$ cat y
cat: x: No such file or directory
This is y.
```

When you redirect standard output of a command, output sent to standard error is not affected and still appears on the screen.

```
$ cat x > hold
cat: x: No such file or directory
$ cat hold
This is y.
```

Similarly, when you send standard output through a pipe, standard error is not affected. The following example sends standard output of cat through a pipe to tr, which in this example converts lowercase characters to uppercase (See the tr for more information). The text that cat sends to standard error is not translated because it goes directly to the screen rather than the pipe.

```
$ cat x y | tr "[a-z]" "[A-Z]"
cat: x: No such file or directory
THIS IS Y.
```

The following example redirects standard output and standard error to different files. The token 2> tells the shell to redirect standard error (file descriptor 2). The following token 1> tells the shell to redirect standard output (file descriptor 1). You can use > in place of |.

```
$ cat x y 1> hold1 2> hold2
$ cat hold1
This is y.
$ cat hold2
cat: x: No such file or directory
```

In the next example, the && redirects standard output and standard error to a single file:

```
$ cat x y && hold
$ cat hold
cat: x: No such file or directory
This is y.
```

In the next example, first 1> redirects standard output to hold and then 2>&1 declares file descriptor 2 to be a duplicate of file descriptor 1. As a result, both standard output and standard error are redirected to hold.

```
$ cat x y 1> hold 2>&1
$ cat hold
cat: x: No such file or directory
This is y.
```

In this case, 1> precedes 2>&1. If they had been listed in the opposite order, standard error would have been made a duplicate of standard output before.

| [n]>& | Closes standard output or file descriptor *n* if specified. |

# WRITING A SIMPLE SHELL SCRIPT

A shell script is a file that holds commands that the shell can execute. The commands in a shell script can be any commands you enter in response to a shell prompt. For example, a command in a shell script might run a Linux utility, a compiled program, or another shell script. Like the commands you give on the command line, a command in a shell script can use ambiguous file references and can have its input or output redirected to a file or sent through a pipe. You can also use pipes and redirection with the input and output of the shell script.

In addition to the commands you would ordinarily use on the command line, control flow commands (also called control structures) find most of their use in shell scripts. This group of commands enables you to alter the order of execution of commands in a script in the same way you would alter the order of execution of statements using a structured programming language. Refer to “Control Structures” on page 954 for specifications.

The shell interprets and executes the commands in a shell script, one after another. Thus a shell script enables you to simply and quickly initiate a complex series of tasks or repetitive procedure.

# chmod: MAKES A FILE EXECUTABLE

To execute a script by giving its name as a command, you must have permission to read and execute the file that contains the script (refer to “Access Permissions” on page 215). Read permission enables you to read the file that holds the script. Execute permission tells the shell and the system that the owner, group, or public has permission to execute the file; it implies that the content of the file is executable.

When you create a shell script using an editor, the file does not typically have its execution permission set. The following example shows a file named whoson that contains a script:

```
$ cat whoson
date
echo "Users Currently Logged In"
who
```

```
$ ./whoson
bash: ./whoson: Permission denied
```

You cannot execute whoson by giving its name as a command because you do not execute permission for the file. The shell does not recognize whoson as an executable file and issues the error message Permission denied when you try to execute it. (See the tip on the next page if you get a command not found error message.) When you give the filename as an argument to bash (bash whoson), bash takes the argument to be a shell script and executes it. In this case bash is executable and whoson is an argument that bash executes so you do not need to have execute permission to whoson. You must read permission.

```
$ ls -l whoson
-rw-rw--r-- 1 max group 40 May 24 11:30 whoson

$ chmod u+x whoson
$ ls -l whoson
-rw-xr--r-- 1 max group 40 May 24 11:30 whoson

$ ./whoson
Mon May 25 11:40:49 PDT 2010
Users Currently Logged In
zach pts/7 2010-05-23 18:17
hls pts/1 2010-05-24 09:59
sam pts/12 2010-05-24 06:29 (bravo.example.com)
max pts/4 2010-05-24 09:08
```

**Figure 9-1** to make a shell script executable

The chmod utility changes the access privileges associated with a file. Figure 9-1 shows ls the -l option displaying the access privileges of whoson before and after chmod gives permission to the file. The first displays is a hyphen--) as the fourth character, indicating that the owner does not have permission to execute the file. The next chmod gives the owner execute permission: u+x causes chmod to add (+) permission (x) for the owner (u). The u stands for user, although it means the x of the owner of the file. The second argument is the second ls shows an x in the fourth position, indicating that the owner has execute permission.

# Command not found?

If you give the name of a shell script as a command without including the leading ./ the shell typically displays the following error message:

```
$ whoson
bash: whoson: command not found
```

This message indicates the shell is not set up to search for executable files in the working directory. Give this command instead:

```
$ ./whoson
```

The ./ tells the shell to look for an executable file in the working directory. To change the environment so the shell searches the working directory automatically, see the section about PATH on page 319.

If other users execute the file, you must also change group and public access permissions for the file. Any user must have execute access to the file's name as a command. If the file is a shell script, the user trying to execute the file must have read access to the file as well. You do not need read access to execute a binary executable (compiled program).
