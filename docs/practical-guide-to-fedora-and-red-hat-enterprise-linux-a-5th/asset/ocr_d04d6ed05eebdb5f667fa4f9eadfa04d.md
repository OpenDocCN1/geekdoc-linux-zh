C program, **exec** succeeds and the system overlays the newly created subshell with the executable program. If the command is a shell script, **exec** fails. When **exec** fails, the command is assumed to be a shell script, and the subshell runs the commands in the script. Unlike a login shell, which expects input from the command line, the subshell takes its input from a file: the shell script.

As discussed earlier, if you have a shell script in a file that you do not have execute permission for, you can run the commands in the script by using a **bash** command to exec a shell to run the script directly. In the following example, **bash** creates a new shell that takes its input from the file named **whoson**:

$ **bash whoson**

Because the **bash** command expects to read a file containing commands, you do not need execute permission for **whoson**. (You do need read permission.) Even though **bash** reads and executes the commands in **whoson**, standard input, standard output, and standard error remain connected to the terminal.

Although you can use **bash** to execute a shell script, this technique causes the script to run more slowly than giving yourself execute permission and directly invoking the script. Users typically prefer to make the file executable and run the script by typing its name on the command line. It is also easier to type the name, and this practice is consistent with the way other kinds of programs are invoked (so you do not need to know whether you are running a shell script or another kind of program). However, if **bash** is not your interactive shell or if you want to see how the script runs with different shells, you may want to run a script as an argument to **bash** or **csh**.

# **sh does not call the original Bourne Shell**

> caution The original Bourne Shell was invoked with the command **sh**. Although you can call **bash** with an **sh** command, it is not the original Bourne Shell. The **sh** command (**/bin/sh**) is a symbolic link to **/bin/bash**, so it is simply another name for the **bash** command. When you call **bash** using the command **sh**, **bash** tries to mimic the behavior of the original Bourne Shell as closely as possible. It does not always succeed.

# # SEPARATING AND GROUPING COMMANDS

Whether you give the shell commands interactively or write a shell script, you must separate commands from one another. This section reviews the ways to separate commands that were covered in Chapter 7 and introduces a few new ones.

# ## ; AND NEWLINE SEPARATE COMMANDS

The NEWLINE character is a unique command separator because it initiates execution of the command preceding it. You have seen this throughout this book each time you press the RETURN key at the end of a command line.

The semicolon (;) is a command separator that *does not* initiate execution of a command and *does not* change any aspect of how the command functions. You can execute a series of commands sequentially by entering them on a single command line and separating each from the next with a semicolon (;). You initiate execution of the sequence of commands by pressing RETURN.