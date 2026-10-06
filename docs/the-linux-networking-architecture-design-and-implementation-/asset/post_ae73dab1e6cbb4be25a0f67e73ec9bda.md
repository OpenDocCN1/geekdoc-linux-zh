
```c
(void *) 1,
NULL
};
int test_pack_rcv(struct sk_buff *skb, struct net_device *dev, struct
    packet_type *pt)
{
    printk(KERN_DEBUG "Test protocol: Packet Received with length: %u\n",
    skb->len);
    return skb->len;
}
int init_module(void)
{
    dev_add_pack(&test_protocol);
    return 0;
}
void cleanup_module(void)
{
    dev_remove_pack(&test_protocol);
}
```

## APPENDIX F
### Example for a Transport Protocol

****************************************************************
* Example for a transport protocol
* Compile:
* gcc -I/lib/modules/uname -r/build/include -c file.c
****************************************************************

```c
#ifndef __KERNEL__
#define __KERNEL_
#endif
#ifndef MODULE
#define MODULE
#endif

#include <linux/module.h>
#include <linux/version.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/skbuff.h>
#include <linux/in.h>
#include <net/protocol.h>

MODULE_AUTHOR("Test Author (fixme@Linux-netzwerkarchitektur.de)");
MODULE_DESCRIPTION("Module with a layer-4 test protocol");

int test_proto_rcv(struct sk_buff *skb);
static struct inet_protocol test_protocol = {
	&test_proto_rcv,    /* protocol handler */
	NULL,               /* error control */
	NULL,               /* next */
	IPPROTO_TCP,        /* protocol ID */
};
```

```c
0,
NULL,                /* copy */   /* data */
    "Test_Protocol"      /* name */
;
int test_proto_rcv(struct sk_buff *skb)
{
    printk(KERN_DEBUG "Test protocol: Packet Received with length: %u\n",
           skb->len);
    return skb->len;
}
int init_module(void)
{
    inet_add_protocol(&test_protocol);
    return 0;
}
void cleanup_module(void)
{
    inet_del_protocol(&test_protocol);
}
```

## APPENDIX G
### Example for Communication over Sockets

#### G.1 SERVER

```
****************************************************************************************************
* Socket example: Chat application, server component comm_s.c
* Compilation: gcc -o comm_s comm_s.c
* comm_s <port> is used to start a server on each end system,
* and comm_c <destination system> <port> is used to start an
* arbitrary number of clients.
* All messages written in the client are displayed at the respective
* destination server.
****************************************************************************************************
```

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <signal.h>
#include <string.h>
/* Macro for easier output of IP addresses with printf() */
#define NTOPOUAD(addr) \
    ((unsigned char*)&addr)[0], \
    ((unsigned char*)&addr)[1], \
    ((unsigned char*)&addr)[2], \
    ((unsigned char*)&addr)[3]

#define BUFSIZE 1024
char buf[BUFSIZE + 1];
```

#### 596 Appendix G Example for Communication over Sockets

```c
* Signal handler to accept the SIGCHLD signal when terminating
* child processes; otherwise, these zombie processes would remain.
*/
```

```c
void sighandler(int dummy)
{
    wait(NULL);
}
```

```c
/* Function to serve a client:
* Read available characters from socket into the buffer.
* Search for end-of-line character; if found, or if buffer full:
* output message, move the rest forward, and repeat.
* Abort, if error, or connection closed.
*/
```

```c
void serve(int s, struct sockaddr_in *peer)
{
    int space, n;
    char *p, *q;
    q = p = buf; space = BUFSIZE;
    while (1) {
        if ((n = read(s, p, space)) <= 0) break;
        p += n; space -= n;
        while ((q < p) && (*q != '\n')) q++;
        while ((q < p) || !*q) {
            *q = 0;
            printf("message from %d.%d.%d.%d: %s\n",
                NIPQUAD(peer->sin_addr.s_addr), ntohs(peer->sin_port), buf);
            if (q < p) q++;
            memmove(buf, q, p - q);
            n = q - buf; // Number of characters "done"
            p -= n; space += n;
            q = buf;
            while ((q < p) && (*q != '\n')) q++;
        }
    }
}
```

```c
if (n < 0) perror("read");
else if (p > buf) { // Output rest
    *p = 0;
    printf("message from %d.%d.%d.%d: %s\n",
        NIPQUAD(peer->sin_addr.s_addr), ntohs(peer->sin_port), buf);
}
```

```c
/* Main program:
* Process arguments
* Open socket and wait for connections
* Start separate process for each new connection
*/
```

```c
int main(int argc, char *argv[])
{
    int s;
    struct sockaddr_in myaddr;
    int optval;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <port>\n", argv[0]); exit(1);
    }
    if ((s = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("socket");
        exit(1);
    }
    /* Socket option SO_REUSEADDR: Allow bind(), even when old
    protocol instances are still using the address. */
    optval = 1;
    if (setsockopt(s, SOL_SOCKET, SO_REUSEADDR, &optval, sizeof(optval))) {
        perror("setsockopt");
        exit(1);
    }
    memset(&myaddr, 0, sizeof(myaddr));
    myaddr.sin_family = AF_INET;
    myaddr.sin_port = htons(atoi(argv[1]));
    myaddr.sin_addr.s_addr = INADDR_ANY;

    if (bind(s, (struct sockaddr *)&myaddr, sizeof(myaddr)) < 0) {
        perror("bind");
        exit(1);
    }
    if (listen(s, SOMAXCONN) < 0) {
        perror("listen");
        exit(1);
    }
    /* Install signal handler for SIGCHLD */
    signal(SIGCHLD, sighandler);
    while (1) {
        struct sockaddr_in clientaddr;
        socklen_t len = sizeof(clientaddr);
        int client;
        if ((client = accept(s, (struct sockaddr *)&clientaddr, &len)) < 0) {
            perror("accept");
            continue;
        }
        if (fork() == 0) { // Child process
            close(s);
            close(client);
            while (fgets(buf, BUFSIZE, stdin)) != NULL) {
                printf("message from %d.%d.%d.%d: %s\n",
                    NIPQUAD(clientaddr.sin_addr.s_addr), ntohs(clientaddr.sin_port), buf);
            }
            close(client);
            exit(0);
        } // Parent process
        close(client);
    }
}
```

[621
### Example for Communication over Sockets

#### G.2 CLIENT

```
* Socket example: Chat application, server component comm_s.c
* Compilation: gcc -o comm_s comm_s.c
* comm_s <port> is used to start a server on each end system,
* and comm_c <destination system> <port> is used to start an
* arbitrary number of clients.
* All messages written in the client are displayed at the respective
* destination server.
```

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <signal.h>
#include <string.h>
/* Macro for easier output of IP addresses with printf() */
#define NTOPOUAD(addr) \
    ((unsigned char*)&addr)[0], \
    ((unsigned char*)&addr)[1], \
    ((unsigned char*)&addr)[2], \
    ((unsigned char*)&addr)[3]

#define BUFSIZE 1024
char buf[BUFSIZE + 1];

/* Main program:
* Process arguments
* Open socket and wait for connections
* Start separate process for each new connection
*/
```

