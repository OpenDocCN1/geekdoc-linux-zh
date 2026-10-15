
## FIGURE 20.1

A computer performing IP masquerading or NAT has the power to hide, re-label, or consolidate machines on its private network, as far as the outside world is concerned.

- It’s difficult to run servers for the outside world on computers that reside on the internal network. If an outside client can’t see your server machine, that server might as well not exist. There are methods to get around this limitation, but I don’t describe them in much detail in this book.
- You can run servers entirely within the internal network. For instance, if you run a Samba server on a computer inside a private masqueraded network, other computers on that private network will have access to the Samba shares. The outside world will know nothing about the Samba server, though.
- Typically, the internal network’s computers use IP addresses from the reserved private IP address ranges, such as 10.x.x.x. This way, there is no chance that those addresses will accidentally conflict with addresses on the Internet as a whole. The IP masquerading computer must have two IP addresses, one for the private network, and one for the Internet as a whole.
- The IP masquerading software must know something about the protocols used on the internal network to access the Internet. To forward FTP access from an internal FTP client, for instance, the masquerading software must understand something about FTP. Linux IP masquerading does understand many common protocols, including FTP, HTTP (for Web access), SMTP (for outgoing mail), and POP (for incoming mail). Many others exist or are under development, including support for unknown protocols, so long as these protocols don’t embed IP addresses in the data stream in unexpected places. Occasionally, though, you may encounter an application that doesn’t work from inside an IP masqueraded network.

![](img/5d4d3092919d1d16884788127447cc6d_489_0.png)

These characteristics make IP masquerading an excellent choice for many small offices. If you want to provide services internal to your network, have a limited number of public IP addresses, and want to protect your internal network from the Internet as a whole while providing access to the outside for Web browsing and other common activities, setting up a dedicated IP masquerading gateway is just what you need.

## Characteristics of NAT

NAT is more flexible than IP masquerading, and in fact many NAT utilities can be configured to do much the same job as IP masquerading. In addition to IP masquerading’s features, with NAT you can

- Configure the system to let one or more computers on the internal network be seen from the Internet. You can either show these computers using their real IP addresses or another one. For instance, the internal computer on 10.0.0.2 could appear to the outside world as 151.198.0.9 (as shown in Figure 20.1), although the IP masquerading gateway is 151.198.0.1. This characteristic can be useful when your internal network is subject to frequent reorganization you want to hide from the external world.
- Feed requests from an external source addressed to a single IP address to multiple computers. For instance, suppose you have a very busy Web site and want to devote two computers to serving this site. You can do so with NAT, by configuring the two machines with identical Web pages and telling NAT to split requests for the Web site to those two internal machines. In Figure 20.1, the computers on 10.0.0.1 and 10.0.0.4 could be used in this way.
- Assign multiple external IP addresses to a single internal computer. For instance, one computer can do duty under two names in this way. (In some cases, using aliased DNS entries for a single computer or multiple NICs on one computer can accomplish the same effect.)

NAT can be extremely useful in many cases, but IP masquerading by itself can accomplish a great deal. In particular, IP masquerading is usually adequate if the internal network contains servers for internal services and client computers for Internet access. NAT is best applied when you want to run servers for the Internet at large on your internal network.

Tip

If you want to run one or two Internet servers but use IP masquerading, one alternative to NAT is to place two NICs on the Internet server. One NIC provides these machines with Internet access; the other with your private network access. This arrangement has the advantage over NAT of reducing the load on the IP masquerading server. This solution does mean, however, that you can’t use the IP masquerading machine as a firewall for the Internet servers.

## Kernel Options Needed for IP Masquerading

IP masquerading uses both kernel and non-kernel features. You must compile your kernel with a handful of options in order to get the low-level networking support that’s required for IP masquerading. In addition, you must use the ipchains utility to tell the system how to perform the masquerading. I first describe the kernel options required for IP masquerading.

## Kernel Version Requirements

IP masquerading can be performed with kernels in the 2.0.x or the 2.2.x series. The details differ substantially from one kernel version to another, however, including changes in both the kernel options and the supporting utilities. I describe the 2.2.x options in this book because Red Hat 6.0 ships with this kernel.

## Kernel Modules Needed

To use IP masquerading, your kernel must include support for several options, all in the Networking options area of the kernel configuration.

Note

Some of the IP masquerading protocols are considered experimental, so you may need to select Y for Prompt for development and/or incomplete code/drivers in the Code maturity level options section of the kernel configuration to see these protocols.
