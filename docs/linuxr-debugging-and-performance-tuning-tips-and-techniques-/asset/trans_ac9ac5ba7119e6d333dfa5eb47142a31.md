
## 10.8.3 父进程监督：三种不同的策略

如第 9.1.1 节“创建过程：fork( )”第 284 页所述，调用 fork( ) 的一个副作用是在进程之间创建父子关系。父进程可以使用 wait( ) 系统调用族中的一个，等待其一个或多个子进程终止并恢复子进程的退出状态。

未被等待的已终止子进程被称为僵尸进程。通常，每当子进程终止时，内核都会向父进程发送 SIGCHLD 信号。[^6]

默认操作是忽略此信号。在这种情况下，僵尸进程会不断累积，直到父进程执行 wait( ) 或父进程自身终止为止。在后一种情况下，僵尸子进程会被重新分配给 init 系统进程（PID 1），该进程会在其正常工作过程中收割它们。类似地，活跃的子进程也会被重新分配给 init，并将在它们退出时被收割。

SIGCHLD 不仅用于通知子进程终止。每当子进程被停止（由前文讨论的作业控制信号之一触发）时，也会向父进程发送 SIGCHLD。POSIX 标准指出，当子进程恢复运行（continued）时，“可能会发送” SIGCHLD；显然，历史上的不同 Unix 系统之间存在差异。

struct sigaction 中 sa_flags 字段的标志组合，以及将 SIG_IGN 用作 SIGCHLD 的操作，允许你改变内核处理子进程停止、恢复或终止的方式。

与信号总体情况一样，这里描述的接口和机制之所以复杂，是因为它们随时间推移而演变。

### 10.8.3.1 糟糕的父职：完全忽略子进程

你能做的最简单的事情就是将 SIGCHLD 的操作更改为 SIG_IGN。在这种情况下，终止的子进程不会成为僵尸进程。相反，它们的退出状态会被丢弃，它们将被完全从系统中移除。另一种产生相同效果的选项是使用 SA_NOCLDWAIT 标志。在代码中：

```c
/* Old style: */
signal(SIGCHLD, SIG_IGN);
```

```c
/* New style: */
struct sigaction sa;
sa.sa_handler = SIG_IGN;
sa.sa_flags = SA_NOCLDWAIT;
sigemptyset(&sa.sa_mask);
sigaction(SIGCHLD, &sa, NULL);
```

### 10.8.3.2 放任的父职：最小化监督

或者，你可能只关心子进程终止，而对简单的状态变化（停止和恢复）不感兴趣。在这种情况下，使用 SA_NOCLDSTOP 标志，并设置一个信号处理器，该处理器调用 wait()（或其同族函数之一）来收割进程。

通常，你*不能*指望每个终止的子进程都收到一个 SIGCHLD。你应该将 SIGCHLD 理解为“至少有一个子进程已终止”，并在处理 SIGCHLD 时准备好尽可能收割多个子进程。

以下程序 `ch10-reap1.c` 在准备好恢复子进程之前会阻塞 SIGCHLD。

```c
1  /* ch10-reap1.c --- demonstrate SIGCHLD management, using a loop */
2
3  #include <stdio.h>
4  #include <errno.h>
5  #include <signal.h>
6  #include <string.h>
7  #include <sys/types.h>
8  #include <sys/wait.h>
9
10 #define MAX_KIDS 42
11 #define NOT_USED -1
12
13 pid_t kids[MAX_KIDS];
14 size_t nkids = 0;
```

`kids` 数组跟踪子进程的进程 ID。如果某个元素是 NOT_USED，则它不代表一个未被收割的子进程。（下面第 89–90 行对其进行初始化。）`nkids` 指示应检查 `kids` 中有多少个值。

```c
16 /* format_num --- helper function since can't use [sf]printf() */
17 const char *format_num(int num)
18 {
19     #define NUMSIZ 30
20     static char buf[NUMSIZ];
21     int i;
22
23     if (num <= 0) {
24         strcpy(buf, "0");
25         return buf;
26     }
27
28     i = NUMSIZ - 1;
29     buf[i--] = '\0';
30     /* Generate digits backwards into string. */
31     do {
32         buf[i--] = (num % 10) + '0';
33         num /= 10;
34     } while (num > 0);
35     return &buf[i+1];
36 }
```

由于信号处理器不应调用 printf() 族的任何成员，我们提供了一个简单的“辅助”函数 format_num()，用于将十进制信号或 PID 号转换为字符串。这种方法很原始，但有效。

