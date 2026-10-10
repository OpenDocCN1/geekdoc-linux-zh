
Often, you see a distribution with its default system shell (`sh`) pointing to the Bash shell using a soft link. An example of this is shown here on a CentOS distribution:

```bash
$ which sh
/usr/bin/sh
$ ls -l /usr/bin/sh
lrwxrwxrwx. 1 root root 4 Nov  8 11:30 /usr/bin/sh -> bash
$
```

However, be aware that on some distributions, the default system shell is linked differently, such as on this Ubuntu distribution:

```bash
$ which sh
/usr/bin/sh
$ ls -l /usr/bin/sh
lrwxrwxrwx 1 root root 4 Mar 10 18:43 /usr/bin/sh -> dash
$
```

In this case, the default system shell, `/usr/bin/sh`, points to the Dash shell, instead of the Bash shell.

> **TIP**
>
> For Bash shell scripts, these two different shells, default interactive shell and default system shell, can cause problems. Be sure to read about the important syntax needed for a Bash shell script's first line in Chapter 11, "Basic Script Building," to avoid these issues.

You are not forced to stick with your default interactive shell. You can start any shell available on your distribution simply by typing its name. However, there's no fanfare or message displayed to indicate what shell you are currently using. But help is available from the `$0` variable. The command `echo $0` will display the name of your current shell, providing the needed reference.

> **NOTE**
>
> The `echo $0` command shows the current shell in use only when issued at a shell prompt. If used in a shell script, it will display the script's name instead. This is covered in Chapter 14, “Handling User Input.”

With our handy `$0` variable, we'll display the shell we are currently using, start the Dash shell by typing the command `dash`, and show the new shell's name via `echo $0` again:

```bash
$ echo $0
-bash
$
$ dash
$
$ echo $0
dash
$
```

> **NOTE**
>
> In the previous example, notice the dash (`-`) in front of the `bash` response from the first `echo $0` command. This indicates that this shell is the user's login shell.

The `$` prompt is a CLI prompt for the Dash shell. You can leave the Dash shell program (and the Bash shell for that matter) by typing the command `exit`:

```bash
$ echo $0
dash
$ exit
$ echo $0
-bash
$
```

Jumping back and forth through the various shells seems simple, but there is more to the action happening behind the scenes. To understand this process, the next section explores the relationship between a login shell program and a newly started shell program.

### Exploring Parent and Child Shell Relationships

The default interactive shell (login shell) that starts when a user logs into a virtual console terminal or starts a terminal emulator in the GUI is a *parent shell*. As you have read so far in this book, a parent shell process provides a CLI prompt and waits for commands to be entered. When the `bash` command (or other shell program name) is entered at the CLI prompt, a new shell program is created. This is a *child shell*. A child shell also has a CLI prompt and waits for commands to be entered.

Because you do not see any relevant messages when you type `bash` and spawn a child shell, another command can help bring clarity. The `ps` command was covered in *Chapter 4*, “More Bash Shell Commands.” Using this with the `-f` option before and after entering a child shell is useful:

```bash
$ ps -f
UID     PID  PPID  C STIME TTY          TIME CMD
christi+ 6160  6156  0 11:01 pts/1    00:00:00 -bash
christi+ 7141  6160  0 12:51 pts/1    00:00:00 ps -f
$
$ bash
$
$ ps -f
UID     PID  PPID  C STIME TTY          TIME CMD
christi+ 6160  6156  0 11:01 pts/1    00:00:00 -bash
christi+ 7142  6160  0 12:52 pts/1    00:00:00 bash
christi+ 7164  7142  0 12:52 pts/1    00:00:00 ps -f
$
```

The first use of `ps -f` shows two processes. One process has a process ID of 6160 (second column) and is running the Bash shell program (last column). The second process (process ID 7141) is the actual `ps -f` command running.

> **NOTE**
>
> A process is a running program. The Bash shell is a program, and when it runs, it is a process. A running shell is simply one type of process. Therefore, when reading about running a Bash shell, you often see the word “shell” and the word “process” used interchangeably.

