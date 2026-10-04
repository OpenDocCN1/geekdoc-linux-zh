
/* Open specified file */
if ((fd = open(name, O_RDONLY))==-1)
    fatal(strcat(name, " open()"));

/* Transfer contents to client */
while ((i = read(fd, &c, 1))!=0)
    if (i==-1)
        fatal("file read()");
    else if (write(sd, &c, 1)!=1)
        fatal("write()");

/* Terminate child and with it the connection to this client */
exit(0);
}

即使它能工作，但目前服务器的编码方式还不够健壮，无法投入实际使用。我们将在研究完守护进程之后，再回到这段代码。

## 18.3 示例客户端

下面给出的 C 代码是前面介绍的服务器的对应客户端。假设客户端名为 getfile，则应按如下方式调用：

```
getfile host remote_file local_file
```

其中 host 是运行服务器的机器的主机名，remote_file 是要从服务器获取的文件名，local_file 是客户端为传输文件的副本使用的文件名。

/******************************************************
EXAMPLE SOCKET CLIENT
******************************************************/

#include <stdio.h>
#include <string.h>
#include "socklib.h"

/* Server's communication port number */
#define PORT 2121

/******************************************************
MAIN - This program implements the client end of a simple file transfer
system using the tiny socket library. It should be invoked with:
getfile <machine_name> <remote_file_name> <local_file_name>
**************************************************************/
main(int argc, char **argv)
{
    SOCKET *sp;
    FILE *fp;
    int sd, i;
    char namlen, c;

    /* Check correct usage */
    if (argc!=4)
        fatal("command line parameters");

    /* Open local file */
    if ((fp = fopen(argv[3], "w"))==0)
        fatal("opening local file");

    /* Create client's socket */
    if ((sp = sopen())==0)
        fatal("sopen()");

    /* Make contact with server */
    if ((sd = sclient(sp, argv[1], PORT))==-1)
        fatal("sclient()");

    /* Get length of remote file name */
    namlen = strlen(argv[2]);

    /* Send name length to server */
    if (write(sd, &namlen, 1)!=1)
        fatal("sending namlen");

    /* Send name to server */
    for (i = 0; i<namlen; ++i)
        if (write(sd, &argv[2][i], 1)!=1)
            fatal("sending file name");

    /* Read file bytes from server */
    while ((i = read(sd, &c, 1))!=0)
        if (i==-1)
            fatal("reading remote file");
        /* Write bytes to local file */
        else if (putc(c, fp)==EOF)
            fatal("writing local file");
}

/* Tidy up open files and sockets */
close(sd);
fclose(fp);
sclose(sp);
}

/**************************************************************
FATAL - Function to print a fatal error message to the standard error device and then terminate the client process.
**************************************************************/
fatal(char *text)
{
    fprintf(stderr, "Error in %s\n", text);
    exit(1);
}

## 练习

- 1. 编写一个简单的程序，以确定单个进程中同时可以打开多少个套接字。
- 2. 使用微型套接字库编写简单的客户端和服务器程序，为客户端提供有关服务器运行系统的一些信息（如当前登录的用户数，或密码文件中非 root 用户 ID 的数量等）。
- 3. 使用微型套接字库编写一个简单的聊天服务器，允许多个客户端连接并向服务器发送文本消息。服务器在收到客户端的消息后，会将消息广播给所有当前连接的客户端。用户应使用 telnet 作为客户端程序。

## 答案

1. 假设该数字不超过 1000，则以下代码片段将显示一系列数字，其中最后一个就是你需要的数字：

```
#include <stdio.h>
#include "socklib.h"

#define MAX 1000

main()
{
SOCKET *sp[MAX];
int i, j;

for (i = 0; (sp[i] = sopen())!=0 && i<MAX; ++i)
    printf("%d\n", i);

for (j = 0; j<i; ++j)
    sclose(sp[j]);
}
```

2. 这是一个直接的练习，其解决方案几乎可以直接基于本章给出的示例客户端和服务器程序。

3. 为了使该程序在单个进程中工作，有必要在套接字上使用 O_NDELAY，这样当没有文本可用时，来自客户端的读取操作不会阻塞。这允许服务器继续处理其他客户端，以查看它们是否有准备好的文本。以下代码是该问题的完整（尽管是骨架式的）解决方案。代码开头的三个 #define 指定了服务器使用的端口、服务器接受的最大行长度以及服务器将接受的最大同时客户端连接数：

