
## Review

In this session, you tried out many key features of the Bash shell—the Linux command interpreter. Among other things, you learned the syntax of commands, how you can combine commands, how to run commands in the background, and how to use aliases.

## Quiz Yourself

- 1. What is the shell and what does it do? (See "Using the Bash Shell.")
- 2. How would you continue a long command on multiple lines? (See "Combining commands.")
- 3. How do you save the output of a Linux command in a file? (See "Redirecting command input and output.")
- 4. What are aliases and why would you use them? (See "Using aliases for commands.")
- 5. What keys would you press to get the second virtual console? (See "Using virtual consoles.")

# SESSION 7

## Learning Linux Commands

### Session Checklist

- Reviewing commands you've learned so far
- Commands for managing processes
- Useful date and time commands
- Commands for working with text files
- File-system maintenance commands

In this session, you'll review the commands you learned in previous sessions and be introduced to a few Linux commands from several categories. However, because of the large number of Linux commands, you cannot really explore each and every command in a half-hour session. You'll try out more commands in later sessions. To begin this session, log in at the graphical login screen and open a terminal window. You can then type the commands in that login screen.

## Reviewing Commands You've Learned So Far

You've already tried quite a few Linux commands in previous sessions. Browse through Table 7-1 to refresh your memory about these commands. We organized them in categories for your convenience.

### Table 7-1 Linux Commands You've Learned in Previous Sessions

| Command Category and Name | Description |
|---------------------------|------------|
| **Getting Online Help** | |
| help | Displays a list of Bash built-in commands. Type `help` at a Bash prompt. |
| help *command* | Displays help text for the Bash built-in command named *command*. Type `help cd` for help with Bash's built-in cd command. |
| man | Displays online help information. Type `man ls` for help with the `ls` command. |
| **Making Commands Easier** | |
| alias | Defines an abbreviation (shortcut) for a long command. Type `alias` alone to view all currently defined aliases. Type `alias topdir="~"` and then type `topdir` to change the directory to the root directory (`/`). |
| unalias | Deletes an abbreviation defined using `alias`. Type `unalias topdir` to undefine the `topdir` abbreviation. |
| **Managing Files and Directories** | |
| cd | Changes the current directory. Type `cd /usr` to change to the `/usr` directory. |
| chmod | Changes file permissions. Type `chmod +x filename` to make that file executable (replace *filename* with the name of an existing file). |
| cp | Copies files. Type `cp` to change the directory to your home directory. Then type `cp /etc/X11/XF86Config .` to copy a file to your home directory. |
| ls | Displays the contents of a directory. Type `ls -F` to see the contents of the current directory. |
| mkdir | Creates a directory. Type `cd` to change to your home directory and then type `mkdir temp` to create a directory named *temp*. |
| mv | Renames a file or moves it from one directory to another. Type `mv filename1 filename2` to change a file's name; use an existing file's name for *filename1*. |
| rm | Deletes files. The syntax is `rm filename`. (Use with caution because the file gets deleted.) |
| rm dir | Deletes directories. Type `rm dir -temp` to remove the directory named *temp* from your home directory (see the `mkdir` command earlier in this table). |
| pwd | Displays the current directory. Type `pwd` to see the current directory name. |

## Finding Files

find: Finds files based on specified criteria such as name, size, and so on. Type `find /usr -name "README*" -print` to try this command.

## Processing Files

cat: Displays a file on standard output (can concatenate several files into one big file). Type `cd` to go to your home directory and then type `cat .bash_profile` to see the contents of that file.

grep: Searches for regular expressions within a text file. Type `cd` to go to your home directory and then type `grep BASH .b*` to see the result of searching for the string, BASH, in specified files.

more: Displays a text file one page at a time. Type `more /etc/inittab` to see the contents one page at a time. (Press the spacebar to advance or type `q` to quit.)

## Managing Users

passwd: Changes the password. Type `passwd` and follow the prompts to change your password.

su: Becomes another user or root when invoked without any argument. Type `su` and enter the root password when prompted. Be careful what you do because now you are the super user. Type `exit` to return to normal user.

The following sections cover new commands, by category, that were not covered in the earlier sessions.

## Commands for Managing Processes

Every time the shell acts on a command that you type, it starts a process, a single instance of a running program. The shell itself is a process, as are any scripts or applications that it executes. You can use the `ps` command to see a list of processes. When you type `ps -x`, for example, Bash shows you the current set of processes. Following is partial output from the command. I also included the `-cols 132` option to ensure that you can see each command in its entirety:

```text
ps -x --cols 132
  PID TTY  STAT TIME COMMAND
  1  ?    S     0:05 init [5]
  325 ?  S     0:00 syslogd -m 0
```

```text
335 ? S 0:00 *clockd
480 ? S 0:00 crond
511 ? S 0:00 xinetd reuse pidfile /var/run/xinetd.pid
580 ? S 0:00 sendmail: accepting connections
596 ? S 0:00 gpm -t imp2
849 ? S 0:01 /usr/bin/gnome-session
853 ? S 0:00 gnome-apropos --sm-client-id default0
901 ? S 0:02 sawfish --sm-client-id=default0
967 ? S 8:36 magic --sm-client-id=default12
985 ? S 0:00 gnome-name-service
994 ? S 0:01 panel --sm-client-id default1
1001 ? S 0:00 gmc --nomindows --sm-client-id default8
2143 ? S 0:00 gnome-terminal --use-factory --start-factory-server
21433 ? S 0:00 gnome-pty-helper
21444 pts/5 S 0:00 bash
21455 pts/0 R 0:00 ps x --cols 132
```

In the preceding output, the **COMMAND** column shows the commands that create the processes. This list shows the Bash shell and the `ps` command as processes. Other processes include all the programs that the shell starts when you log in at the graphical login screen and start a GNOME session. In particular, the list includes the `sawfish` (window manager) process and the `gnome-terminal` (terminal window) process. Note that `ps` even shows its own process as the last one in the list.

The default `ps x` command does not provide all the processes running on a Linux system. What `ps x` shows are the commands that you start either directly or indirectly through shell scripts that run automatically when you log in. To see the full complement of processes, use the `a` option of the `ps` command together with the `x` option as follows:

```text
ps -ax
```

If you study the output of the `ps` command, you find that the first column has the heading PID and that it shows a number for each process. PID stands for process ID (identification), which is a sequential number assigned by the Linux kernel. If you look through the output of the `ps ax` command, you should see that the `init` command is the first process; it has a PID or process number of 1. That’s why `init` is referred to as the mother of all processes.

## Date and Time Commands

You can use the `date` command to display the current date and time or set a new date and time. Type `date` at the shell prompt and you get a result similar to the following:

```text
date
Wed Jun 13 19:46:31 MDT 2001
```

You can also format the way you want the date or time to appear. For example, to view the date alone (without the current time), try the following command:

```text
date "+%A %B %d %Y"
Wednesday June 13 2001
```
