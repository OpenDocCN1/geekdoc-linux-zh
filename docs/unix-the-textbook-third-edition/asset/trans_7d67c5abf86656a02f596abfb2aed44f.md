

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

请注意，该程序会提示你输入，并在未回显键盘输入内容的情况下出现故障。在 C 编程中这种情况很常见，尤其是在刚接触 C 的程序员或不注意在程序中初始化变量并依赖编译器的程序员身上。是时候使用 gdb 了！

## 17.7.1.2 进入 gdb 环境

正如我们前面所说，为了进入 gdb 环境，你必须使用 -g 编译器选项编译你的 C 程序。该选项会创建一个包含符号表以及程序的调试、重定位和剖析信息的可执行文件。源程序成功编译后，你就可以使用 gdb 命令来调试代码，如以下会话所示。我们运行了 gdb -q 命令以防止显示介绍性信息。请注意，(gdb) 是 gdb 调试器的提示符。

```
% cc -g bugged.c -o bugged
% gdb -q bugged
(gdb)
```

进入 gdb 环境后，你可以运行许多命令来监控代码的执行。你可以使用 help 命令获取有关 gdb 命令的信息。如果不带任何参数，help 命令会显示所有 gdb 命令类的名称。命令类指定了你可以在可执行代码、核心文件或进程上执行的操作类型。在一个命令类下，你可以运行该类可用的命令。你可以通过将命令名作为参数传递给 help 命令来获取有关任何 gdb 命令类的信息。在以下会话中，help 命令显示了所有 gdb 命令的名称，而 help tracepoints 命令显示了命令类 tracepoints 的简要描述以及 gdb 在该类下支持的命令。

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

除了 gdb 特定命令外，gdb 还允许你执行所有 shell 命令。

## 17.7.1.3 执行程序

你可以使用 run 命令在 gdb 环境中运行程序。以下命令执行名为 bugged 的程序。

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

程序（现在是一个进程）会提示你输入。当你输入输入内容（本例中为 Need gdb!）并按下 <Enter> 后，进程在尝试执行第 30 行的命令时失败。对初学者和不熟悉 UNIX 术语的人来说，该错误信息相当晦涩。错误信息只说明了在执行第 30 行语句时，进程收到了类型为 SIGSEGV（段错误，即地址空间违规）的信号。信息解释说，由于 Segmentation fault，SIGSEGV 被发送给了程序。段错误是由 UNIX 内核在进程尝试访问其未被授权的内存区域（段）时产生的

