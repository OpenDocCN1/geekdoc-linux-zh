
If your path variable includes the /bin directory, you can simply use the csh command, instead of using the /bin/csh command.

The third method, which is also the most commonly used method, is to force the current shell to execute a script in the C shell, regardless of your current shell. You can do so by beginning a shell script with the following line:

```
#!/bin/csh
```

When your current shell encounters the string #!, it takes the rest of the line as the absolute pathname for the shell to be executed, under which the script in the file is executed.

Throughout this chapter, we would use the chmod u+x script_file command to make script_file executable by the owner of the file and run the script by using the ./script_file command.

## 14.3 SHELL VARIABLES AND RELATED COMMANDS

A variable is a main memory location that is given a name. This allows you to reference the memory location by using its name instead of its address. The name of a shell variable is comprised of digits, letters, and underscores, with the first character being a letter or underscore. Because the main memory is read/write storage, you can read a variable's value or assign it a new value. Under the C shell, the value of a variable can be a string of characters or a numeric value. There is no theoretical limit to the length of a variable's value stored as a string; the practical limit is dictated by the length of a line.

Shell variables can be one of two types: shell environment variables and user-defined variables. You can use environment variables to customize the environment in which your shell runs and for proper execution of shell commands. A copy of these variables is passed to every command that executes in the shell as its child. Most of these variables are initialized when the login script(s) execute(s), according to the environment set by your system administrator. You can further customize your environment by assigning appropriate values to some or all of these variables in your ~/.login and ~/.cshrc start-up files, which also execute when you log on. See Chapter 2 for a discussion of start-up files. Table 14.1 lists most of the environment variables whose values you can change.

The shell environment variables listed in Table 14.1 are writable, meaning that you can assign them any values to make your shell environment meet your needs. Other shell environment variables are read only. That is, you can use (read) the values of these variables, but you cannot change them directly. These variables are most useful for processing command line arguments (also known as positional arguments), the parameters passed to a shell script at the command line. Examples of command line arguments are the source and destination files in the cp command. Some other read-only shell variables are used to keep track of the process ID of the current process, the process ID of the most recent background process, and the exit status of the last command. Some important read-only shell environment variables are listed in Table 14.2.

User-defined variables are used within shell scripts as temporary storage places whose values can be changed when the program executes. These variables can be made global and passed to the commands that execute in the shell script in which they are defined. As with most programming languages, you have to declare C shell variables before using them. A reference to a C shell variable that has not been declared results in an error.

You can display the values of all shell variables (environmental and user-defined) and their current values by using the set command without any argument. The following is a sample run of the set command on a machine running PC-BSD.

```
% set
_
addsuffix
anyerror
argv ()
autocorrect
autoexpand
autolist      ambiguous
autorehash
complete      enhance
correct       cmd
csubstonl
```

### TABLE 14.1 Some Important Writable C Shell Environment Variables

| Environment Variable | Purpose of the Variable |
|---|---|
| cdpath | Directory names that are searched, one by one, by the cd command to find the directory passed to it as a parameter; the cd command searches the current directory if this variable is not set |
| home | Name of your home directory, the C shell places you in this directory when you first log on |
| mail | Name of your system mailbox file |
| path | Variable that contains your search path—the directories that a shell searches to find an external command or program that you try to run |
| prompt | Primary shell prompt that appears on the command line, usually set to % |
| prompt2 | Secondary shell prompt displayed on the second line of a command if the shell thinks that the typed command is not complete, typically when the command line terminates with a backslash (\), the escape character |
| cwd | Name of the current working directory |
| term | Type of user's console terminal |

### TABLE 14.2 Some Important Read-Only C Shell Environment Variables

| Environment Variable | Purpose of the Variable |
|---|---|
| $argv[0] or $0 | Name of the executing program |
| $number or ${number} | Equivalent to $argv[number], where number may be 0, 1, 2, ... |
| $argv[*] or $* | Values of all of the command line arguments |
| $#argv or $# | Total number of command line arguments |
| $$ | Process ID (PID) of the current process; typically used as a file name extension to create (most probably) unique file names |
| $! | PID of the most recent background process |