```
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <errno.h>
#include "socklib.h"

#define PORT 2121
#define MAX_LEN 80
#define MAX_USERS 10

#define LINE_READY 1
#define LOGGED_OUT 2

struct client
{
    int sd;
    char in_use;
    char next;
    char text[MAX_LEN+1];
} user[MAX_USERS];

main()
{
    SOCKET *sp;
    int i, sd, flags;
    if ((sp = sopen())==0)
        fatal("sopen()");
loop:
    if ((sd = sserver(sp, PORT, S_NDELAY))!=-1)
        grab_user_slot(sd);
    else if (errno!=EWOULDBLOCK)
        fatal("sserver()");
    for (i = 0; i<MAX_USERS; ++i)
        if (user[i].in_use)
            switch(user_state(i))
            {
            case LINE_READY:
                broadcast_line(i);
                break;
            case LOGGED_OUT:
                free_user_slot(i);
                break;
            }
    goto loop;
}
user_state(int slot)
{
    char *ptr;
    int n;
    ptr = &user[slot].text[user[slot].next];
    while ((n = read(user[slot].sd, ptr, 1))==1)
    {
        if (*ptr=='\n')
        {
            *(ptr+1) = '\0';
            user[slot].next = 0;
            return LINE_READY;
        }
        if (++user[slot].next==MAX_LEN)
            --user[slot].next;
        else
            ++ptr;
    }

    if (n==0)
        return LOGGED_OUT;

    return 0;
}

broadcast_line(int slot)
{
    int i, n;

    for (i = 0; i<MAX_USERS; ++i)
        if (user[i].in_use && i!=slot)
        {
            n = strlen(user[slot].text);
            write(user[i].sd, user[slot].text, n);
        }
}

grab_user_slot(int sd)
{
    int i, flags;

    for (i = 0; i<MAX_USERS; ++i)
    {
        if (!user[i].in_use)
        {
            user[i].in_use = 1;
            user[i].sd = sd;
            user[i].next = 0;

            if ((flags = fcntl(sd, F_GETFL))==-1
            || fcntl(sd, F_SETFL, flags|O_NDELAY)==-1)
                fatal("fcntl()");

            break;
        }
    }

    if (i==MAX_USERS)
    {
        write(sd, "Too many users - sorry...\n", 26);
        close(sd);
    }
}

free_user_slot(int slot)
{
    user[slot].in_use = 0;
    close(user[slot].sd);
}

fatal(char *mess)
{
    printf("Error: %s\n", mess);
    exit(1);
}
```

## 信号

信号是进程获知系统中发生的事件的机制。信号的一个重要特性是异步，这意味着进程可能在其执行期间的任何时间收到信号，并且必须准备好在此时响应信号。甚至有可能在进程执行系统调用时收到信号。通常，如果系统调用被信号中断，则它将返回其错误值并将 errno 设置为 EINTR。此时，由收到信号的进程负责重试被中断的调用。

每种信号类型，目前大约有三十多种，都通过 <signal.h> 头文件访问的符号名来表示。最常见的信号值及其符号名如下：

| 值 | 符号 | 用途 |
|---|---|---|
| 1 | SIGHUP | 控制终端挂断 |
| 2 | SIGINT | 键盘中断（Ctrl-c） |
| 3 | SIGQUIT | 键盘退出（Ctrl-\） |
| 8 | SIGFPE | 浮点异常（例如除以 0） |
| 9 | SIGKILL | 终止接收进程 |
| 14 | SIGALRM | alarm() 系统调用超时结束 |
| 15 | SIGTERM | 默认 kill 命令信号 |
| 17 | SIGCHLD | 子进程停止或终止 |
| 19 | SIGSTOP | 从键盘 Ctrl-z 停止执行 |

每种信号类型都关联着一个动作，当进程收到该信号时，内核将代表该进程执行该动作。对于大多数信号，默认动作是终止接收进程，不过，通常进程可以请求系统的某些替代动作。各种替代方案如下：

- 忽略信号。设置此选项后，进程将不知道信号已发生。两种信号不能被忽略：SIGKILL，它将终止进程；以及 SIGSTOP，它将作为作业控制机制的一部分挂起其执行。
