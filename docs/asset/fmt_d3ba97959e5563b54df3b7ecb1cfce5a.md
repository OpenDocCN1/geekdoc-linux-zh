
```
1:   #include <sys/types.h>
2:   #include <sys/wait.h>
3:   #include <unistd.h>
4:   #include <stdio.h>
5:   #include <stdlib.h>
6:   #include <string.h>
7: 
8:   #define MAX_LINE      80
9:   
10:  int main()
11:  {
12:      int status;
13:      pid_t childpid;
14:   char cmd[MAX_LINE+1];
15:   char *sret;
16:
17:   while (1) {
18: 
19:     printf("mysh");
20: 
21:     sret = fgets(cmd, sizeof(cmd), stdin);
22: 
23:     if (sret == NULL) exit(-1);
24: 
25:     cmd[strlen(cmd)-1] = 0;
26: 
27:     if (!strncmp(cmd, "bye", 3)) exit(0);
28: 
29:     childpid = fork();
30: 
31:     if (childpid == 0) {
32: 
33:       execcl(cmd, cmd, NULL);
34: 
35:     } else if (childpid > 0) {
36: 
37:       waitpid(childpid, &status, 0);
38: 
39:     }
40: 
41:     printf("\n");
42: 
43:     }
44: 
45:   return 0;
46: }
```

该解释器是围绕简单的父/子应用程序构建的。父进程在第 29 行 `fork()` 出子进程，然后等待其完成。子进程获取从用户处读取的命令（第 21 行）并使用 `execcl()`（第 33 行）执行它。你只需将命令指定为要执行的命令，并将其包含在 `arg0`（第二个参数）中。`NULL` 终止参数列表；在这种情况下，没有为命令传递参数。子进程永远不会返回，但其退出状态会在父进程的 `waitpid()` 函数（第 37 行）中被识别。

## 240 GNU/Linux 编程

当用户输入命令时，这些命令通过 `execvp()` 执行。输入命令会导致应用程序退出。

由于没有向命令（通过 `execvp()`）传递任何参数，因此用户只能输入命令而不能带参数。用户提供的任何参数都会被解释器忽略。

此处显示了该应用程序的示例执行：

```
$ ./simpshell
mush>date
Sat Apr 24 13:47:48 MDT 2004
mush>ls
simpshell      simpshell.c
mush>bye
$
```

你可以看到，在执行 shell 后会显示提示符，表示可以输入命令。首先输入 `date` 命令，它提供了当前的日期和时间。接下来，你执行 `ls`，它给出了当前目录的内容。最后，你使用 `bye` 内部命令使用 shell。

现在来看一种 `exec` 变体，将其作为探索和管理进程环境方面的方法。`execve` 变体允许应用程序为新进程提供一组命令行参数（以向量的形式）以及新进程的环境（以环境变量向量的形式）。现在回头来看 `execve` 的原型：

```
int execve(const char filename, const char argv[],
             const char envp[]);
```

`filename` 参数是要执行的程序，它必须是一个二进制可执行文件，或在文件顶部包含 `#` 解释器说明的脚本。`argv` 参数是命令的参数数组，第一个参数是命令本身（与 `filename` 参数相同）。最后，`envp` 参数是一个包含环境变量的键值对字符串数组。考虑以下简单的函数，它通过光盘 `./source/ch14/sigenv.c` 获取环境变量：

```
#include <stdio.h>
#include <unistd.h>
int main(int argc
{
    ret = execve("/bin/ls", args, envp);
    fprintf(stderr, "execve failed\n");
    return 0;
}
```

此示例中第一个需要注意的项目是 `main()` 函数定义。你使用了一个传递第三个参数的变体，该参数列出了进程的环境。程序也可以通过特殊的 `environ` 变量获取环境，其定义如下：

```
extern char *environ[];
```

## 242 GNU/Linux 编程

这是一个使用 alarm 的示例，如果用户在合理时间内输入密码，则杀死当前进程（参见列表 14.7）。在第 18 行，你为 `SIGALRM` 信号安装了信号处理器。信号处理器是 `wakeup()` 函数（6-9 行），它简单地引发了 `SIGKILL` 信号。这会终止应用程序。你随后发出在三秒内输入密码的消息，并尝试从键盘（`stdin`）读取密码。如果读取成功，你禁用闹钟（通过调用参数为零的 `alarm()`）。测试部分（第 30 行）检查密码并继续。如果闹钟超时，将产生 `SIGALRM`，导致 `SIGKILL` 信号，从而终止程序。

列表 14.7 alarm 与信号捕获示例（位于光盘的 `/source/ch14/alarm.c`）

```
1: #include <stdio.h>
2: #include <unistd.h>
3: #include <signal.h>
4: #include <string.h>
5: 
6: void wakeup(int sig_num)
7: {
8: raise(SIGKILL);
9: }
10: 
11: #define MAX_BUFFER 80
12: 
13: int main()
14: {
15:     char buffer[MAX_BUFFER+1];
16:     int ret;
17: 
18: signal(SIGALRM, wakeup);
19: 
20:     printf("You have 3 seconds to enter the password\n");
21: 
22: alarm(3);
23: 
24:     ret = read(0, buffer, MAX_BUFFER );
25: 
26:     alarm(0);
27: 
28:     if (ret == -1) {
29:         printf("Error reading input\n");
30: } else {
31:     printf("Password entered: %s\n", buffer);
32: }
33: 
34:     return 0;
35: }
```

# 第 14 章 GNU/Linux 进程模型

## exit

`exit()` API 函数会终止调用进程。传递给 `exit()` 的参数将作为父进程 `wait()` 或 `waitpid()` 调用产生的状态返回给父进程。`exit()` 的函数原型如下：

```
void exit(int status );
```

调用 `exit()` 的进程还会向父进程发送一个 `SIGCHILD` 信号，并释放该进程分配的资源（例如已打开的文件描述符）。如果进程注册了 `exit` 或 `on_exit` 函数，这些函数将会被调用（按照它们注册的相反顺序）。

此调用非常重要，因为它向 shell 环境指示了成功或失败。如果应用程序没有提供适当的状态，依赖于该程序退出状态的脚本可能会表现不当。该调用提供了与脚本环境的连接。向脚本返回 0 表示 `TRUE`（真）或 `SUCCESS`（成功）。

## POSIX 信号

在结束对进程相关函数的讨论后，你需要快速查看一下 POSIX 信号 API。符合 POSIX 标准的信号最早在 BSD 中引入，并通过使用 `sigaction()` 函数提供了一个可移植的 API。来看一个使用 `sigaction()` 函数安装信号处理程序的多进程应用程序。`sigaction()` API 函数的原型如下：

```
#include <signal.h>
int sigaction(int signum,
    const struct sigaction *act,
    struct sigaction *oldact);
```

`signum` 是你正在安装处理器的信号，`act` 指定了针对 `signum` 要采取的操作，而 `oldact` 用于存储之前的操作。`sigaction` 结构包含多个可以配置的元素：
