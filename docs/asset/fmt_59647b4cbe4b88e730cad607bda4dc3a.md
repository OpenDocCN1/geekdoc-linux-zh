
# 第7章 主从接口软件架构

## 列表 7.1 客户端：从远程文件请求一行

```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#define PORT 9876
#define NUM 50

main(int argc, char *argv[])
{
    struct timeval bef, aft;     /* 发送前后的定时器值 */
    struct sockaddr_in sock;      /* socket 结构体 */
    struct hostent *hp;          /* IP 地址结构体 */
    double random;               /* 随机数：0.0->1.0 */
    long timeleft;               /* IAT 剩余时间 */
    long secs = 0L;              /* 到达间隔秒 */
    long usec = 0L;              /* 到达间隔微秒 */
    int pids[NUM];               /* 子任务进程 ID */
    int opt = 1;                 /* setsockopt 参数 */
    int fd;                      /* socket 文件句描述符 */
    int ii, jj, kk = 0;
    char buf[80], *p;

    srand((unsigned int) getpid()); /* rand() 种子 */

    /*
    ** 操作数是远程主机名和 IAT（到达间隔）
    */
    if (argc != 3) {
        printf("\n%s <HOST> <IAT>\n", argv[0]);
        exit(-1);
    }

    /* 到达间隔的微秒 */
    if ((p = strchr(argv[2], '.')) != NULL) {
        *p = '\0'; /* 结束整数部分 */
        p++;       /* 指针移动到小数部分 */
        while (strlen(p) < 6)
            strcat(p, "0"); /* 补齐到 6 位 */
        p[6] = '\0'; /* 截断为 6 位 */
        usec = atol(p);
    }

    secs = atol(argv[2]); /* IAT 的秒部分 */

    /*
     循环：发送并接收数据包
    */
    for (ii = 0; ii < NUM; ii++) {
        /* 获取发送前时间 */
        gettimeofday(&bef, NULL);

        /* 1 到 5 之间的随机整数 */
        random = rand() / (double) RAND_MAX;
        jj = (int) ((5.0) * random) + 1;
        if (jj == 6)
            jj = 5;

        sprintf(buf, "/tmp/sample.txt %d", jj);

        if ((pids[kk++] = fork()) == 0) {
            /* 准备连接用的 socket */
            fd = socket(AF_INET, SOCK_STREAM, 0);
            memset((char *)&sock, 0, sizeof(sock));
            hp = gethostbyname(argv[1]);
            memcpy(sock.sin_addr.s_addr, hp->h_addr, hp->h_length);
            sock.sin_port = htons(PORT);
            setsockopt(fd, SOL_SOCKET, SO_REUSEADDR, (char *) &opt, sizeof(opt));

            /* 连接到服务器 */
            connect(fd, (struct sockaddr *)&sock, sizeof(sock));
            send(fd, buf, strlen(buf) + 1, 0);
            buf[0] = 0; /* 清空缓冲区 */
            recv(fd, buf, sizeof(buf), 0);

            /* 打印我们的查询输出 */
            printf("%d: %s\n", jj, buf);
            /* 检查行 */
            p = strchr(buf, ' ') + 2;
            if (p)
                printf("%s\n", p);
            close(fd);
            exit(0);
        }

        /* 休眠直到 IAT 剩余时间 */
        gettimeofday(&aft, NULL);
        aft.tv_sec -= bef.tv_sec;
        aft.tv_usec -= bef.tv_usec;
        if (aft.tv_usec < 0) {
            aft.tv_usec += 1000000L;
            aft.tv_sec -= 1;
        }

        bef.tv_sec = secs;
        bef.tv_usec = usec;
        bef.tv_sec -= aft.tv_sec;
        bef.tv_usec -= aft.tv_usec;
        if (bef.tv_usec < 0L) {
            bef.tv_usec += 1000000L;
            bef.tv_sec -= 1;
        }
        timeleft = (bef.tv_sec * 1000000L) + bef.tv_usec;
        if (timeleft < 0) {
            printf("ERROR: 需要更高的 IAT 值 - 退出。\n");
            break;
        }
        usleep(timeleft);
    }
    for (ii = 0; ii < kk; ii++)
        wait(pids[ii]);
    puts("Done.");
    return (0);
}
```

流中的数据包数量由由于初始 `socket` 连接而产生的任何时间延迟定义，但不会大至于让测试变得繁琐。为了方便，到达间隔是一个命令行参数。若要测试系统，请在你的其中一台远程机器上启动服务器，在本例中命名为 `gamma`：

> `gamma 0.025`

上述命令启动了一个客户端，向运行在 `gamma` 上的服务器进程每 25 毫秒发送一次查询。所有查询之间间隔 25 毫秒，时间间隔相等。当你扩展客户端功能时，下一章将介绍一些更真实的到达间隔分布。

## 串行服务器进程

服务器进程可以用多种方式处理传入的事务；最直接的方法是简单的接收-响应-重复循环，如列表 7.2 所示。

## 列表 7.2 串行服务器方法

