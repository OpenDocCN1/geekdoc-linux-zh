If you do not follow `#!` with the name of an executable program, the shell reports it cannot find the program you asked it to run. You can optionally follow `#!` with **SPACES** before the name of the program. If you omit the `#!` line and try to run, for example, a `tcsH` script from **bash**, the script will run under **bash** and might generate error messages or not run properly.

# # `#` **Begins a Comment**

Comments make shell scripts and all code easier to read and maintain by you and others. If a `hashmark` (`#`) in the first character position of the first line of a script is not immediately followed by an exclamation point (`!`) or if a `hashmark` occurs in any other location in a script, the shell interprets it as the beginning of a comment. The shell then ignores everything between the `hashmark` and the end of the line (the next **NEWLINE** character).

# # **Executing a Shell Script**

+   fork and exec  |  system calls

As discussed earlier, you can execute commands in a shell script file that you do not have `execute` permission for by using a **bash** command to `exec` a shell that runs the script directly. In the following **example**, **bash** creates a new shell that takes its input from the file named **whoson**:

```
$ bash whoson
```

Because the **bash** command expects to read a file containing commands, you do not need execute permission for **whoson**. (You do need read permission.) Even though **bash** `reads` and `executes` the commands in **whoson**, standard input, standard output, and standard error remain directed from/to the terminal. Alternatively, you can supply commands to **bash** using standard input:

```
$ bash < whoson
```

Although you can use **bash** to execute a shell script, these techniques cause the script to run more slowly than if you give yourself execute permission and directly invoke the script. Users typically prefer to make the file executable and run the script by `typing` its name on the command line. It is also easier to type the name, and this practice is consistent with the way other kinds of programs are invoked (so you do not need to know whether you are running a shell script or an executable file). However, if **bash** is not your `interactive` shell or if you want to see how the script runs with different shells, you might want to run a script as an argument to **bash** or `tcsH`.

> **sh** does not call the original Bourne Shell

+   caution |

The original **Bourne Shell** was invoked with the command **sh**. Although you can call **bash** with an **sh** command, it is not the original Bourne Shell. The **sh** command (**/bin/sh**) is a symbolic link to **/bin/bash**, so it is simply another name for the **bash** command. When you call **bash** using the command **sh**, **bash** tries to mimic the behavior of the original **Bourne Shell** as closely as possible—but it does not always succeed.