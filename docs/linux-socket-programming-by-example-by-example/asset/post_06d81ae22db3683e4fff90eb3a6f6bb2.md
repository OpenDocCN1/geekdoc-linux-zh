
Before any value is placed into this union, your C program might initialize the union as follows:

```
u.sa.sa_family = AF_UNSPEC;
```

Later in the program, when you go to place an `AF_INET` address into this union, you would use:

```
u.in.sin_family = AF_INET;
```

The `AF_UNSPEC` acts as a safe placeholder for you when you don't know what the address family is yet.

# What's Next

Socket addressing is the messiest part of socket programming, but that is all behind you now. With the examples that you have worked through, you now know how to apply local addresses, Internet addresses, and a few others. You learned that each address structure must have its corresponding address family constant stored in it (`AF_INET`, for example).

In this chapter, you learned that the `AF_INET` address was sensitive about network ordered bytes in the `sin_port` and `sin_addr` members. The byteorder(3) conversion functions were mastered to deal with this problem.

You also saw that each address family has its own quirks for establishing both the address itself and the length of the address. Consequently, this chapter will continue to serve as a reference for you.

In the next chapter, you'll build upon the concept of network addresses that you've learned and you'll be introduced to new library functions that manipulate addresses for you.

# Address Conversion Functions

In the last chapter, you learned how various types of socket addresses could be allocated and initialized. These were all simple cases of initializing from a constant. Setting up an address from a C string with varying addresses requires more programming effort. In this chapter, you will focus on the additional issues pertaining to establishing Internet addresses, and learning about the functions that can assist you in this area.

In this chapter, you will learn about:

- Classes of internet addresses
- IP netmasks
- Private and reserved IP numbers
- Functions that convert IP numbers

Before you get started however, it's a good time to review the design of an IP address. Then, you'll have a greater insight into the job that is ahead of you.

![](img/961a0296fe36074690a9847b79332eff_82_0.png)

# Internet IP Numbers

The IP number consists of four decimal values separated by decimal points, often referred to as "dots." This convention is frequently called *dotted-quad* notation, or sometimes *dotted-decimal* notation. Each decimal byte represents the unsigned value of one byte, in network byte sequence. Remember that network order requires that the most significant bytes appear first.

Each byte is considered as an unsigned 8-bit value. This restricts each byte to a decimal value range of zero to 255. Because the value is unsigned, the value cannot be negative, and a plus sign is not permitted. Consider the address 192.168.0.1; for example, you know that the first byte in network order must have the value of 192 decimal.

When you see a movie showing an IP number on the screen with a value such as 192.168.300.5, you know that the producer knew very little about TCP/IP networking! Although this IP number is syntactically correct, the decimal value 300 obviously exceeds the maximum unsigned value of 255.

Later, starting with the section "Manipulating IP Numbers," you will look at functions that can parse a C string into network address bytes, and range check the decimal values for you.

# Internet Address Classes

Internet addresses are made up of two components:

- Network number (most significant bits)
- Host number (least significant bits)

The network number identifies the network where the host can be contacted. The host number identifies one host (your PC, for example) out of several on that particular network.

As you already know, the IP number is a 32-bit value (or four 8-bit bytes). However, the division between the network address and host number components is not at a fixed location. The dividing line depends upon the classification of the address, which is determined by examining the most significant byte of the address. Table 3.1 summarizes how IP numbers are classified.

Table 3.1: Internet Address Classes

| Class | Lowest | Highest | Network Bits | Host Bits |
| :--- | :--- | :--- | :--- | :--- |
| A | 0.0.0.0 | 127.255.255.255 | 7 | 24 |
| B | 128.0.0.0 | 191.255.255.255 | 14 | 16 |
| C | 192.0.0.0 | 223.255.255.255 | 21 | 8 |
| D | 224.0.0.0 | 239.255.255.255 | 28 | N/A |
| E | 240.0.0.0 | 247.255.255.255 | 27 | N/A |

Class A, B, and C define specific IP addresses of hosts. For class D and E addresses, there are zero host bits available in the address. Class D addresses are used for multicasting where the 28 bits are used to describe a multicast group. The 27 bits of the class E address are reserved.

Figure 3.1 helps you visualize the breakdown of the 32-bit IP address. The frequently used classes A, B, and C are shown.

![](img/961a0296fe36074690a9847b79332eff_84_0.png)

> **Figure 3.1:** *This figure illustrates the Internet address classes A, B, and C.*

## Understanding Netmask Values

There are situations in which you must determine the *netmask* value of an address. This is particularly true if you are setting up your own network. So, just what is a netmask value anyway?

If you take the Internet IP Address as a 32-bit number, then you know that the network ID is specified in the most significant bits of the address. Additionally, the host ID is specified by the least significant bits of the same address (review Figure 3.1 if necessary). The netmask is simply the value that you would "bit-wise and" with the address to leave only the network ID. Figure 3.2 illustrates how the IP address 192.168.9.1 is masked to extract only the network ID bits.

> **TIP**
> You will often hear people use the terms *net* and *subnet* interchangeably. Technically speaking, these terms represent two distinctly different network ID values. The network ID identifies the network ID number proper.

However, within an IPv4 number, it is possible to further subdivide the host ID leaving a subnetwork ID in the most significant bits of the host ID and the final host ID in the least significant bits. When subnetting is used, the netmask value will take into account these additional subnetwork ID bits.

Consequently, when subnetting is in use, the network mask will differ from the ones presented in this chapter.

![](img/961a0296fe36074690a9847b79332eff_85_0.png)

*Figure 3.2: Applying a netmask to 192.168.9.1 yields a network address.*

The resulting most significant bits represent the network portion of the IP address without the host ID. Figure 3.3 illustrates how the network mask is converted from hexadecimal back into dotted-quad notation.

![](img/961a0296fe36074690a9847b79332eff_85_1.png)

*Figure 3.3: Here is the netmask expressed in dotted-quad notation.*

If you must set up your own IP network, then you will need to determine what the netmask values should be. Table 3.2 lists the netmask values for class A, B, and C addresses.

Table 3.2: Netmask Values by IP Class

| Class | Lowest | Highest | Netmask |
| :--- | :--- | :--- | :--- |
| A | 0.0.0.0 | 127.255.255.255 | 255.0.0.0 |
| B | 128.0.0.0 | 191.255.255.255 | 255.255.0.0 |
| C | 192.0.0.0 | 223.255.255.255 | 255.255.255.0 |

Sometimes, in networking software, your software must be able to classify a network address. Sometimes this is simply done in order to determine a default netmask value.

Listing 3.1 provides a short program that illustrates how to classify an IP address, starting from a socket address. To compile and run the provided source code, perform the following:

```
$ make netmask
gcc -c -D_GNU_SOURCE -Wall netmask.c
gcc netmask.o -o netmask
$ ./netmask
```

The program in Listing 3.1 sets up four different IP addresses in an Internet socket address structure. Then, the address is examined and classified. This is done to demonstrate how you would classify an IP address of a remote client that has connected to your server.

Listing 3.1: netmask.c--Classifying and Determining a Netmask

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
