
finishes execution and then, if necessary, will report the status of the exiting program. A prompt will appear and the whole process will start again. The order of processing the command line is as follows:

- 1. History substitution is performed (if applicable).
- 2. Command line is broken up into tokens, or words.
- 3. History is updated (if applicable).
- 4. Quotes are processed.
- 5. Alias substitution and functions are defined (if applicable).
- 6. Redirection, background, and pipes are set up.
- 7. Variable substitution ($user, $name, etc.) is performed.
- 8. Command substitution (echo "Today is `date`") is performed.
- 9. Filename substitution, called globbing (cat abc.??, rm *.c, etc.) is performed.
- 10. Command is executed.

## 1.4.2 Types of Commands

When a command is executed, it is an alias, a function, a built-in command, or an executable program residing on disk. Aliases are abbreviations (nicknames) for existing commands and apply to the C, TC, Bash, and Korn shells. Functions apply to the Bourne (introduced with AT&T System V, Release 2.0), Bash, and Korn shells. They are groups of commands organized as separate routines. Aliases and functions are defined within the shell's memory. Built-in commands are internal routines in the shell, and executable programs reside on disk. The shell uses the path variable to locate the executable programs on disk and forks a child process before the command can be executed. This takes time. When the shell is ready to execute the command, it evaluates command types in the following order:

- 1. Aliases
- 2. Keywords
- 3. Functions
- 4. Built-in commands
- 5. Executable programs

If, for example, the command is xyz the shell will check to see if xyz is an alias. If not, is it a built-in command or a function? If neither of those, it must be an executable program residing on the disk. In order to execute the command, the shell must then search the path to find out where the command is located in the directory structure in order to execute it. This process is illustrated in Figure 1.2.

![](img/60a0b5d254bd6007403850f972cbfad8_48_0.png)

Figure 1.2 The shell and command execution.

## 1.5 Processes and the Shell

A process is a program in execution and can be identified by its unique PID number. The kernel controls and manages processes. A process consists of the executable program, its data and stack, program and stack pointer, registers, and all the information needed for the program to run. The shell is a special program that starts when you have completed the login process. Once started, the shell is a process. The shell belongs to a process group identified by the group's PID. Only one process group has control of the terminal at a time and is said to be running in the foreground. When you log on, your shell is in control of the terminal and waits for you to type a command at the prompt.

When you log on, your system may go directly into a graphical user interface (GUI) or start up in a terminal with a shell prompt. If you are using Linux, the shell normally starts up another process to launch the X Window System. After X Windows starts, a window manager process (twm, fvwm, etc.) is executed, providing a virtual desktop. Then, from a pop-up menu, you can start up a number of other processes, such as xterm (gets a terminal), xman (provides manual pages), or emacs (starts a text editor). If you are using UNIX, the GUI may be CDE, KDE, or OpenWindows. Once started, you will have a virtual desktop consisting of a number of smaller windows, including a console and a number of terminals, each displaying a shell prompt.

Multiple processes are running and monitored by the Linux/UNIX kernel, allocating each of the processes a little slice of the CPU in a way that is unnoticeable to the user.

### 1.5.1 What Processes Are Running?

**The ps Command.** The ps command with its many options displays a list of the processes currently running in a number of formats. Example 1.2 shows all processes that are running by users on a Linux system. (See Appendix A for ps and its options.)

### Example 1.2

```
$ ps aux (BSD/Linux ps) (use ps -ef for SVR4)
```

| USER | PID | %CPU | %MEM | SIZE | RSS | TTY | STAT | START | TIME | COMMAND |
|---|---|---|---|---|---|---|---|---|---|---|
| ellie | 456 | 0.0 | 1.3 | 1268 | 840 | 1 | S | 13:23 | 0:00 | -bash |
| ellie | 476 | 0.0 | 1.0 | 1200 | 648 | 1 | S | 13:23 | 0:00 | sh /usr/X11R6/bin/sta |
| ellie | 478 | 0.0 | 1.0 | 2028 | 676 | 1 | S | 13:23 | 0:00 | xinit /home/ellie/.xi |
| ellie | 480 | 0.0 | 1.6 | 1852 | 1068 | 1 | S | 13:23 | 0:00 | fvwm2 |
| ellie | 483 | 0.0 | 1.3 | 1660 | 856 | 1 | S | 13:23 | 0:00 | /usr/X11R6/lib/X11/fv |
| ellie | 484 | 0.0 | 1.3 | 1696 | 868 | 1 | S | 13:23 | 0:00 | /usr/X11R6/lib/X11/fv |
| ellie | 487 | 0.0 | 2.0 | 2348 | 1304 | 1 | S | 13:23 | 0:00 | xclock -bg #0c0c0c -p |
| ellie | 488 | 0.0 | 1.1 | 1620 | 724 | 1 | S | 13:23 | 0:00 | /usr/X11R6/lib/X11/fv |
| ellie | 489 | 0.0 | 2.0 | 2364 | 1344 | 1 | S | 13:23 | 0:00 | xload -nolabel -bg gr |
| ellie | 495 | 0.0 | 1.3 | 1272 | 848 | p0 | S | 13:24 | 0:00 | -bash |
| ellie | 797 | 0.0 | 0.7 | 852 | 484 | p0 | R | 14:03 | 0:00 | ps au |
| root | 457 | 0.0 | 0.4 | 724 | 296 | 2 | S | 13:23 | 0:00 | /sbin/mingetty tty2 |
| root | 458 | 0.0 | 0.4 | 724 | 296 | 3 | S | 13:23 | 0:00 | /sbin/mingetty tty3 |
| root | 459 | 0.0 | 0.4 | 724 | 296 | 4 | S | 13:23 | 0:00 | /sbin/mingetty tty4 |
| root | 460 | 0.0 | 0.4 | 724 | 296 | 5 | S | 13:23 | 0:00 | /sbin/mingetty tty5 |
| root | 461 | 0.0 | 0.4 | 724 | 296 | 6 | S | 13:23 | 0:00 | /sbin/mingetty tty6 |
| root | 479 | 0.0 | 4.5 | 12092 | 2896 | 1 | S | 13:23 | 0:01 | X :0 |
| root | 494 | 0.0 | 2.5 | 2768 | 1632 | 1 | S | 13:24 | 0:00 | xterm -ls -sb -fn |

- 5. A number of desktop environments come with Linux, including Gnome, KDE, X, and so on.
