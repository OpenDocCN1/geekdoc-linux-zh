# Part I: Getting Started in Fedora and RHEL

Many processes running on a computer are not associated with a terminal. A normal Linux system has many processes running in the background. Background system processes perform tasks as logging system activity or listening for data coming from the network. They are often started when Linux boots up and run continuously until it shuts down. To see and monitor all the processes on your Linux system, type:

```
$ ps au
```

I added the (|) and the less command to allow you to page through the many processes that will appear on your screen. A pipe lets you direct the output of one command to be the input of the next. Use the spacebar to page through, and press q to end the list. You can also use the arrow keys to move one line at a time through the output.

# Exiting the shell

To exit the shell when you are done, type exit or press Ctrl+D.

I showed a few commands designed to familiarize you quickly with your Linux system. Hundreds of other commands that you can contain in directories such as /bin and /usr/bin. There are also administrative commands in /bin or /usr/bin directories. Many of these commands are described in the remainder of this chapter.

# Understanding the Shell

Before icons and windows took over screens, you typed commands to interact with most computers. On UNIX systems, from Linux was derived, the program used to interpret and manage commands was referred to as the shell.

The shell provides a way to run programs, work with the file system, compile computer code, and manage the computer. Although the shell is less intuitive than GUIs, most Linux experts prefer the shell to be much more powerful than GUIs. Shell have been around for long, many advanced features have been built into them. Many old-Linux administrators and programmers use a GUI to open lots of shells.

The shell illustrated in this picture is called the bash shell, which stands for Bourne Again Shell. The name is derived from the fact that bash is compatible with the first UNIX shell: the sh. Other shells include the C shell (csh), which is popular among BSD users, and the Korn shell (ksh), which is popular among. Linux also has a tsh (a C shell look-alike) and an ash shell (another Bourne shell look-alike).

> NOTE: While you can invoke the Bourne shell with /bin/sh, the command actually runs the bash shell in sh compatibility mode. Running /bin/sh produces a shell that behaves more like sh than bash, you will probably be able to use bash scripting that the real Bourne shell wouldn't recognize. The sh still exists primarily for compatibility with scripts that were written specifically for that shell.