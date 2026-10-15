
```
if (argc < 2 || strcmp(argv[1], "--help") == 0)

    usageErr("%s sleep-time...\n", argv[0]);

setbuf(stdout, NULL);                    /* 使标准输出不缓冲，因为

                             我们使用 _exit() 终止子进程 */

printf("%s Parent started\n", currTime("%S"));

if (pipe(pfd) == -1)

    errExit("pipe");

for (j = 1; j < argc; j++) {

    switch (fork()) {

        case -1:

            errExit("fork %d", j);

        case 0: /* 子进程 */

            if (close(pfd[0]) == -1)    /* 读端未使用 */

                errExit("close");

            /* 子进程执行工作，并通知父进程它已完成 */

            sleep(getint(argv[j], JN_NONMEM, "sleep-time"));    /* 模拟处理 */

            printf("%s Child %d (PID=%ld) closing pipe\n",

                currTime("%S"), j, (long)getpid());

            if (close(pfd[1]) == -1)

                errExit("close");

            /* 子进程执行工作，并通知父进程它已完成 */

            // (逻辑继续)
```

## 44.4 使用管道连接过滤器

使用管道进行同步相比早前的信号示例有一个优势：它可以解决信号广播在这种情况下不合适的问题。当创建一个管道时，用于管道两端的文件描述符是下一个可用的。由于在正常情况下描述符 0、1 和 2 已被占用，将为管道分配编号较大的描述符。那么，我们如何实现图 44-1 所示的情况，即两个过滤器（即从 `stdin` 读取并写入 `stdout` 的程序）通过管道连接，使得一个程序的标准输出重定向到管道，而另一个程序的标准输入从管道获取？答案是使用5.5节描述的复制描述符的技术。传统上，使用以下系列调用来实现结果：

```
int pfd[2];

pipe(pfd);               /* 为管道分配（例如）描述符 3 和 4 */
/* 其他步骤，例如 fork() **/

close(STDOUT_FILENO);      /* 释放描述符 1 */
dup(pfd[1]);               /* 使用最低空描述符，即 fd 1 */
```

上述步骤的结果是进程的标准输出绑定到了管道的写端。相应的调用可以用于将进程的标准输入绑定到管道的读端。

注意，这些步骤依赖于一个假设，即进程的文件符 0、1 和 2 已经是打开的（shell 在执行每个程序时通常会这样做）。如果在执行上述步骤之前描述符 0 已经关闭，那么我们将错误地将进程的标准输入绑定到管道的写端。为了避免这种可能性，我们可以将 `close()` 和 `dup()` 调用替换为下面的 `dup2()`，它允许显式指定绑定到管道的描述符：

```
dup2(pfd[1], STDOUT_FILENO);   /* 关闭描述符 1，并重新打开绑定的管道写端 */
```

在复制`pfd[1]`后，我们现在有了两个指向管道写端的文件描述符：描述符 1 和`pfd[1]`。由于未使用的管道文件描述符应该被关闭，在调用`dup2(1)`之后，关闭多余的描述符：

```
close(pfd[1]);
```

我们目前展示的代码依赖于标准输出之前已经打开。假设在调用 `pipe()` 之前，标准输入和标准输出都已关闭。在这种情况下，`pipe()` 将将这两个描述符分配给管道，可能`pfd[0]`的值为 0，而`pfd[1]`的值为 1。按顺序执行，`dup2(1)` 和 `close()` 调用将等同于以下操作：

```
dup2(1, 1);      /* 什么都不做 */
close(1);               /* 关闭管道写端的文件描述符 */
```

因此，一种良好的防御性编程习惯是使用以下语句包裹这些调用：

```
if (pfd[1] != STDOUT_FILENO) {
dup2(pfd[1], STDOUT_FILENO);
close(pfd[1]);
}
```

## 示例程序

列表 44-4 中的程序使用了本节描述的技术来实现图 44-1 所示的设置。构建管道后，该程序创建了两个子进程。第一个子进程将其标准输出绑定到管道的写端，然后执行 `wc`。第二个子进程将其标准输入绑定到管道的读端，然后执行 `wc`。

## 列表 44-4：使用管道连接 `ls` 和 `wc`

```
#include <sys/wait.h>
#include <unistd.h>

int
main(int argc, char *argv[]) {
    int pfd[2];                /* 管道文件描述符 */

    if (pipe(pfd) == -1)       /* 创建管道 */
        errExit("pipe");

    switch (fork()) {
        case -1:
            errExit("fork");

        case 0:                   /* 第子进程：执行 'ls' 写入管道 */
            if (close(pfd[0]) == -1) /* 读端未使用 */
                errExit("close 1");

/*
/* 在管道写端复制 stdout；关闭复制的描述符 */
if (pfd[1] != STDOUT_FILENO) { /* 防御性检查 */
    if (dup2(pfd[1], STDOUT_FILENO) == -1)
        errExit("dup2 2");
    if (close(pfd[1]) == -1)
        errExit("close 2");
}

execl("ls", "ls", (char *) NULL); /* 写入管道 */
errExit("execl ls");

default:
    break; /* 父进程继续创建下一个子进程 */
}

switch (fork()) {
    case -1:
        errExit("fork");
    case 0: /* 第二子进程：执行 'wc' 从管道读取 */
        if (close(pfd[1]) == -1) /* 写端未使用 */
            errExit("close 3");

/* 在管道读端复制 stdin；关闭复制的描述符 */
if (pfd[0] != STDIN_FILENO) { /* 防御性检查 */
    if (dup2(pfd[0], STDIN_FILENO) == -1)
        errExit("dup2 2");
    if (close(pfd[0]) == -1)
        errExit("close 4");
}

execl("wc", "wc", "-1", (char *) NULL); /* 从管道读取 */
errExit("execl wc");

default:
    break; /* 父进程继续 */
}

/* 父进程关闭管道未使用的文件描述符，并等待子进程 */
if (close(pfd[0]) == -1)
    errExit("close 5");
if (close(pfd[1]) == -1)
    errExit("close 6");
if (wait(NULL) == -1)
    errExit("wait 1");
if (wait(NULL) == -1)
    errExit("wait 2");

exit(EXIT_SUCCESS);
```

`pipes/pipe_ls_wc.c`

当我们运行列表 44-4 中的程序时，我们看到以下内容：

```
$ ./pipe_ls_wc
24
$ ls | wc -1
24
```
