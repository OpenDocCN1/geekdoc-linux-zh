
Of course, the process list of `sleep` and `echo` commands are just for example purposes. Creating backup files with `tar` (see Chapter 4) is a more practical example of using background process lists effectively:

```
$ (tar -cf Doc.tar Documents ; tar -cf Music.tar Music)&
[1] 2567
$
$ ls *.tar
Doc.tar  Music.tar
[1]+  Done    (tar -cf Doc.tar Documents;
tar -cf Music.tar Music )
$
```

Putting a process list in background mode is not the only way to use subshells creatively at the CLI. Co-processing is another method.

## Looking at co-processing

Co-processing does two things at the same time. It spawns a subshell in background mode and it executes a command within that subshell.

To perform co-processing, the `coproc` command is used along with the command to be executed in the subshell:

```
$ coproc sleep 10
[1] 2689
$
```

Co-processing performs almost identically to putting a command in background mode, except for the fact that it creates a subshell. You’ll notice that when the `coproc` command and its parameters were entered, a background job was started. The background job number (1) and process ID (2689) were displayed on the screen.

The `jobs` command allows you to display the co-processing status:

```
$ jobs
[1]+  Running     coproc COPROC sleep 10 &
$
```

From the preceding example, you can see that the background command executing in the subshell is `coproc COPROC sleep 10`. COPROC is a name given to the process by the `coproc` command. You can set the name yourself by using extended syntax for the command:

```
$ coproc My_Job { sleep 10; }
[1] 2706
$
$ jobs
[1]+  Running            coproc My_Job { sleep 10; } &
$
```

By using the extended syntax, the co-processing name was set to My_Job. Be careful here, because the extended syntax is a little tricky. Make sure you place a space after the first curly bracket ({) and before the start of your command. Also, the command must end with a semicolon (;). And you must put a space after the semicolon and before the closing curly bracket (}).

> **NOTE**
> Co-processing allows you to get very fancy and send/receive information to the process running in the subshell. The only time you need to name a co-process is when you have multiple co-processes running and you need to communicate with them all. Otherwise, just let the coproc command set the name to the default, COPROC.

You can be really clever and combine co-processing with process lists, creating nested subshells. Just type your process list and put the command coproc in front of it:

```
$ coproc ( sleep 10; sleep 2 )
[1] 2750
$
$ jobs
[1]+  Running            coproc COPROC ( sleep 10; sleep 2 ) &
$
$ ps --forest
  PID TTY          TIME CMD
2367 pts/0    00:00:00 bash
2750 pts/0    00:00:00 \_ bash
2751 pts/0    00:00:00 | \_ sleep
2752 pts/0    00:00:00 \_ ps
$
```

Just remember that spawning a subshell can be expensive and slow. Creating nested subshells is even more so!

Using subshells can provide flexibility as well as convenience. Understanding their behavior is important in order to reach these goals. Command actions are also important to understand. In the next section, the behavior differences between built-in and external commands are explored.

## Understanding External and Built-In Commands

While learning about the GNU Bash shell, you likely have heard the term *built-in command*. It is important to understand both shell built-in and non–built-in (external) commands. Built-in commands and non–built-in commands operate very differently.

### Looking at external commands

An *external command*, sometimes called a filesystem command, is a program that exists outside of the Bash shell. In other words, it is not built into the shell program. An external command program is typically located in /bin, /usr/bin, /sbin, or /usr/sbin directories.

The ps command is an external command. You can find its filename by using both the which and the type commands:

```
$ which ps
/usr/bin/ps
$ type ps
ps is /usr/bin/ps
$ ls -l /usr/bin/ps
-rwxr-xr-x. 1 root root 142216 May 11  2019 /usr/bin/ps
$ 
```

Whenever an external command is executed, a child process is created. This action is termed *forking*. Conveniently, the external command ps displays its current parent as well as its own forked child processes:

```
$ ps -f
UID   PPID  C STIME  TTY        TIME CMD
christi+ 2367 2363  0 10:47 pts/0    00:00:00 -bash
christi+ 4242 2367  0 13:48 pts/0    00:00:00 ps -f
$
```

Because it is an external command, when the `ps` command executes, a child process is created. In this case, the `ps` command's PID is 4242 and the parent PID is 2367. The Bash shell process, which in this case is the parent process, has a PID of 2367. **Figure 5-3** illustrates the forking that occurs when an external command is executed.

![](img/a5025f22e05b92f409563a958cac7312_192_0.png)

### FIGURE 5-3 External command forking

Whenever a process must fork, it takes time and effort to set up the new child process's environment. Thus, external commands can be a little expensive.

> **NOTE**
> If you fork a child process or create a subshell, you can still communicate with it via signaling, which is extremely helpful in both the command line and in writing shell scripts. Signaling allows process communication via signals. Signals and signaling are covered in Chapter 16, “Script Control.”

### Looking at built-in commands

*Built-in commands* are different in that they do not need a child process to execute. They were compiled into the shell, and thus are part of the shell’s toolkit. No external program file exists to run them. Both the `cd` and `exit` commands are built into the Bash shell. You can tell a command is built-in by using the `type` command:

```
$ type cd
cd is a shell builtin
$
$ type exit
exit is a shell builtin
$
```

Because they do not need to fork a child process to execute or open a program file, built-in commands are faster and more efficient. A list of GNU Bash shell built-in commands is provided in [Appendix A](appendix#a "Appendix A").

Be aware that some commands have multiple flavors. For example, both `echo` and `pwd` have a built-in command flavor as well as an external command flavor. These flavors are slightly different. To see multiple flavors for commands, use the `-a` option on the `type` command:

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

> **TIP**
> To use the external command for a command that has multiple flavors, directly reference the file. For example, to use the `pwd` external command, type `/usr/bin/pwd`.

## Using the *history* command

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

> **TIP**
> You can set the number of commands to keep in the Bash history. To do so, you need to modify an environment variable called `HISTSIZE` (see Chapter 6).

You can recall and reuse the last command in your history list. This can save time and typing. To recall and reuse your last command, type `!!` and press the Enter key:

```
$ ps --forest
PID TTY TIME CMD
2367 pts/0 00:00:00 bash
5240 pts/0 00:00:00 \_ ps
$
$ !!
ps --forest
PID TTY TIME CMD
2367 pts/0 00:00:00 bash
5241 pts/0 00:00:00 \_ ps
$
```

When `!!` was entered, the Bash shell first displayed the command it was recalling from the shell's history. And after the command was displayed, it was executed.

Command history is kept in the hidden `.bash_history` file, which is located in each user's home directory:

```
$ pwd
/home/christine
$
$ ls .bash_history
.bash_history
$
```

Be aware that during your CLI session, the `bash` command history is stored in memory. It is only written out into the history file when the
