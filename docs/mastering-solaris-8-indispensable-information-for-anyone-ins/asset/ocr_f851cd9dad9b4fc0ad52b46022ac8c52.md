prompt. The default time is 600 seconds (10 minutes). If MAILCHECK is not set, the shell will not check for mail at all.

The Prompt the User (primary), or PS1, variable (a $ prompt in the csh shell) tells you that the shell is waiting for you to give it a command. A $ followed by a space is the usual prompt. It is stored as a string in the PS1 variable. If you want to change the appearance of your prompt, you may change the value of the variable.

The Prompt the User (secondary) variable is stored in a string in PS2. This variable is used with unclosed quotes on the first line. Unclosed quotes tell the shell that the command is not finished. The shell will then respond with the default prompt (>), which indicates that the shell is waiting for the user to complete the response. The shell will wait for the closing quotation marks before it executes the command.

The IFS variable is used to specify what characters you use to separate arguments on the command line. It has a default value of SPACE TAB NEWLINE, which means that you may use a space or tab on the command line if these characters are not quoted. IFS can have an impact on the interpretation of a command line by means of word splitting. The following example demonstrates how:

```
$ barries=I:m:n:0
$ cat $barries
cat: cannot open I:m:n:0
$IFS=':'
$ cat $barrriers
cat: cannot open I
cat: cannot open m
cat: cannot open n
cat: cannot open o
```

> **WARNING** The IFS variable should be used sparingly. It is usually reserved for use with shell scripts, where it will not affect the parent. You should have a complete understanding of how it works in relation to the parent/child process.

# Built-Ins

Built-ins are commands that are built in to the shell and are always available, making a directory search redundant. The shells recognize built-ins and execute them without spawning a new process. If a command is not recognized as a built-in, then the shell will search the directory for the correct program.