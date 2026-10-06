Because users often prefer different shells, multiuser systems can have a number of different shells in use at any given time. The choice of shells demonstrates one of the powers of the GNU/Linux operating system: the ability to provide a customized user interface.

Besides its function of interpreting commands from a terminal or workstation keyboard and sending them to the operating system, the shell is a high-level programming language. Shell commands can be arranged in a file for later execution (DOS and MS Windows call this a batch file). This flexibility allows users to perform complex operations with relative ease, often with rather short commands, or to build elaborate programs that perform highly complex operations with surprisingly little effort.

# Filename Generation

When you are typing commands to be processed by the shell, you can construct patterns using characters that have special meanings to the shell. These patterns are a kind of shorthand: Rather than typing in complete filenames, users can type in patterns, and the shell expands them into matching filenames. A pattern can save the effort of typing in a long filename or a long series of similar filenames. Patterns can also be useful when you know only part of a filename or cannot remember the exact spelling.

# Device-Independent Input and Output

Devices (such as a printer or terminal) and disk files all as files to GNU/Linux programs. When you give the GNU/Linux operating system command, you can instruct it to send the output to any one of several devices or files. This diversion is called output redirection.

In a similar manner a program's input that normally comes from a terminal can be redirected so that it comes from a disk file. Input and output are device independent; they can be redirected to or from any appropriate device.

As an example, the cat utility normally displays the contents of a file on the terminal screen. When you run a cat command, you can easily cause its output to go to a disk file instead of the terminal.

# Shell Functions

One of the most important features of the shell is that users can use it as a programming language. Because the shell is an interpreter, it does not compile programs written for it it interprets them each time they are loaded from the disk. Loading and interpreting programs can be time-consuming.

Many shells, including bash and zsh, include shell functions that the shell holds in memory so it does not have to read them from the disk each time you want to execute them. The shell also keeps functions in an internal format so it does not have to spend as much time interpreting them.