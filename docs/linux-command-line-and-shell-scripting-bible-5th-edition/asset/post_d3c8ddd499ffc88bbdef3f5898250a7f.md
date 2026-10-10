
The `jobs` command allows you to display the co-processing status:

```
$ jobs
[1]+  Running                     coproc COPROC sleep 10 &
$
```

From the preceding example, you can see the background command executing in the subshell is `coproc COPROC sleep 10`. The `COPROC` is a name given to the process by the `coproc` command. You can set the name yourself by using extended syntax for the command:

```
$ coproc My_Job { sleep 10; }
[1]+  2706
$
$ jobs
[1]+  Running                     coproc My_Job { sleep 10; } &
$
```

By using the extended syntax, the co-processing name was set to `My_Job`. Be careful here, because the extended syntax is a little tricky. Make sure you place a space after the first curly bracket (`{`) and before the start of your command. Also, the command must end with a semicolon (`;`). And you must put a space after the semicolon and before the closing curly bracket (`}`).

> **Note**
> Co-processing allows you to get very fancy and send/receive information to the process running in the subshell. The only time you need to name a co-process is when you have multiple co-processes running and you need to communicate with them all. Otherwise, just let the `coproc` command set the name to the default, `COPROC`.

Using subshells can provide flexibility as well as convenience. Understanding their behavior is important in order to reach these goals. Command actions are also important to understand. In the next section, the behavioral differences between built-in and external commands are explored.

# Understanding External and Built-In Commands

While learning about the GNU Bash shell, you likely have heard the term *built-in command*. It is important to understand both shell built-in and non-built-in (external) commands. Built-in commands and non-built-in commands operate very differently.

## Looking at external commands

An *external command*, sometimes called a filesystem command, is a program that exists outside of the Bash shell. In other words, they are not built into the shell program. An external command program is typically located in the `/bin`, `/usr/bin`, `/sbin`, or `/usr/sbin` directories.

The **ps** command is an external command. You can find its filename by using the **which** and **type** commands:

```
$ which ps
/usr/bin/ps
$
$ type ps
ps is /usr/bin/ps
$
$ ls -l /usr/bin/ps
-rwxr-xr-x. 1 root root 142216 May 11 2019 /usr/bin/ps
$
```

Whenever an external command is executed, a child process is created. This action is termed *forking*. Conveniently, the external command **ps** displays its current parent as well as its own forked child processes:

```
$ ps -f
        UID   PID  PPID C STIME TTY          TIME CMD
christi+  2367  2363 0 10:47 pts/0    00:00:00 -bash
christi+  4242  2367 0 13:48 pts/0    00:00:00 ps -f
$
```

Because it is an external command, when the **ps** command executes, a child process is created. In this case, the **ps** command’s PID is **4242**, and the parent PID is **2367**. The Bash shell process, which in this case is the parent process, has a PID of **2367**. Figure 5.3 illustrates the forking that occurs when an external command is executed.

![](img/0798d50a0e5dbf1265fbda3832b3e015_140_0.png)

Whenever a process must fork, it takes time and effort to set up the new child process’s environment. Thus, external commands can be a little expensive.

> **Note**
> If you fork a child process or create a subshell, you can still communicate with it via *signaling*, which is extremely helpful in both the command line and in writing shell scripts. *Signaling* allows process communication via signals. Signals and signaling are covered in Chapter 16, "Script Control."

## Looking at built-in commands

When using a built-in command, no forking is required. Therefore, built-in commands are less expensive.

Built-in commands are different in that they do not need a child process to execute. They were compiled into the shell, and thus are part of the shell's toolkit. No external program file exists to run them.

Both the `cd` and `exit` commands are built into the Bash shell. You can tell a command is built-in by using the `type` command:

```
$ type cd
cd is a shell builtin
$
$ type exit
exit is a shell builtin
$
```

Because they do not need to fork a child process to execute or open a program file, built-in commands are faster and more efficient. A list of GNU Bash shell built-in commands is provided in Appendix A.

Be aware that some commands have multiple flavors. For example, `echo` and `pwd` both have a built-in command flavor as well as an external command flavor. These flavors are slightly different. To see multiple flavors for commands, use the `-a` option on the `type` command:

