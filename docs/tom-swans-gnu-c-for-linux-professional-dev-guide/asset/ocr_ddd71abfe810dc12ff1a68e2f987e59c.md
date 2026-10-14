commands, type them as you do when running gdb in console mode. The advantage of using Emacs is that it shows you the program's source code and also highlights the current line and any breakpoints. Also, you can write, compile, and debug programs without switching away from Emacs.

If you are following along, repeat the steps in “Using the gdb Console Debugger” to see how Emacs displays the results of various commands. Another advantage of running gdb in Emacs is that the debugger's output is saved in a buffer (in this case, named gud-welcome). Use the buffer to scroll back through commands and their output. You might even save or print the entire debugging session. When tracking a difficult bug, it's helpful to have a record of debugging commands issued.

# Useful Debugger Options

Use -h (or -help) to list available options you can specify when starting gdb. Following are explanations of some of the options that you might find useful.

Specify --command=FILE where FILE is the name of a text file containing gdb commands. This is a great way to repeat debugging sessions without typing the same commands over and over. For example, create a text file named commands containing the following two lines:

```
break 15
run
```

To debug the welcome.cpp program and execute the file's commands, type the following at the console prompt (this assumes that you compiled welcome.cpp using the -g option). This command loads welcome and then executes the break and run commands in the commands file:

```
$ gdb --command=commands welcome
```

If you store your program's source code in a directory that is different from where you store the executable code, use the --directory option to tell gdb where to find the source code files. Use a command such as

```
gdb --directory=/home/you/source yourprogram
```

You might need to do that when using Emacs to run gdb if the current directory does not contain the compiled program. To send the program's output to a terminal that is different from the one you are using to view gdb's messages, use the --tty command as follows:

```
gdb --tty=/dev/tty0 welcome
```

This works the same in the console, X, and Emacs debugger interfaces. To find the device name of a terminal, type the following tty command at a shell prompt:

```
$ tty
/dev/tty0
```

Switch to another terminal—or under X, open a new shell window—and then specify the reported device name to gdb using the --tty option. The program's output appears on the other console window. This is particularly useful when debugging programs that display