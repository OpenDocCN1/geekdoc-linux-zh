
| Name | Dept | GPA |
|---|---|---|
| Jason Kim | ECE | 3.97 |
| Jim Davis | CS | 2.71 |
| John Doe | ECE | 3.54 |
| Pam Meyer | CS | 3.61 |

$
At times, you may need to connect several commands. The following command line demonstrates the use of multiple pipes, forming a pipeline of commands. In this command line, we have used the grep and sort filters.

```
$ who | sort | grep "john" | mail -s "John's Terminal" doe@coldmail.com
$
```

This command sorts the output of who and sends the lines containing the string "john" (if any exists) as an e-mail message to doe@coldmail.com, with the subject line "John's Terminal". In terms of input and output redirection, this command line is equivalent to the following command sequence.

```
$ who > temp1
$ sort < temp1 > temp2
$ grep "john" temp2 > temp3
$ mail -s "John's Terminal" doe@coldmail.com < temp3
$ rm temp1 temp2 temp3
$
```

The command with pipes does not use any disk files, but the preceding command sequence needs three temporary disk files and six disk I/O (read and write) operations. The number of I/O operations may be a lot higher, depending on the sizes of these files, the system load in terms of the number of users currently using the system, and the runtime behavior of other processes running on the system.

A pipe, therefore, is a UNIX feature that allows two UNIX commands (processes) to communicate with each other. Hence, a pipe provides an interprocess communication (IPC) mechanism in UNIX. More specifically, it can be used as a channel between two related processes on the same system to talk to each other. Typically, processes have a parent–child relationship (see Chapter 10) but processes with a common ancestor (parent, grandparent, etc.) can also communicate using a pipe. From a programmer's perspective, we discuss IPC using pipes in detail in Chapter 19. The communication between processes is one-way only. For example, in ls | more, the output of ls is read by more as input. Thus, the one-way communication is from ls to more. For a two-way communication between processes, at least two pipes must be used. This cannot be accomplished at the command shell level, but it can be done in C/C++ by using the pipe() system call. We explore this topic in Chapter 19 also.

I/O redirection and pipes can be used in a single command, as follows:

```
$ grep "John" < Students | lpr -P spr
$
```

![](img/02e070097d401d3bf7de4bf1c470b267_359_0.png)

FIGURE 9.13 Semantics of the grep "John" < Students | lpr -Pspr command.

![](img/02e070097d401d3bf7de4bf1c470b267_359_1.png)

FIGURE 9.14 Semantics of the egrep 'A$' < ece446.grades | sort > ece446.As.sorted command.

Here, the grep command searches the Students file for lines that contain the string "John" and sends those lines to the lpr command to be printed on a printer named spr. Figure 9.13 illustrates the semantics of this command.

In the following command, egrep takes its input from ece446.grades and sends its output (lines ending with the character A) to the sort utility, which sorts these lines and stores them in the file called ece446.As.sorted in the current directory. The end result is that the names, scores, and grades of those students who have A grades in the ECE446 course are stored in the ece446.As.sorted file in the current directory. Figure 9.14 illustrates the semantics of this command.

```
$ egrep 'A$' < ece446.grades | sort > ece446.As.sorted
$
```

Suppose that, before running the ssh server sort < datafile command in Section 9.4, you want to be sure that datafile on your local system is consistent with the updated copy on the server, called ~/research/pvm/datafile.server. You can copy datafile.server and compare it with your local copy, datafile. But, you will then have three copies, and if you are not careful you might remove the wrong copy. In this case, you can run the following command to see the differences between your local copy and the copy on the server without copying datafile.server on your (local) computer.

```
$ ssh server cat ~/research/pvm/datafile.server | diff datafile -
$
```

In this case, the cat command runs on the server side, and its output is fed as input to the diff command executed on the local machine. The output of the diff command also goes to the display screen on the local machine. Figure 9.15 illustrates the semantics of this command.

## 9.12 REDIRECTION AND PIPING COMBINED

You cannot use the redirection operators and pipes alone to redirect the stdout of a command to a file as well as connect it to stdin of another command in a single command line. However, you can use the tee utility to do so. You can use this utility to tell the command shell to send the stdout of a command to one or more files specified as arguments of tee,
