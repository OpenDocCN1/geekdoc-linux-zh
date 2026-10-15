![](bbox=[0.295, 0.185, 0.705, 0.365])

Figure B.2: The shell: A user's view of UNIX.

specified in the user's entry in a file called the password file. The system administrator can change this entry, but very often the chsh command available on some systems can also be used by the user to change shells. In some versions of UNIX, the user can also use the command passwd -s to change the login shell.

# B.5.0.1 Shell Features

In all shells, a simple command is of the form

```
$ commandname command-options arg1 arg2 ... argn
```

The shell waits for a newline character to be typed before it attempts to interpret (parse) a command. A newline signals the end of the command. Once it receives the entered line, it checks to see if commandname is a built-in shell command (A built-in command is one that is hard-coded into the shell itself.) If it is, it executes the command. If not, it searches for a file whose name, either relative or absolute, is commandname. (How that search takes place is explained in a later chapter.) If it finds one, this file is loaded into memory and the shell creates a child process to execute the command, using the arguments from the command line. When the command is finished, the child process terminates and the shell resumes its execution.

In addition to command interpretation, all shells provide

+   - redirection of the input and output of commands
+   - pipes – a method of channeling the output of one command to the input of another
+   - scripting – a method of writing shell programs that can be executed as files
+   - file name substitution using metacharacters
+   - control flow constructs such as loops and conditional execution

Shells written after the Bourne shell also provide

+   - history mechanism – a method of saving and reissuing commands in whole or in part