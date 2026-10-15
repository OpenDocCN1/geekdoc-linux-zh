
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

除了 `gdb` 特定命令外，`gdb` 还允许你执行所有 `shell` 命令。

## 17.7.1.3 执行程序

你可以使用 `run` 命令在 `gdb` 环境中运行程序。以下命令执行名为 `bugged` 的程序。

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

程序（现在是一个进程）会提示你输入。当你输入输入内容（本例中为 Need gdb!）并按下 `<Enter>` 后，进程在尝试执行第 30 行的命令时失败。对初学者和不熟悉 UNIX 术语的人来说，该错误信息相当晦涩。错误信息只说明了在执行第 30 行语句时，进程收到了类型为 `SIGSEGV`（段错误，即地址空间违规）的信号。信息解释说，由于 Segmentation fault，`SIGSEGV` 被发送给了程序。段错误是由 UNIX 内核在进程尝试访问其未被授权的内存区域（段）时产生的

允许访问。换句话说，你的进程尝试访问一个不属于其地址空间的内存位置。

## 17.7.1.4 列出程序代码

你可以使用 `list` 命令来显示源程序的全部或部分内容。默认情况下，它会显示你作为参数指定的行（或函数）周围的 10 行。你可以显示特定函数中的代码行或某一范围的行。在下面的示例中，`list get_input` 命令用于显示 `get_input` 函数周围代码的 10 行，而 `list 14,27` 命令用于显示 14–27 行的源程序。请注意，`list get_input` 命令会显示函数代码开始前的五行和之后的五行。为了显示该函数代码的前 10 行，我们使用 `list get_function,` 命令。由于 `get_function` 的代码少于 10 行，因此也会额外显示函数之后的几行。使用 `help list` 命令可获取有关 `list` 命令的更多信息。

```
(gdb) list get_input
23     (void) printf("The end of buggy code!\n");
24     return (0);
25 }
26
27 void get_input(char *prompt, char *str)
28 {
29     (void) printf("%s", prompt);
30     for (*str = getchar(); *str != '\n'; *str = getchar())
31         str++;
32     *str = '\0'; /* string terminator */
(gdb) list get_input,
28 {
29     (void) printf("%s", prompt);
30     for (*str = getchar(); *str != '\n'; *str = getchar())
31         str++;
32     *str = '\0'; /* string terminator */
33 }
34
35 void null_function1 ()
36 { }
(gdb) list 14,27
14 int main ()
15 {
16     char *s_val, *temp;
17
18     temp = s_val;
19     null_function1 ();
20     null_function2 ();
```

```
21      get_input(PROMPT, temp);
22      (void) printf("You entered: %s.\n", s_val);
23      (void) printf("The end of buggy code!\n");
24      return (0);
25  }
26
27  void get_input(char *prompt, char *str)
(gdb)
```

## 17.7.1.5 跟踪程序执行

要找出我们的进程出了什么问题，我们需要确定代码中可能有问题的部分。有几种方法可以做到这一点，包括逐行跟踪整个程序、跟踪函数的语句、对特定函数的调用以及对变量的更改。我们通过使用 `gdb` 的 `where` 或 `backtrace` 命令回溯程序，如以下会话所示。两个命令的输出相同：程序发生故障的位置以及如何到达该位置。如何到达的部分由命令显示的函数调用序列标识，该序列在编程语言术语中也称为堆栈跟踪（也称为堆栈帧或激活记录）。第 `#0` 行显示堆栈顶部，显示发生崩溃的 `get_input()` 函数的语句，而 `#1` 行显示 `get_input()` 函数是在 `main()` 函数的第 21 行被调用的。`main()` 函数被称为调用者，而 `get_input()` 函数被称为被调用者。

```
(gdb) where
#0 0x0000000000400951 in get_input (prompt=0x400a76 "Enter a
    string: ", str=0x0) at bugged.c:30
#1 0x0000000000400862 in main () at bugged.c:21
(gdb) backtrace
#0 0x0000000000400951 in get_input (prompt=0x400a76 "Enter a
    string: ", str=0x0) at bugged.c:30
#1 0x0000000000400862 in main () at bugged.c:21
(gdb)
```

命令的输出显示，程序在 `get_input()` 函数的第 30 行的内存地址 `0x0000000000400951` 处收到 `SIGSEGV` 信号时正在运行。堆栈帧显示调用序列为 `main()` => `get_input()`，并且程序在崩溃时正在执行第 30 行的 `*str = getchar()` 语句（参见上一节中的程序列表）。请注意，该行代码包含两个赋值语句和一个比较语句。在所有这些语句中，我们都解引用了字符串指针 `str`。两个语句使用了 C 库函数 `getchar()`。该库函数经过充分测试，已使用了多年。因此，问题一定出在指针变量 `str` 上。我们将在后面的章节中继续研究这个问题。

## 17.7.1.6 设置断点
