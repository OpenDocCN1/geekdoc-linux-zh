
```
29        (void) printf("%s", prompt);
30        for (*str = getchar(); *str != '\n'; *str = 
getchar())
31            str++;
32            *str = '\0'; /* string terminator */
33    }
34
35    void null_function1 ()
36    { }
37
38    void null_function2 ()
39    { }
40
```

```
% cc bugged.c -o bugged
% bugged
Enter a string: Need gdb!
Segmentation Fault
%
```

Note that the program prompts you for input and faults without echoing what you enter from the keyboard. This happens frequently in C programming, particularly with programmers who are new to C or are not careful about initializing variables in their programs and rely on the compiler. It is time to use gdb!

## 17.7.1.2 Entering the gdb Environment

As we stated earlier, in order to enter the gdb environment, you must compile your C program with the -g compiler option. This option creates an executable file that contains the symbol table and debugging, relocation, and profiling information for your program. After the source program compiles successfully, you can then use the gdb command to debug your code, as in the following session. We ran the gdb -q command to prevent the introductory messages from being displayed. Note that (gdb) is the prompt for the gdb debugger.

```
% cc -g bugged.c -o bugged
% gdb -q bugged
(gdb)
```

Once inside the gdb environment, you can run many commands to monitor the execution of your code. You can use the help command to get information about the gdb commands. Without any argument, the help command displays the names of all of the gdb command classes. A command class specifies the type of operations you can perform on your executable code, a core file, or a process. Under a command class, you can run the commands available for that class. You can get information about any gdb command class by passing the command name as an argument to the help command. In the following session, the help command shows the names of all gdb commands and the help tracepoints command displays a brief description of the command class tracepoints and commands supported by gdb under this class.

```
(gdb) help
List of classes of commands:
aliases -- Aliases of other commands
breakpoints -- Making program stop at certain points
data -- Examining data
files -- Specifying and examining files
internals -- Maintenance commands
obscure -- Obscure features
running -- Running the program
stack -- Examining the stack
status -- Status inquiries
support -- Support facilities
tracepoints -- Tracing of program execution without stopping the program
user-defined -- User-defined commands
Type "help" followed by a class name for a list of commands in that class.
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb) help tracepoints
Tracing of program execution without stopping the program.
List of commands:
actions -- Specify the actions to be taken at a tracepoint
collect -- Specify one or more data items to be collected at a tracepoint
delete tracepoints -- Delete specified tracepoints
disable tracepoints -- Disable specified tracepoints
enable tracepoints -- Enable specified tracepoints
end -- Ends a list of commands or actions
passcount -- Set the passcount for a tracepoint
save-tracepoints -- Save current tracepoint definitions as a script
tdump -- Print everything collected at the current tracepoint
tfind -- Select a trace frame;
tfind end -- Synonym for 'none'
tfind line -- Select a trace frame by source line
tfind none -- De-select any trace frame and resume 'live' debugging
tfind outside -- Select a trace frame whose PC is outside the given range
tfind pc -- Select a trace frame by PC
tfind range -- Select a trace frame whose PC is in the given range
```

```
tfind start -- Select the first trace frame in the trace buffer
tfind tracepoint -- Select a trace frame by tracepoint number
trace -- Set a tracepoint at a specified line or function or address
tstart -- Start trace data collection
tstatus -- Display the status of the current trace data collection
tstop -- Stop trace data collection
while-stepping -- Specify single-stepping behavior at a tracepoint
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb) help trace
Set a tracepoint at a specified line or function or address.
Argument may be a line number, function name, or '*' plus an address.
For a line number or function, trace at the start of its code.
If an address is specified, trace at that exact address.
Do "help tracepoints" for info on other tracepoint commands.
(gdb)
```

In addition to the gdb-specific commands, gdb also allows you to execute all shell commands.

## 17.7.1.3 Executing a Program

You can run your program inside the gdb environment by using the run command. The following command executes the program called bugged.

```
(gdb) run
Starting program: /usr/home/sarwar/unix3e/ch17/gdb/bugged
Enter a string: Need gdb!
Program received signal SIGSEGV, Segmentation fault.
0x0000000000400951 in get_input (prompt=0x400a76 "Enter a string:", str=0x0) at bugged.c:30
30     for (*str = getchar(); *str != '\n'; *str = getchar())
Current language: auto; currently minimal
(gdb)
```

The program (now a process) prompts you for input. When you enter the input (Need gdb! in this case) and hit <Enter>, the process fails when it tries to execute the command at line 30. The error message is quite cryptic for beginners and those who are not familiar with UNIX jargon. All the error message says is that a signal of type SIGSEGV (segmentation violation, i.e., address space violation) was received by the process when it was executing the statement at line 30. The message explains that SIGSEGV was sent to the program because of Segmentation fault. A segmentation fault is generated by the UNIX kernel when a process tries to access a memory region (a segment) that it is not
