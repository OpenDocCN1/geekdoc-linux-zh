# Executing the Command Line

```
$ abc
bash: abc: command not found
```

When the shell finds the program but cannot execute it (you do not have access to the file that contains the program), you see a message similar to

```
$ def
bash: ./def: Permission denied.
```

If it runs an executable file with the same name as the command, the shell starts a new process. A *process* is the execution of a program (page 560). The shell makes each command line argument, including options and the name of the command, available to the called program. While the command is executing, the shell waits, inactive for the process to finish. The shell is in a state called *sleep*. When the program finishes execution, the shell returns to an active state (wakes up), issues a prompt, and waits for another command.

Because the shell does not process line arguments but only handles them to the called program, the shell has no way of knowing whether a particular option or other argument is valid for a given program. Any error or usage messages about options or arguments come from the program itself. Some utilities ignore bad options.

# Standard Input and Standard Output

The *standard output* is a place that a program can send information, such as text. The command (program) never “knows” where the information stands to standard output is going (Figure 5-3). The information can go to a printer, an ordinary file, or your screen. The following sections show that, by default, the shell directs standard output from a command to the screen^4 and describe how you can cause the shell to redirect this output to another file. Standard input is a place that a program gets information from. As with standard output, the command never “knows” where the information came from. The following sections also explain how to redirect *standard input* to a command so that it comes from an ordinary file instead of the keyboard (the default).

+   3. Refer to “Shell Specifier” on page 26 for an explanation of the symbol.
4. The term screen is used throughout to mean screen, terminal emulator window, and workstation: 
Screen* refers to the device that you see the prompt and messages displayed on.