The first example uses the newer syntax of the bash shell. The second shows the older Bourne Shell syntax using the backward apostrophe. Both of these commands will output the pwd. Either one works with the bash shell.

The advantage of using command substitution is most obvious in scripting. It enables you to use a command's output as input to another command. So, if you wanted to use the name of the working directory as an argument to another command, you could use command substitution.

# ## Processes

A shell is both a command interpreter and a programming language. Commands may be run either one at a time (synchronously) or more than one at a time (asynchronously).

When running synchronous commands the shell waits for the command to finish before accepting additional input. This is also referred to as running the process in the foreground.

An asynchronous command executes at the same time the shell executes other commands. This is known as running a process in the background.

All shells provide control of input and output of commands through redirection. Usually, redirection of input is initiated by the < character, whereas redirection of output is accomplished through the use of the > character.

For example, the command ls -ltr > MyFile110 sends the output of the command ls -ltr to a file called MyFile110. The command cat < MyFile110 passes the file MyFile110 as input to the cat command.

As you remember from Chapter 4, “File Management,” cat is used for displaying the contents of a file. The previous example would produce the same results as typing cat MyFile110.

The use of redirection provides control of input and output to commands. Each shell also provides built-in commands referred to as built-ins.

Shells can be used either interactively or non-interactively. An interactive shell is one in which you can provide input to the shell and the output from commands is sent back to you. On the other hand, a non-interactive shell runs a process without input from the user.

Any request sent to the shell is called a process. Whenever a request is made, the shell assigns a unique process identifier (PID) to that process. To see a list of currently running processes, use the ps command.

```
```
ps
PID TTY STAT TIME COMMAND
```

```