```c
41 /* childhandler --- catch SIGCHLD, reap all available children */
42 void childhandler(int sig)
43 {
44     int status, ret;
45     int i;
46     char buf[100];
47     static const char entered[] = "Entered childhandler\n";
48     static const char exited[] = "Exited childhandler\n";
49
50     write(1, entered, strlen(entered));
51     for (i = 0; i < nkids; i++) {
52         if (kids[i] == NOT_USED)
53             continue;
54
55     retry:
56         if ((ret = waitpid(kids[i], &status, WNOHANG)) == kids[i]) {
57             strcpy(buf, "\treaped process ");
58             strcat(buf, format_num(ret));
59             strcat(buf, "\n");
60             write(1, buf, strlen(buf));
61             kids[i] = NOT_USED;
62         } else if (ret == 0) {
63             strcpy(buf, "\t.pid ");
64             strcat(buf, format_num(kids[i]));
65             strcat(buf, " not available yet\n");
66             write(1, buf, strlen(buf));
67         } else if (ret == -1 && errno == EINTR) {
68             write(1, "\tretrying\n", 10);
69             goto retry;
70         } else {
71             strcpy(buf, "\twaitpid() failed: ");
72             strcat(buf, strerror(errno));
73             strcat(buf, "\n");
74             write(1, buf, strlen(buf));
75         }
76     }
77     write(1, exited, strlen(exited));
78 }
```

第 50 行和第 77 行打印“entered”和“exited”消息，以便我们可以清楚地看到信号处理器何时被调用。其他消息以制表符（TAB）字符开头。

信号处理器的主要部分是一个大循环，位于第 51–76 行。第 52–53 行检查 `NOT_USED`，如果当前槽位未使用，则继续循环。

第 57 行对 `kids` 当前元素中的 PID 调用 `waitpid()`。我们提供 `WNOHANG` 选项，这会使 `waitpid()` 在请求的子进程不可用时立即返回。由于并非所有子进程都一定已退出，因此这个调用是必要的。

根据返回值，代码采取相应的操作。第 56–61 行处理找到子进程的情况，通过打印消息并将 `kids` 中相应的槽位标记为 `NOT_USED`。

第 62–66 行处理请求的子进程不可用的情况。在这种情况下，返回值为 0，因此我们打印消息并继续。

第 67–69 行处理系统调用被中断的情况。在这种情况下，使用 goto 返回到 waitpid() 调用是最干净的处理方式。（由于 main() 导致在信号处理器运行时阻塞所有信号 [第 99 行]，这种中断本不应发生。但此示例展示了如何处理所有情况。）

第 70–75 行处理其他任何错误，打印适当的错误消息。

```c
81 /* main --- set up child-related information and signals, create children */
82
83 int main(int argc, char *argv[])
84 {
85
86     struct sigaction sa;
87     sigset_t childset, emptyset;
88     int i;
89
90     for (i = 0; i < nkids; i++)
91         kids[i] = NOT_USED;
92
93     sigemptyset(&emptyset);
94
95     sa.sa_flags = SA_NOCLDSTOP;
96     sa.sa_handler = childhandler;
97     sigfillset(&sa.sa_mask);     /* block everything when handler runs */
98     sigaction(SIGCHLD, &sa, NULL);
99
100    sigemptyset(&childset);
101    sigaddset(&childset, SIGCHLD);
102
103    sigprocmask(SIG_SETMASK, &childset, NULL); /* block it in main code */
104
105    for (nkids = 0; nkids < 5; nkids++) {
106        if ((kids[nkids] = fork()) == 0) {
107            sleep(3);
108            _exit(0);
109        }
110    }
111
112    sleep(5);  /* give the kids a chance to terminate */
113
114    printf("waiting for signal\n");
115    sigsuspend(&emptyset);
116
117    return 0;
118 }
```

第 90–91 行初始化 `kids`。第 93 行初始化 `emptyset`。第 95–98 行设置并安装 SIGCHLD 的信号处理器。注意第 95 行使用 SA_NOCLDSTOP，而第 97 行在处理器运行时阻塞所有信号。

第 100–101 行创建一个仅表示 SIGCHLD 的信号集，第 103 行将其安装为程序的进程信号掩码。

第 105–110 行创建五个子进程，每个子进程睡眠三秒。在此过程中，它更新了 `kids` 数组和 `nkids` 变量。

然后，第 112 行通过睡眠时间比子进程长，给子进程一个终止的机会。（这并不*保证*子进程会终止，但可能性相当大。）

最后，第 114–115 行打印消息，然后暂停，将阻塞 SIGCHLD 的进程信号掩码替换为空掩码。这允许 SIGCHLD 信号通过，进而导致信号处理器运行。以下是发生的情况：

```bash
$ ch10-reap1                    Run the program
waiting for signal
Entered childhandler
    reaped process 23937
    reaped process 23938
    reaped process 23939
    reaped process 23940
    reaped process 23941
Exited childhandler
```

信号处理器一次性收割了所有子进程。

以下程序 `ch10-reap2.c` 与 `ch10-reap1.c` 类似。区别在于它允许 SIGCHLD 在任何时间到达。这种行为增加了接收多个 SIGCHLD 的可能性，但并不*保证*这一点。因此，信号处理器仍然必须准备好在循环中收割多个子进程。

```c
1  /* ch10-reap2.c -- demonstrate SIGCHLD management, one signal per child */
2
   ... unchanged code omitted ...
12
13 pid_t kids[MAX_KIDS];
14 size_t nkids = 0;
15 size_t kidsleft = 0;                     /* << Added */
16
   ... unchanged code for format_num() omitted ...
41
42 /* childhandler --- catch SIGCHLD, reap all available children */
43
```
