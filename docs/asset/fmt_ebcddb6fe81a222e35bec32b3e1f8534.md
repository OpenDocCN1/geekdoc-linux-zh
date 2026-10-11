
```c
/*
** 统计收集循环
*/
while(1)
{
   /*
```

# 附录 A 源代码

## 列表 A.5 继续

```
** 真实内存利用率
/*
fptr = fopen("/proc/meminfo", "r");
gets(buf, sizeof(buf), fptr); /* 跳过表头 */
gets(buf, sizeof(buf), fptr);
buf[strlen(buf)-1] = 0;
sscanf(buf, "%*s %ld %ld", &tmem, &umem);
fem = (float) umem / (float) tmem;
stats.rm = (int) (100 * (fmem + .005));
fclose(fptr);

/*
** 后续 CPU 利用率
/*
fptr = fopen("/proc/stat", "r");
gets(buf, sizeof(buf), fptr);
buf[strlen(buf)-1] = 0;
sscanf(buf, "%*s %ld %ld %ld", &usec1, &nsec1, &isec1);
/* 计算 CPU 利用率 */
usec1 = use0; /* 1秒用户态 */
nsec1 = nsec0; /* nice */
ssec1 = ssec0; /* 系统 */
isec1 = isec0; /* 空闲 */
fcpu = (float) (usec1 + nsec1 + ssec1) / (float)(usec1 + nsec1 + ssec1 + isec1);
stats.cp = (int) (100 * (fcpu + .005));

/*
** 后续磁盘 I/O 速率（也在 /proc/stat 中）
/*
while((gets(buf, sizeof(buf), fptr)) != NULL) {
	if(strnmp(buf, "disk_rio", 8) == 0) /* 跳过 * */
	break;
}
sscanf(buf, "%*s %ld", &rio);
/* disk_rio 之后的字符串是 disk_wio */
gets(buf, sizeof(buf), fptr);
sscanf(buf, "%*s %ld", &nio);
fclose(fptr);
```

近实时性能

## 列表 A.5 继续

```
/* 计算磁盘 I/O 速率 */
stats.dr = (rio1 - rio0) / 5;
stats.dw = (wio1 - wio0) / 5;
fclose(fptr);
```

```
/*
** 后续网络 I/O 速率
*/
fptr = fopen("/proc/net/dev", "r");
/* 跳过 net dev 中的列表头字符串 */
gets(buf, sizeof(buf), fptr); /* 跳过 */
gets(buf, sizeof(buf), fptr); /* 跳过 */
gets(buf, sizeof(buf), fptr); /* 跳过 */
gets(buf, sizeof(buf), fptr); /* 跳过 eth0 */
buf[strcsp(buf,"\n")] = 0; /* 替换 '\n' */
buf[6] = ' '; /* 替换 '; ' */
sscanf(buf, "%*s %ld %*d %*d %*ld", &rpkts1, &spckts1);
/* 计算网络 I/O 速率 */
stats.pr = rpkts1;
stats.ps = spkts1 - spkts0;
fclose(fptr);
```

```c
/*
** 重置下一次迭代的值
*/
rpkts0 = rpkts1;
spckts0 = spkts1;
usec0 += usec1;
sec0 += nsec1;
ssec0 += ssec1;
isec0 += isec1;
```

```c
/*
** 每1秒发送一次统计信息
*/
sendto(fd, &stats, sizeof(stats), 0,
    (struct sockaddr *) &soc, sizeof(soc));
sleep(1);
```

rio0 = rio1;

wio0 = wio1;

```

# 附录 A 源代码

监控进程运行在一个非集群节点上，在我们的示例中命名为 `omega`。它接收来自运行在集群节点上的每个性能任务的信息，显示整体系统性能信息以便快速进行视觉参考。更多细节请参见第 8 章。以下是启动监控任务的命令行：

> `monitor`

注意，该命令没有命令行操作数。另请注意，你可以根据方便随时启动和停止此任务；在任务运行时发送的任何 UDP 数据包将被被丢弃。

## 列表 A.6 集中化性能监控进程

```c

#include <netinet/inet.h>

#include <sys/socket.h>

#include <string.h>

#include <stdio.h>

#include <netdb.h>

#include "cpm.h"

main(void)

{

    /*

     ** monitor.c - 集中化性能监控

     */

    int cp[4], rm[4]; /* 中央处理器, 真实内存 */

    int ps[4], pr[4]; /* 发出的包, 接收的包 */

    int dr[4], dw[4]; /* 磁盘读取, 磁盘写入 */

    union {

        unsigned long addr;

        char bytes[4];

    } u;

    struct sockaddr_in in_soc;

    struct cprStats stats;

    int len=sizeof(soc);

    struct hostent *hp;

    int fd, ii, jj;

    int netload;

    char buf[256];

    /* 建立并初始化 UDP socket 结构体 */

    fd = socket(AF_INET, SOCK_DGRAM, 0);

    memset((char *) &soc, 0, sizeof(soc));

```

```c

soc.sin_addr = htonl(INADDR_ANY);

soc.sin_port = htons(PORT);

soc.sin_family = AF_INET;

bind(fd, (struct sockaddr *) &soc, len);

```

```c

/* 初始化 */

for(ii=0; ii<4; ii++) {

    cp[ii] = 0;

    rm[ii] = 0;

    ps[ii] = 0;

    pr[ii] = 0;

    dr[ii] = 0;

    dw[ii] = 0;

}

```

```c

/*

** 集中化性能报告

*/

while(1) {

    for(ii=0; ii<4; ii++) {

        recvfrom(fd, &stats, sizeof(stats), 0,

            (struct sockaddr *) &soc, &len);

        /* 索引为 IP 地址 */

        memcpy(&u.addr, &soc.sin_addr, 4);

        jj = (unsigned int) u.bytes[3];

        cp[jj] = stats.cp;

        rm[jj] = stats.rm;

        ps[jj] = stats.ps;

        pr[jj] = stats.pr;

        dr[jj] = stats.dr;

        dw[jj] = stats.dw;

    }

}

```

```c

/*

** 计算网络负载

*/

netload = 0;

for(ii=0; ii<4; ii++) {

    netload += (ps[ii] + pr[ii]);

}

netload /= 2; /* 每个节点发送和接收的平均值 */

/*

** 绘制显示集群统计信息的图 */

system("clear");

printf("\n REAL-TIME PERFORMANCE STATISTICS \n");

printf("\nBase \n");

printf("\nALPHA-\tBETA+\n");

printf("\nCPU |\tCPU |\n");

```

此 C 头文件在 `perform` 和 `monitor` 中引用。它描述了数据包的内容。

## 列表 A.7 性能报告头文件

```c

/*

** report.h - 被 report.c 和 perform.c 引用

*/

#define PORT 9090
