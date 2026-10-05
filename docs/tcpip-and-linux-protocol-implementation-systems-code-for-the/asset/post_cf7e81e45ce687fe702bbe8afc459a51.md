
## 102 TCP/IP and Linux Protocol Implementation

```c
23 gettimeofday(&then,(struct timezone *0);
24 if (select(selret,NULL, NULL, NULL, timeout) < 0) {
25     check(selret, "select");
26 gettimeofday(&now,(struct timezone *0);
27     printf("Delay %ld microseconds\n",now.tv_sec - then.tv_sec)*1000000 +
28             now.tv_use - then.tv_use);
29     exit(0);
30 }
```

As well as select(), many systems implement the poll() call.

**Figure 4.6** poll().

```c
1 #include <sys/poll.h>
2 int poll(struct pollfd *ufds, unsigned int nfds, int timeout);
```

poll() is a variation on the theme of select. It specifies an array of nfds structures of the type shown below.

**Figure 4.7** pollfd.

```c
1 struct pollfd {
2     int fd;          /* file descriptor */
3     short events;    /* requested events */
4     short revents;    /* returned events */
5 };
```

The timeout is in milliseconds, rather than the more complex structure in select().

### 4.4.2 Nonblocking I/O

In some cases, we are not interested in waiting to see if output has finished yet or not, but we wish to start it. In other cases, the programmer would like to read as much data as is available immediately if it is ready, but not to wait if there is no data yet. For this purpose, nonblocking I/O is provided, and is triggered by setting a flag in the process data associated with the file descriptor.

Figure 4.8 NBIO: pix/nbio.c.

```c
setnb()
{
    int on = 1;
    int iret;

    if ((iret=ioctl(0, FNBIO, (char *) &on) < 0)
        check(iret, "ioctl FNBIO error");
}
```

Finally, we may wish to carry out some set of tasks, but be interrupted with the arrival of new data—this can be done in user space with the use of signals. For I/O, this is set up as follows.

### 4.4.3 Asynchronous I/O

Figure 4.9 illustrates asynchronous input. Here the application continues with its current work after registering an interest in callbacks for given events.

![](img/06c11ba8be5c1c24aa633e12618e2ebd_158_0.png)

Figure 4.9 Asynchronous reception.

## TCP/IP and Linux Protocol Implementation

An example of an application using this is shown in Figure 4.10.

# Figure 4.10 SIGIO: pix/asynch.c.

```c
#include    <signal.h>
#include    <fcntl.h>

#define BUFFERSIZE 4096
int     sigflag; /* gotta be global! */
int sigio_handler()
{
    sigflag = 1;      /* just set flag and return */
}

int main()
{
    int     n, fret;
    char    buff[BUFFERSIZE];

    signal(SIGIO, sigio_handler);
    fret=fcntl(0, F_SETOWN, getpid());
    check(fret, "F_SETOWN error");

    fret=fcntl(0, F_SETFL, FASYNC);
    check(fret, "F_SETFL FASYNC error");

/* This turns async into a loop which blocks in sigpause ... */
    for (;;) {
        sigblock(sigmask(SIGIO));
        while (sigflag == 0)
            pause(0);      /* wait for a signal */

        /*
        * We're here if sigflag != 0. Also, we know that
        * SIGIO signal is currently blocked.
        */
        if ((n = read(0, buff, BUFFERSIZE)) > 0) {
            if (write(1, buff, n) != n)
                check(-1, "write error");
        } else if (n < 0)
            check(fret, "read error");
        } else if (n == 0)
            exit(0);      /* EOF */

        sigflag = 0;      /* turn off our flag */
        sigsetmask(0);    /* and reenable signals */
    }
}
```

## Alternative Programming Models

Other languages such as Java have built in mechanisms for concurrency such as threads. It can be very elegant for event handling programs to program using these.

### 4.4.4 System Include Files

There are several include files in the preceding examples that are quite generic to all socket programming, and provide the definitions of types to use the socket system layer. These are installed in /usr/include/netinet from the source tree.

Figure 4.11 IP user view of address structure: linux/include/linux/in.h.

```c
/* Structure describing an Internet (IP) socket address. */
#define SOCK_SIZE__ 16    /* sizeof(struct sockaddr) */
struct sockaddr_in {
    sa_family_t      sin_family;    /* Address family */
    unsigned short   sin_port;      /* Port number */
    struct in_addr    sin_addr;      /* Internet address */
    /* Pad to size of 'struct sockaddr'. */
    unsigned char     __pad[SOCK_SIZE__ - sizeof(short int) - 
                      sizeof(unsigned short int) - sizeof(struct sockaddr)];
};
#define sin_zero         __pad          /* for BSD UNIX comp. -FVK */
```

The IPv6 version of this is as follows (and is, not surprisingly, more complex).

Figure 4.12 IP user view of the IPv6 address structure: linux/include/linux/in6.h.

```c
struct sockaddr_in6 {
    union {
        u8_t            __u8    u6_addr[16];
        u16_t           __u16   u6_addr[8];
        u32_t           __u32   u6_addr[4];
    } in6_u;
    #define s6_addr         
    #define s6_addr16      in6_u
    #define s6_addr32      in6_u
    u8_t            sin6_family;    /* Address family */
    u16_t           sin6_port;      /* Port number */
    struct in6_addr sin6_addr;      /* Internet address */
    /* Pad to size of 'struct sockaddr_6'. */
    unsigned char     __pad[40 - sizeof(short int) - 
                      sizeof(unsigned short int) - sizeof(struct in6_addr)];
};
#define sin6_zero         __pad          /* for BSD UNIX comp. -FVK */
```