```c
#include <netdb.h>
#include <stdio.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <sys/socket.h>

#define PORT 9876

main(void)
{
    /*
     ** 列表7.2.c 服务器：从文件返回一行
     */
    struct sockaddr_in sock; /* socket 结构体 */
    int socklen = sizeof(sock); /* accept 的结构长度 */
    FILE *fp; /* sample.txt 文件指针 */
    int acc; /* accept 文件句描述符 */
    int cli; /* 文件句描述符 */
    int line; /* 请求的行数 */
    int opt = 1; /* setsockopt 参数 */
    char buf[80]; /* socket 接收缓冲区 */
    char file[32]; /* 来自客户端的文件 */
    int fd; /* socket 文件描述符 */
    struct hostent *hp; /* IP 地址结构体 */

    /* 准备连接用的 socket */
    fd = socket(AF_INET, SOCK_STREAM, 0);
    memset((char *)&sock, 0, sizeof(sock));
    hp = gethostbyname(argv[1]);
    memcpy(sock.sin_addr.s_addr, hp->h_addr, hp->h_length);
    sock.sin_port = htons(PORT);
    setsockopt(fd, SOL_SOCKET, SO_REUSEADDR, (char *) &opt, sizeof(opt));

    /* 连接到服务器 */
    connect(fd, (struct sockaddr *)&sock, sizeof(sock));

    while (1) {
        cli = accept(fd, (struct sockaddr *)&sock, &socklen);
        /* 清空缓冲区 */
        recv(cli, buf, sizeof(buf), 0);
        buf[0] = 0;

        /* 打开文件 */
        fp = fopen(file, "r");
        if (fp) {
            /* 读取一行 */
            if (fgets(buf, sizeof(buf), fp)) {
                /* 打印我们的查询输出 */
                printf("%d: %s\n", line, buf);
                /* 检查行 */
                p = strchr(buf, ' ') + 2;
                if (p)
                    printf("%s\n", p);
            }
            fclose(fp);
        }
    }
}
```

## 列表 7.3 继续

```c
sock.sin_port = htons(PORT);
sock.sin_addr.s_addr = htonl(INADDR_ANY);
bind(acc, (struct sockaddr *) &sock, socklen);
setsockopt(acc, SOL_SOCKET, SO_REUSEADDR, (char *) &opt, sizeof(opt));
listen(acc, 5);
```

```c
while (1) {
    /* 等待远程客户端的连接 */
    cli = accept(acc, (struct sockaddr *) &sock, &socklen);

    /* 获取客户端请求的随机行数据 */
    if (fork() == 0) {
        recv(cli, buf, sizeof(buf), 0);

        /* 打开请求的文件 */
        sscanf(buf, "%s %d", file, &line);
        fp = fopen(file, "r");
        while (line--)
            fgets(buf, sizeof(buf), fp);
        fclose(fp);

        buf[strlen(buf) - 1] = '\0';
        send(cli, buf, strlen(buf) + 1, 0);
        close(cli);
        exit(0);
    }
    close(cli);
}
```

为每个传入的数据包创建一个子任务的好处是利用数据处理中的任何并行性。在这种情况下，共享资源是只读的；许多子任务可以同时读取文本，通过减少响应时间来提高性能。然而，为每个传入的数据包创建单独子任务是有成本的。你可以通过提前创建足够的子任务来处理预期的峰负载（最短到达时间），从而减少这种开销，代价是增加一些进程间通信开销来管理并行查询处理，如列表 7.4 所示。

## 列表 7.4 服务器提前创建子任务池以处理传入的查询流

```c
#include <netdb.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/time.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <sys/socket.h>
#include <sys/signal.h>

#define PORT 9876
#define FALSE 0
#define TRUE 1
#define MAX 5

int Running = TRUE; /* 布尔值：在 control_C() 中重置 */

main(void)
{
    /*
     ** Listing7.4.c - 并发服务器：子任务池
     */
    struct area {
        int flag[MAX];      /* 每个子任务的标志 */
                            /* 0:空闲, 1:可用, ::退出 */
    } area, *aptr;
    int flag = IPC_CREATE | IPC_EXCL | 0660;
    int size = sizeof(struct area);
    key_t key = 0x5a5a5a5a; /* 共享内存区域 ID */
    int shmid;

    void control_C(); /* ctrl-C 信号处理器 */
    struct sockaddr_in sock; /* socket() 的结构 */
    int socklen = sizeof(sock); /* accept() 的结构长度 */
    FILE *fp;                 /* 查询文本文件指针 */
    fd_set fds;               /* select 等待客户端 */
    int acc;                  /* accept 文件描述符 */
    int cli;                  /* 客户端文件描述符 */
    int line;                 /* 请求的行号 */
    int opt = 1;              /* setsockopt 参数 */
    int ident;                /* 子任务 ID */
    int pids[MAX];            /* 子任务进程 ID */
    char file[32];            /* 来自客户端的文本文件 */
    char buf[100];            /* socket 接收缓冲区 */

    /* 初始化 "C 处理器 */
    signal(SIGINT, control_C);

    /* 创建（服务器）socket 以接收客户端 */
    acc = socket(AF_INET, SOCK_STREAM, 0);

    /* 将 socket 绑定到端口 */
    sock.sin_family = AF_INET;
    sock.sin_port = htons(PORT);
    sock.sin_addr.s_addr = htonl(INADDR_ANY);
    bind(acc, (struct sockaddr *) &sock, socklen);
    setsockopt(acc, SOL_SOCKET, SO_REUSEADDR, (char *) &opt, sizeof(opt));
    listen(acc, 5);

    /* 获取共享内存区域 */
    shmid = shmget(key, size, flag);
    /* 挂载子任务的共享内存数组 */
    aptr = (struct area *) shmat(shmid, 0, 0);

    /* 预建立子任务池 */
    for (ident = 0; ident < MAX; ident++) {
        aptr->flag[ident] = 0; /* 设置标志为空闲 */

        if ((pids[ident] = fork()) == 0) { /* 子任务 */
            /* 挂载父进程的共享内存数组 */
            aptr = (struct area *) shmat(shmid, 0, 0);
            /* 注意：shmid 仍然设置正确 */

            /* 取消 "C 处理器 */
            signal(SIGINT, SIG_DFL);

            /*
            ** 轮询内存数组查找非零标志
            */
        }
    }
}
```
