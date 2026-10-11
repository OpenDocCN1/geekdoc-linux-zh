Table 3.2: Netmask Values by IP Class

| Class | Lowest | Highest | Netmask |
|---|---|---|---|
| A | 0.0.0.0 | 127.255.255.255 | 255.0.0.0 |
| B | 128.0.0.0 | 191.255.255.255 | 255.255.0.0 |
| C | 192.0.0.0 | 223.255.255.255 | 255.255.255.0 |

Sometimes, in networking software, your software must be able to classify a network address. Sometimes this is simply done in order to determine a default netmask value.

Listing 3.1 provides a short program that illustrates how to classify an IP address, starting from a socket address. To compile and run the provided source code, perform the following:

```
```
$ make netmask
gcc -c -D_GNU_SOURCE -Wall netmask.c
gcc netmask.o -o netmask
$ ./netmask
```
```

The program in Listing 3.1 sets up four different IP addresses in an Internet socket address structure. Then, the address is examined and classified. This is done to demonstrate how you would classify an IP address of a remote client that has connected to your server.

Listing 3.1: netmask.c--Classifying and Determining a Netmask

```
```c
1:  /* netmask.c:
2:      *
3:      * Classify an IP address:
4:      */

5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <sys/types.h>
9:  #include <sys/socket.h>
10: #include <netinet/in.h>

11:
12: int
13: main(int argc, char **argv) {
14:     int x;                    /* Index variable */
15:     struct sockaddr_in adr_inet;  /* AF_INET */
16:     int len_inet;             /* length */
17:     unsigned msb;  /* Most significant byte */
18:     char class;
19:     char *netmask;
20:     static struct {
21:         unsigned char  ip[4];
22:     } addresses[] = {
```

EXAMPLE