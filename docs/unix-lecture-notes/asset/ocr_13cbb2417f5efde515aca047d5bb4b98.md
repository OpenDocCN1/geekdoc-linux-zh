The printenv command displays the values of all environment variables as does the env command. Within a program the getenv() function can be used to retrieve a particular environment string, as in

```
char* username = getenv("LOGNAME");
printf("The user's user-name is %s\n, username);
```

The operating system also makes available to every running program an external global variable

```
extern char **environ;
```

which is a pointer to the start of the array of the name-value pairs in the running program's environment. Programs can read and modify these variables if they choose. For example, a program that needs to know how many columns are in the current terminal window will query the COLUMNS variable, whereas other programs may just ignore it.

# 1.3.6 Shells

The kernel provides services to processes, not to users; users interact with UNIX through a command-line interface called a shell. The word "shell" is the UNIX term for a particular type of command-line interpreter. Command-line interpreters have been in operating systems since they were first created. DOS uses a command-line-interpreter, as is the Command window of Microsoft Windows, which is simply a DOS emulator. The way that DOS and the Command window are used is similar to the way that UNIX is used: you type a command and press the Enter key, and the command is executed, after which the prompt reappears. The program that displays the prompt, reads the input you type, runs the appropriate programs in response and re-displays the prompt is the command-line-interpreter, which in UNIX is called a shell.

In UNIX, a shell is much more than a command-line-interpreter. It can do more than just read simple commands and execute them. A shell is also programming language interpreter; it allows the user to define variables, evaluate expressions, use conditional control-of-flow statements such as while- and if-statements, and make calls to other programs. A sequence of shell commands can be saved into a file and executed as a program by typing the name of the file. Such a sequence of shell commands is called a shell script. When a shell script is run, the operating system starts up a shell process to read the instructions and execute them.

# 1.3.7 Online Documentation: The Man Pages

Shortly after Ritchie and Thompson wrote the first version of UNIX, at the insistence of their manager, Doug McIlroy, in 1971, they wrote the UNIX Programmer's Manual. This manual was initially a single volume, but in short course it was extended into a set of seven volumes, organized by topic. It existed in both printed form and as formatted files for display on an ordinary character display device. Over time it grew in size. Every UNIX distribution comes with this set of manual pages, called "manpages" for short. Appendix B.4 contains a brief description of the structure of the manpages, and Chapter 2 provides more detail about how to use them.

> 14 This is not a coincidence. Long before Microsoft wrote MS-DOS, they wrote a version of UNIX for the PC called Xenix, whose rights they sold to Santa Cruz Operations in 1987