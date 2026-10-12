you need a static IP. Because your ISP cannot reuse that IP with its other customers, it will likely charge you more for a static IP than a dynamic IP. The average consumer doesn't need the benefit of a static IP, so he is happily paying less for a dynamically assigned IP. Also, the DNS information can be provided automatically by the ISP by the Dynamic Host Configuration Protocol, or DHCP. This is discussed in depth in Chapter 17, “Network Connectivity.”

If you are using DSL access or a cable modem, you might have a dynamic IP provided through DHCP, or you might be assigned a static IP. You might automatically be provided with the names of the DNS servers if you use DHCP, or you will need to set up DNS manually (in which case, you will need to know the IP addresses of the DNS servers).

In all cases, you will need to know your username, your password, and for the configuration of other services, the names of the mail servers and the news server. This information can be obtained from your ISP if you specifically ask for it.

> **NOTE**
> 
> The information in this book will help you understand and avoid many connection issues, but you might experience connection problems. Keep the telephone number of the technical help service for your ISP on hand in case you are not able to establish a connection. But be aware that few ISPs offer Linux support, and you might need to seek help from a Linux-savvy friend or a Linux user’s group if your special circumstances cannot be handled from the knowledge you gain from this book.

# Laying the Foundation: The localhost Interface

Prior to connecting to the Internet or network, you must create a dummy or *localhost* interface. This interface, known as *lo* (the *loopback* interface), is used by the TCP/IP protocol to assign an IP address to your machine and is required for establishing a PPP interface. The *lo* interface is also used by many network-aware applications and is easy to set up.

# Checking for the Availability of the Loopback Interface

Fedora Core normally takes care of setting up this interface during the installation. You can use the *ifconfig* command as root to see if it is already available. The command and its response will look similar to this if *lo* is available:

```
# /sbin/ifconfig

lo          Link encap:Local Loopback
            inet addr:127.0.0.1  Mask:255.0.0.0
            UP LOOPBACK RUNNING  MTU:16436  Metric:1
            RX packets:12 errors:0 dropped:0 overruns:0 frame:0
            TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:0
            RX bytes:760 (760.0 b)  TX bytes:760 (760.0 b)
```