In the previous example, after the command `bash` is entered, a child shell is created. The second `ps -f` is executed from within the child shell. From this display, you can see that *two* Bash shell programs are running. The first Bash shell program, the parent shell process, has the original process ID (PID) of 6160. The second Bash shell program, the child shell process, has a PID of 7142. Note that the child shell has a parent process ID (PPID) of 6160, denoting that the parent shell process is its parent. Figure 5-1 diagrams this relationship.

![](img/a5025f22e05b92f409563a958cac7312_179_0.png)

**FIGURE 5-1** Parent and child Bash shell processes

When a child shell process is spawned, only some of the parent's environment is copied to the child's shell environment. This can cause problems with items such as variables. How to prevent such problems is covered in *Chapter 6*, “Using Linux Environment Variables.”

A child shell is also called a *subshell*. A subshell can be created from a parent shell, and a subshell can be created from another subshell:

```bash
$ ps -f
  UID          PID  PPID  C STIME TTY              TIME CMD
christi+     7650  7649  0 16:01 pts/0    00:00:00 -bash
christi+     7686  7650  0 16:02 pts/0    00:00:00 ps -f
$
$ bash
$ bash
$ bash
$
$ ps --forest
  PID TTY          TIME CMD
 7650 pts/0        00:00:00 bash
 7687 pts/0        00:00:00 \_ bash
 7709 pts/0        00:00:00    \_ bash
 7731 pts/0        00:00:00      \_ bash
 7753 pts/0        00:00:00        \_ ps
$
```

In the preceding example, the `bash` command was entered three times. Effectively, this created three subshells. The `ps --forest` command shows the nesting of these subshells. **Figure 5-2** also shows this subshell nesting.

The `ps -f` command can be useful in subshell nesting, because it displays who is whose parent via the PPID column:

```bash
$ ps -f
  UID         PID   PPID  C STIME TTY          TIME CMD
christi+    7650   7649  0 16:01 pts/0    00:00:00 -bash
christi+    7687   7650  0 16:02 pts/0    00:00:00 bash
christi+    7709   7687  0 16:02 pts/0    00:00:00 bash
christi+    7731   7709  0 16:02 pts/0    00:00:00 bash
christi+    7781   7731  0 16:04 pts/0    00:00:00 ps -f
$
```

The Bash shell program can use command-line options to modify the shell's start. **Table 5-1** lists a few of these available switches to use with the `bash` command.

![](img/a5025f22e05b92f409563a958cac7312_181_0.png)

**FIGURE 5-2** Subshell nesting

### TABLE 5-1 The bash Command-Line Options

| Option | Description |
|---|---|
| `-c string` | Reads commands from *string* and processes them |
| `-i` | Starts an interactive shell, allowing input from the user |
| `-l` | Acts as if invoked as a login shell |
| `-r` | Starts a restricted shell, limiting the user to the default directory |
| `-s` | Reads commands from the standard input |

You can find more help on the `bash` command and even more command-line parameters by typing `man bash`. The `bash --help` command provides additional assistance as well.

> **TIP**
>
> If you'd like to see the version of the Bash shell, just type `bash --version` at the command line. This won't create a subshell, but instead displays the current version of your system's GNU Bash shell program.

You can gracefully exit out of each subshell by entering the `exit` command:

```bash
$ ps -f
UID        PID PPID C STIME TTY        TIME CMD
christi+  7650 7649 0 16:01 pts/0    00:00:00 -bash
christi+  7687 7650 0 16:02 pts/0    00:00:00 bash
christi+  7709 7687 0 16:02 pts/0    00:00:00 bash
christi+  7731 7709 0 16:02 pts/0    00:00:00 bash
christi+  8081 7731 0 16:35 pts/0    00:00:00 ps -f
$
$ exit
exit
$
$ ps --forest
  PID TTY          TIME CMD
 7650 pts/0    00:00:00 bash
 7687 pts/0    00:00:00 \_ bash
 7709 pts/0    00:00:00   \_ bash
 8081 pts/0    00:00:00     \_ ps
$
$ exit
exit
$ exit
exit
$
```
