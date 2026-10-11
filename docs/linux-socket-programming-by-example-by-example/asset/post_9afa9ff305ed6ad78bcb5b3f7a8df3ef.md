
If the `setsockopt(2)` function returns zero, the socket `$s$` has been enabled to perform broadcasting. Note, however, that the socket type chosen must be one that is capable of broadcasting, such as a UDP socket.

## Setting the SO_OOBINLINE Option

The topic of out-of-band data will be covered in Chapter 14, “Out-of-Band Data.” Here, you can just note that in some circumstances limited amounts of data can be expedited ahead of data that might already be sent. Normally, this out-of-band data is received using a different method from the usual data receiving functions. There are times, however, when it is preferred to receive this out-of-band data in the normal manner. When this method is chosen, the out-of-band data arrives ahead of the normal data as part of the normal data stream.

To enable this feature, you could use the following code:

```
#define TRUE   1
#define FALSE  0
int z;    /* Status code */
int s;    /* Socket s */
int so_oobinline;

so_oobinline = TRUE;

z = setsockopt(s,
               SOL_SOCKET,
               SO_OOBINLINE,
               &so_oobinline,
               sizeof so_oobinline);

if ( z )
    perror("setsockopt(2)");
```

After the option **SO_OOBINLINE** has been enabled, the out-of-band data will be received with the normal data. In this manner, the out-of-band data received is indistinguishable from the normal data.

## Options SO_PASSCRED and SO_PEERCRED

These options are applicable to **PF_UNIX** (**PF_LOCAL**) sockets only. These are used to control and pass credentials on sockets that are local to the current host machine. The discussion of credentials will be deferred until Chapter 17, "Passing Credentials and File Descriptors." This is perhaps the most difficult topic for you to master in this book. For now, simply note that these two options are likely to be of interest to you if you plan to write server programs that serve clients on the same local host.

## What's Next

In this chapter, you learned that socket options can be fetched and set using the functions **getsockopt(2)** and **setsockopt(2)**, respectively. It was shown that socket options have levels and various **SOL_SOCKET** level options were discussed.

Many options required Boolean values, which are defined in the **int** data type. It was shown that some other options such as **SO_LINGER**, for example, required a special structure to be used instead.

A number of socket options relate to advanced uses of sockets, which have not been covered yet. You will see these options again, as the more advanced topics are encountered in the chapters that follow. The next chapter discusses broadcasting with UDP, and consequently you are now prepared to enable the **SO_BROADCAST** option and use it!

![](img/961a0296fe36074690a9847b79332eff_346_0.png)

## Broadcasting with UDP

Communication would be inefficient if it always had to be accomplished between two individuals. Broadcasting, on the other hand, allows information to be disseminated to many recipients at once.

In this chapter, you will learn how to

-   Establish a broadcast UDP socket
-   Send broadcast messages with a socket
-   Receive broadcast messages with a socket

Upon completion of this chapter, you will know how to write programs using IPv4 socket broadcast facilities.

### Understanding Broadcast Addresses

To use broadcasting, you must know about certain IP broadcast address conventions for IPv4. (Review Figure 3.1 in Chapter 3, “Address Conversion Functions.”) Recall that the IP address is split between the Network ID portion on the left (the most significant bits) and the Host ID portion on the right (the least significant bits). The convention used for a broadcast address is that the Host ID bits are all set to 1 bits.

When your network card is properly configured, you can display the broadcast address for the interface of your choice by performing the following command (interface eth0 is shown in this example):

```
# ifconfig eth0
eth0    Link encap:Ethernet  HWaddr 00:A0:4B:06:F4:BD
        inet addr:192.168.0.1  Bcast:192.168.0.255  Mask:255.255.255.0
        UP BROADCAST RUNNING PROMISC MULTICAST  MTU:1500  Metric:1
        RX packets:1955 errors:0 dropped:0 overruns:0 frame:31
        TX packets:1064 errors:0 dropped:0 overruns:0 carrier:0
        collisions:0 txqueuelen:100
        Interrupt:9 Base address:0xe400
```

![](img/961a0296fe36074690a9847b79332eff_347_0.png)

The second line of output shows the broadcast address for the eth0 interface to be 192.168.0.255. The Network ID in this address is the first three octets (bytes) 192.168.0, whereas the Host ID part of this address is the 255 (recall that this address is a class C address). The value 255 is a decimal value representing all 1 bits for the Host ID.

### Broadcasting on 255.255.255.255

The special broadcast address 255.255.255.255 can also be used for broadcasting. Although this form of the address might suggest a broadcast to the world, it is much more limited than that. This type of broadcast is never forwarded by a router, whereas a more specific broadcast address (such as 192.168.0.255) might be forwarded, depending upon the router's configuration.

The notion of a general broadcast address like 255.255.255.255 is not very well defined. For example, some flavors of UNIX interpret this to mean that a broadcast should take place on all network interfaces for that host. Other UNIX kernels will choose only one of several interfaces—usually the first one defined. This becomes a serious issue when a host has more than one network interface card (or NIC for short). For this reason, the use of the general broadcast address is generally discouraged.

If it becomes necessary to broadcast out of every network interface, then your software should perform the following steps prior to a broadcast:

1.  Determine the next (or first) interface name.
2.  Determine the interface's broadcast address.
3.  **Broadcast using that interface's broadcast address.**
4.  Repeat steps 1 through 3 for all additional network interfaces that are active (that is, “up”) in the system.

After these steps have been performed, you can be assured that a broadcast has been made on every interface of your software.

The remainder of this chapter will focus on how to broadcast out of one network interface. After you have mastered this concept, you can then apply the preceding procedure if it becomes necessary to broadcast out of every interface.

### Enhancing the mkaddr.c Subroutine

One of the limitations of the mkaddr.c subroutine that was presented in Chapter 10, “Using Standard I/O on Sockets,” was that it was not able to properly handle the 255.255.255.255 broadcast address case. In this section, you’ll use the reason for correcting this problem.

The diff output that follows illustrates what to change in the mkaddr.c source code to fix this problem. Applying this change will allow you to experiment with the 255.255.255.255 broadcast address, if you choose to do so.

```
$ diff ../ch.11/mkaddr.c mkaddr.c
99,102c99,100
<       ap->sin_addr.s_addr =
<         inet_addr(host_part);
<     if ( ap->sin_addr.s_addr
<       == INADDR_NONE )
---
>     if ( !inet_aton(host_part,
>       &ap->sin_addr) )
$
```

![](img/961a0296fe36074690a9847b79332eff_348_0.png)

The preceding example shows that the routine inet_aton(3) function replaces the more limited inet_addr(3) function. The problem with inet_addr(3) is that it returns the value INADDR_NONE when an address is invalid. When the IP address 255.255.255.255 is converted to a 32-bit value, its return value is identical to the constant INADDR_NONE. Consequently, it becomes impossible to distinguish between a bad input IP address, and the general broadcast address. Use of the inet_aton(3) function avoids this ambiguity.
