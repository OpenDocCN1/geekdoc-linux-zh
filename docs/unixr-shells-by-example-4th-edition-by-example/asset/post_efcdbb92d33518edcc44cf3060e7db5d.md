
## EXPLANATION

- 1 The stty command sets options for the terminal. Input characters will not be stripped to seven bits if -istrip is used.
- 2 The stty command sets Ctrl-H, the Backspace key, to erase.
- 3 Any line beginning with # is a comment. It is not an executable statement.
- 4 If the current terminal window (tty) is the console (linux), the next line is executed; otherwise, program control goes to the last endif.
- 5 This line is echoed to the screen, and if the user does not press Ctrl-C to kill the process, the program will sleep (pause) for five seconds, and then the X Windows program will start.
- 6 The startx program launches X Windows if this system is Linux.
- 7 The endif marks the end of the innermost if construct.
- 8 The autologout variable is set to 60 so that after 60 minutes of inactivity, the user will automatically be logged out (from the login shell).

## 9.2.2 The Search Path

The path variable is used by the shell to locate commands typed at the command line. The search is from left to right. The dot represents the current working directory. If the command is not found in any of the directories listed in the path, or in the present working directory, the shell sends the message Command not found to standard error. It is recommended that the path be set in the .login file.1 The search path is set differently in the C/TC shell than it is in the Bourne and Korn shells. Each of the elements is separated by whitespace.

```
set path = (/usr/bin /usr/ucb /bin /usr .)
echo $path
/usr/bin /usr/ucb /bin /usr .
```

The environment variable PATH will display as

```
echo $PATH
/usr/bin:/usr/ucb:/bin:/usr:.
```

The C/TC shell internally updates the environment variable for PATH to maintain compatibility with other programs (such as the Bourne or Korn shells) that may be started from this shell and will need to use the path variable.

> 1. Do not confuse the search path variable with the cpath variable set in the .cshrc file.

## 9.2.3 The rehash Command

The shell builds an internal hash table consisting of the contents of the directories listed in the search path. (If the dot is in the search path, the files in the dot directory, the current working directory, are not put in the hash table.) For efficiency, the shell uses the hash table to find commands that are typed at the command line, rather than searching the path each time. If a new command is added to one of the directories already listed in the search path, the internal hash table must be recomputed. This is done by typing

```
% rehash
```

(The % is the C shell prompt.) The hash table is also automatically recomputed when you change your path at the prompt or start another shell.

## 9.2.4 The hashstat Command

The hashstat command displays performance statistics to show the effectiveness of its search for commands from the hash table. The statistics are in terms of "hits" and "misses." If the shell finds most of its commands you use at the end of your path, it has to work harder than if they were at the front of the path, resulting in a higher number of misses than hits. In such cases, you can put the most heavily hit directory toward the front of the path to improve performance.

```
% hashstat
2 hits, 13 misses, 13%²
```

## 9.2.5 The source Command

The source command is a shell built-in command, that is, part of the shell's internal code. It is used to execute a command or set of commands from a file. Normally, when a command is executed, the shell forks a child process to execute the command, so that any changes made will not affect the original shell, called the parent shell. The source command causes the program to be executed in the current shell, so that any variables set within the file will become part of the environment of the current shell. The source command is normally used to re-execute the .cshrc or .login if either has been modified. For example, if the path is changed after logging in, type

```
% source .login or .cshrc
```
