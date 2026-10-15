

## 7.3 命令行

登录后，shell 会显示其主提示符，默认是一个美元符号。shell 是你的命令解释器。当 shell 以交互方式运行时，它从终端读取命令并将命令行拆分为单词。命令行由一个或多个单词（标记）组成，单词之间用空白（空格和/或制表符）分隔，并以换行符终止，该换行符是通过按 Enter 生成的。第一个单词是命令，后续单词是命令的参数。命令可能是 UNIX 可执行程序，如 ls 或 pwd，也可能是内置命令，如 cd 或 test，或 shell 脚本。命令可能包含特殊字符，称为元字符，shell 在解析命令行时必须解释这些字符。如果命令行很长并且你想在下一行继续输入，反斜杠字符后跟换行符将允许你在下一行继续输入。直到命令行终止，次要提示符将会出现。

### 7.3.1 退出状态

命令或程序终止后，它会向父进程返回一个退出状态。退出状态是一个介于 0 和 255 之间的数字。根据惯例，程序退出时，如果返回的状态为 0，则表示命令执行成功。当退出状态为非零时，表示命令以某种方式失败。shell 状态变量 `?` 被设置为最后执行的命令的退出状态值。程序的成功或失败由编写该程序的程序员决定。

### EXAMPLE 7.8

```
1 $ grep "john" /etc/passwd
john:MgYbS2Javd16s:9496:40:John Doe:/home/falcon/john:/bin/sh
2 $ echo $?
0
3 $ grep "nicky" /etc/passwd
4 $ echo $?
1
5 $ grep "scott" /etc/passsswd
grep: /etc/passsswd: No such file or directory
6 $ echo $?
2
```

### EXPLANATION

- 1. grep 程序在 /etc/passwd 文件中搜索模式 john 并成功。/etc/passwd 中的行被显示。
- 2. `?` 变量被设置为 grep 命令的退出值。零表示成功。
- 3. grep 程序在 /etc/passwd 文件中找不到用户 nicky。

### EXPLANATION (CONTINUED)

- 4 If the grep program cannot find the pattern, it returns an exit status of 1.
- 5 The grep program fails because the /etc/passwd file cannot be opened.
- 6 If grep cannot find the file, it returns an exit status of 2.

### 7.3.2 命令行中的多个命令

命令行可以由多个命令组成。每个命令由分号分隔，命令行以换行符终止。

### EXAMPLE 7.9

```
$ ls; pwd; date
```

### EXPLANATION

命令从左到右依次执行，直到遇到换行符。

### Grouping Commands.

命令也可以被分组，以便所有输出都通过管道传递给另一个命令或重定向到文件。

### EXAMPLE 7.10

```
$ ( ls ; pwd; date ) > outfile
```

### EXPLANATION

每个命令的输出都被发送到名为 outfile 的文件。括号内的空格是必要的。

### 7.3.3 命令的条件执行

在条件执行中，两个命令字符串由特殊元字符双与号（&&）和双竖线（||）分隔。位于任一元字符右侧的命令是否执行取决于左侧命令的退出条件。

### EXAMPLE 7.11

```
$ cc prgn1.c -o prgn1 && prgn1
```

### EXPLANATION

如果第一个命令成功（退出状态为 0），则 && 后的命令将被执行；也就是说，如果 cc 程序能够成功编译 prgn1.c，则生成的可执行程序 prgn1 将被执行。

### EXAMPLE 7.12

```
$ cc prog.c 2> err || mail bob < err
```

### EXPLANATION

如果第一个命令失败（退出状态为非零），则 || 后的命令将被执行；也就是说，如果 cc 程序无法编译 prog.c，错误将被发送到名为 err 的文件，并且用户 bob 将收到 err 文件的邮件。

### 7.3.4 后台命令

通常，当你执行命令时，它在前台运行，并且在命令执行完成之前提示符不会重新出现。有时等待命令完成并不方便。通过在命令行末尾放置一个与号（&），shell 将立即返回 shell 提示符并在后台并发执行命令。你不必等待即可启动另一个命令。后台作业的输出将在处理时发送到屏幕。因此，如果你打算在后台运行命令，该命令的输出可能需要重定向到文件或通过管道传输到另一个设备，例如打印机，以便输出不会干扰你正在进行的工作。

变量 `$!` 包含最近放入后台的作业的 PID 号。

### EXAMPLE 7.13

- 1 $ man sh | lp&
- 2 [1] 1557
- 3 $ kill -9 $!

### EXPLANATION

- 1 man 命令的输出（sh 命令的手册页）被通过管道传输到打印机。命令行末尾的与号将作业置于后台。
- 2 屏幕上出现了两个数字：方括号中的数字表示这是被置于后台的第一个作业；第二个数字是该作业的 PID，即进程识别号。
- 3 shell 提示符立即出现。在你的程序在后台运行时，shell 正在等待前台的另一个命令。`!` 变量求值为最近放入后台的作业的 PID。如果你及时操作，你将在它进入打印队列之前杀死此作业。

