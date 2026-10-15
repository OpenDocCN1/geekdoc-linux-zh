
Purpose: Overwrite the code for command on top of the process that executes the exec command (the calling process), which makes command run in place of the calling process without creating a new process

运行此命令后，控制无法返回到调用进程。当 `exec` 命令完成后，控制返回到调用进程的父进程。如果调用进程是你的登录 shell，控制将返回到 `getty` 进程，该进程在 `exec` 命令执行完毕后显示 Login: 提示符，如下所示：

```
% exec date

Thu Jul 31 17:57:39 PKT 2014

Login:
```

当 `exec date` 完成后，控制不会返回到 shell 进程，而是返回到 `getty` 进程——即登录 shell 进程的父进程。此命令执行的语义如图 13.1 所示。

如果命令在登录 shell 的子 shell 下运行，控制将返回到登录 shell，如以下会话所述。这里，C shell 作为登录 shell 的子进程运行，此处登录 shell 也是 C shell，并在子 C shell 下运行 `exec date`。当 `exec date` 命令执行完毕后，控制返回到登录 C shell。图 13.2 中从左到右的三个图表描绘了这些步骤的语义。

```
% ps

PID TT STAT TIME COMMAND

29301 4 Ss 0:00.05 -csh (csh)

41055 4 R+ 0:00.00 ps

% /bin/csh

% ps

PID TT STAT TIME COMMAND

29301 4 Ss 0:00.06 -csh (csh)

41084 4 S 0:00.00 /bin/csh

41097 4 R+ 0:00.01 ps

% exec date

Thu Jul 31 18:16:01 PKT 2014

% ps

PID TT STAT TIME COMMAND

29301 4 Ss 0:00.06 -csh (csh)

41133 4 R+ 0:00.01 ps

%
```

![](img/02e070097d401d3bf7de4bf1c470b267_550_0.png)

FIGURE 13.1 Execution of the exec date command under the login shell.

![](img/02e070097d401d3bf7de4bf1c470b267_551_0.png)

## 图 13.2 在登录 shell 的子 shell 下执行 exec date 命令。

## 13.5.2 通过 exec 命令进行文件 I/O

不同的 shell 允许同时使用不同数量的文件描述符。如第 7 章所述，其中三个描述符被保留用于标准输入（0）、标准输出（1）和标准错误（2）。使用重定向运算符与 `exec` 命令可以对所有这些描述符进行 I/O。表 13.2 描述了 `exec` 命令用于文件 I/O 的语法。

当从命令行执行时，`exec < sample` 命令会使 `sample` 文件中的每一行都被视为一条命令并由当前 shell 执行。这是因为 shell 进程，其唯一目的是从 stdin 读取命令并执行它们，执行了 `exec` 命令；由于 `sample` 文件被连接到 stdin，shell 从该文件读取其命令。shell 在执行完最后

## 表 13.2 exec 命令用于文件 I/O 的语法

| Syntax | Meaning |
|---|---|
| exec < file | Opens file for reading and attaches standard input of the process to file |
| exec > file | Opens file for writing and attaches standard output of the process to file |
| exec >> file | Opens file for writing, attaches standard output of the process to file, and appends standard output to file |
| exec n< file | Opens file for reading and assigns it the file descriptor n |
| exec n> file | Opens file for writing and assigns it the file descriptor n |
| exec n<< tag ... tag | Opens a here document (data between << tag and tag) for reading; the opened file is assigned a descriptor n |
| exec n>> file | Opens file for writing, assigns it file descriptor n, and appends data to the end of file |
| exec n>&m | Duplicates m into n; whatever goes into file with file descriptor n will also go into file with file descriptor m |
| exec <&- | Closes standard input |
| exec >&- | Closes standard output |
| exec n<&- | Closes file with descriptor n attached to stdin |
| exec n>&- | Closes file with descriptor n attached to stdout |

行后终止。当从 shell 脚本内部执行时，此命令会导致脚本其余部分的 stdin 被连接到 `sample`。以下会话说明了当该命令在命令行执行时此命令的语义。如图所示，`sample` 文件包含两个命令：`date` 和 `echo`。Bourne shell 通过 `/bin/sh` 命令在登录 shell 下运行，而登录 shell 是 C shell。当执行 `exec < sample` 命令时，`sample` 文件中的命令会被执行，Bourne shell（登录 C shell 的子进程）在完成 `sample` 中最后一个命令的执行后终止（第三次 `ps` 命令的输出显示在 `exec < sample` 命令执行完成后只有登录 shell 在运行），并且控制权返回到登录 shell。

```
% cat sample

date

echo "Hello, world!"

% ps

PID TT STAT TIME COMMAND

41407 1 Ss 0:00.72 -csh (csh)

43286 1 R+ 0:00.02 ps

% /bin/sh

% ps

PID TT STAT TIME COMMAND

41407 1 Is 0:00.15 -csh (csh)

41802 1 S 0:00.04 /bin/sh

41901 1 R+ 0:00.02 ps

% exec < sample

Thu Jul 31 18:41:38 PKT 2014

Hello, world!

% ps

PID TT STAT TIME COMMAND

41407 1 Ss 0:00.50 -csh (csh)

41914 1 R+ 0:00.00 ps
```