```
$ type -a echo
echo is a shell builtin
echo is /usr/bin/echo
$
$ which echo
/usr/bin/echo
$
$ type -a pwd
pwd is a shell builtin
pwd is /usr/bin/pwd
$
$ which pwd
/usr/bin/pwd
$
```

Using the `type -a` command shows both types (built-in and external) for each of the two commands. Note that the `which` command shows only the external command file.

> **Tip**
> To use the external command for a command that has multiple flavors, directly reference the file. For example, to use the `pwd` external command, type `/usr/bin/pwd`.

## Using the _history_ command

The Bash shell keeps track of the most recent commands you have used. You can recall these commands and even reuse them. A helpful built-in command that lets you explore and manage these previously issued commands is the `history` command.

To see a list of recently used commands, type the `history` command with no options:

```
$ history
    1  ps -f
    2  pwd
    3  ls
    4  coproc ( sleep 10; sleep 2 )
    5  jobs
    6  ps --forest
    7  ls
    8  ps -f
    9  pwd
   10  ls -l /usr/bin/ps
   11  history
   12  cd /etc
   13  pwd
   14  ls
   15  cd
   16  type -a pwd
   17  which pwd
   18  type -a echo
   19  which echo
   20  ls
[...]
$ 
```

In this example, the listing is snipped and only the first 20 commands are shown. Typically, the last 1,000 commands are kept in history. That's a lot of commands!

> **Tip**
> You can set the number of commands to keep in the Bash history. To do so, you need to modify an environment variable called `HISTSIZE` (see Chapter 6).

You can recall and reuse the last command in your history list. This can save time and typing.

To recall and reuse your last command, type `!!` and press the Enter key:

```
$ ps --forest
  PID TTY          TIME CMD
 2367 pts/0    00:00:00 bash
 5240 pts/0    00:00:00 \ ps
$
$ !!
ps --forest
  PID TTY         TIME CMD
 2367 pts/0    00:00:00 bash
 5241 pts/0    00:00:00 \_ ps
$
```

When `!!` was entered, the Bash shell first displayed the command it was recalling from the shell’s history. And after the command was displayed, it was executed.

Command history is kept in the hidden `.bash_history` file, which is located in each user’s home directory:

```
$ pwd
/home/christine
$
$ ls .bash_history
.bash_history
$
```

Be aware that during your CLI session, the bash command history is stored in memory. It is only written out into the history file when the shell is exited:

```
$ history
  1 ps -f
  2 pwd
(...)
 38 exit
 39 history
 40 ps --forest
 41 ps --forest
 42 pwd
 43 ls .bash_history
 44 history
$
$ cat .bash_history
ps -f
pwd
(...)
ls
history
exit
$
```

Notice when the `history` command is run, the last commands displayed do not match final commands in the `.bash_history` file. There were six additional commands issued, which are not recorded in the history file.

You can force the command history to be written to the `.bash_history` file without leaving a shell session. In order to impose this write, use the `-a` option on the `history` command.

> **Note**
> If you have multiple terminal sessions open, you can still append `.bash_history` in each open session using the `history -a` command. However, the histories are not automatically updated for your other open terminal sessions. This is because the `.bash_history` file is read-only when a terminal session is first started. To force the `.bash_history` file to be reread and a terminal session's history in memory to be updated, use the `history -n` command.

You can recall any command from the history list. Just enter an exclamation point and the command's number from the history list:

```
$ history
1 ps -f
2 pwd
[_]
39 history
40 cat .bash_history
41 ps --forest
42 pwd
43 ps -f
44 history
45 cat .bash_history
46 history -a
47 history
48 cat .bash_history
49 history
$
$ 42
pwd
/home/christine
$
```

Command number 42 was pulled from history list. Notice that similar to executing the last command in history, the Bash shell first displays the command it is recalling from the shell's history. After the command is displayed, it is executed.

> **Tip**
> If for some reason, you need to clear out command history, it's simple to do. Just type `history -c` and the contents of the current history are wiped. Next enter `history -a` to also clear out the `.bash_history` file.

Using Bash shell command history can be a great timesaver. You can do even more with the built-in `history` command. Be sure to view the Bash manual pages for `history` by typing `man history`.

## Using command aliases

The `alias` command is another useful built-in shell command. A *command alias* allows you to create an alias name for common commands (along with their parameters) to help keep your typing to a minimum.