```c
int main(int argc, char *argv[])
{
    int s;
    struct sockaddr_in myaddr;
    int optval;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <port>\n", argv[0]); exit(1);
    }
    if ((s = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("socket");
        exit(1);
    }
    /* Socket option SO_REUSEADDR: Allow bind(), even when old
    protocol instances are still using the address. */
    optval = 1;
    if (setsockopt(s, SOL_SOCKET, SO_REUSEADDR, &optval, sizeof(optval))) {
        perror("setsockopt");
        exit(1);
    }
    memset(&myaddr, 0, sizeof(myaddr));
    myaddr.sin_family = AF_INET;
    myaddr.sin_port = htons(atoi(argv[1]));
    myaddr.sin_addr.s_addr = INADDR_ANY;

    if (connect(s, (struct sockaddr *)&myaddr, sizeof(myaddr)) < 0) {
        perror("connect");
        exit(1);
    }

    while (1) {
        if (fgets(buf, BUFSIZE, stdin)) != NULL) {
            send(s, buf, strlen(buf), 0);
        }
    }
}
```

[622
### Bibliography

- Almeberger, Werner. Traffic Control: Next Generation. SourceForge.net, 2001.
- Beck, Michael, Harald Böhm, and Ulrich Kunitz. Linux Kernel Programming. Boston: Addison-Wesley, 3rd ed., 2002.
- Böhm, Uwe and Lennert. BRIDGE-STP-HOWTO. http://www.tldp.org/HOWTO/BRIDGE-STP. (Visited December 23, 2003.)
- Blank, Mitchell. Project: ATM on Linux. SourceForge.net/projects/linux-atm. (Visited January 9, 2003.)
- Bovet, Daniel P. and Marco Cesati. Understanding the Linux Kernel. Beijing and Cambridge, MA: O'Reilly. 2000.
- BradBP, R. Laden, D. Borman, and C. Partridge. Requirements for Internet Hosts—Communication Layers. Internet Engineering Task Force (IETF), Requests for Comments (RFC) 1122, October 1989. http://www.faqs.org/rfcs/1122.html. (Visited on December 23, 2003.)
- Deer, Stephen E. Deering. Host Extensions for IP Multicasting, Internet Engineering Task Force (IETF). Requests for Comments (RFC) document series, RCF 988, July 1986. http://www.faqs.org/rfcs/988.html. (Visited on December 23, 2003.)
- Chewick, William R. and Steven M. Bellovin. Firewalls and Internet Security: Repelling the Wiley Hacker. Reading, MA: Addison-Wesley, 1994.
- Come, Douglas E. Principles, Protocols, and Architecture, vol. 1 of Interworking with TCP/IP. Upper Saddle River: Prentice Hall, 4th ed., 2000.
- Bytenenkk, Lennert. Linux Bridge Utilities. Sources at http://bridge.sourceforge.net, 2001. (Visited January 9, 2004.)
