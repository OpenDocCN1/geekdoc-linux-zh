
# timeserver.c - 基于 socket 的时间服务

```c
/* timeserver.c - 基于 socket 的时间服务 */

#include <stdio.h>

#include <unistd.h>

#include <sys/types.h>

#include <socket.h>

#include <netinet/in.h>

#include <netdb.h>

#include <time.h>

#include <strings.h>

#define PORTNUM 13000      /* 时间服务号 */

#define HOSTLEN 256

#define oops(msg)      ( perror(msg); exit(1); )

int main(int ac, char *argv[])

{

    struct sockaddr_in saddr;   /*在此处构建地址 */

    struct hostent *hp;         

    char hostname[HOSTLEN];

    int sock_id,sock_fd;        /* 文件描述符 */

    FILE *sock_fp;               /* socket 流 */

    time_t thetime;               /* 时间 */

    char *ctime;                 /* 字符串 */

    /*

     步骤 1：向内核索要 socket

     */

    sock_id = socket(PF_INET, SOCK_STREAM, 0);   /* 获取 socket */

    if (sock_id == -1)

        oops("socket");

    /*

步骤 2：将地址绑定到 socket。地址是主机、端口

    */

    bzero(void *)&saddr,sizeof(saddr));   /* 清空结构体 */

    gethostname(hostname, HOSTLEN);   /*在哪里？ */

    hp = gethostbyname(hostname);      /* 获取主机信息 */

    memcpy((void *)hp->h_addr, (void*)&saddr.sin_addr, hp->h_length); /* 填充主机 */

    saddr.sin_port = htons(PORTNUM);   /* 填充端口 */

    saddr.sin_family = AF_INET;      /* 填充地址族 */

    if ( bind(sock_id, struct sockaddr*)&saddr, sizeof(saddr)) != 0 )

        oops("bind");

    /*

    步骤 3：在 socket 上允许队列大小为1的来电

    */

    if ( listen(sock_id, 1) != 0 )

        oops("listen");

    sock_fd = accept(sock_id, NULL, NULL);   /* 等待来电 */

    printf("Wow! got a call!\n");

    if ( sock_fd == -1)                   /* 获取调用错误 */

        oops("accept");

    sock_fp = fdopen(sock_fd, "w");      /* 将 socket 作为流 */

    if ( sock_fp == NULL)                 /* 如果我们无法 */

        oops("fdopen");                    /* 打开 */

    thetime = time(NULL);               /* 获取时间 */

    printf(sock_fp, "The time here is ...\n");

    /* 转换为字符串 */

    printf(sock_fp, "%s", ctime(&thetime));

    fclose(sock_fp);                   /* 释放连接  */

}
```
