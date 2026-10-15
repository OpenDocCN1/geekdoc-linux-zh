
The Internet is running out of IP addresses. This may sound odd at first. After all, an IP address is a four-byte (32-bit) number, meaning that there are over four billion possible IP addresses. In truth, the number is smaller than this because certain addresses are reserved or not legal for individual computers. Splitting networks into subnets further reduces the number of available computers. The allocation of IP addresses is also inefficient because ISPs and other organizations often lay claim to more IP addresses than they need at the time they register the addresses in order to have the addresses immediately available when they are needed. Because of these factors, the number of available IP addresses is dwindling fast.

You might not personally feel this squeeze, but maybe you do. This problem manifests itself on a smaller scale in many organizations. You might work for a firm that has assigned your department a handful of IP addresses, but you suddenly find that you need to add more networked computers than you have IP addresses. If you find yourself in this situation, Linux’s ability to perform IP masquerading can be a great boon. This feature allows a Linux computer to link to two networks in such a way that one network doesn’t know the other exists. Typically, the larger network believes that all requests coming from the smaller network originate from the Linux computer that does the masquerading. This fact allows you to hide a potentially very large number of computers behind the Linux box, thus conserving IP addresses.

IP masquerading is particularly helpful for home and small office networks that link to the Internet via a PPP, cable modem, or DSL line. Providers of these services often restrict you to a single IP address. (This is particularly true of PPP links, which support only a single IP address, and many cable and low-end DSL providers that market their services to home users.)

## CAUTION

Your ISP might or might not object to your using IP masquerading to connect more than one computer to the Internet. Some ISPs maintain policies that allow them to terminate your service or charge you higher rates if they determine that you’re using IP masquerading. You should definitely check with your ISP before engaging in this practice. If you’re using IP masquerading on a larger corporate intranet in order to stretch your department’s pool of IP addresses, you’re less likely to run into such a problem, but you might want to check with whoever manages your organization’s network to be sure.

IP masquerading has one additional benefit: It provides many of the characteristics of a firewall, protecting the computers on the internal network from outside intruders. Of course, this protection is only as good as the security on the IP masquerading computer; if its security is breached, and if you’re lax about internal security, an intruder will have free reign over your internal network.

## IP Masquerading Versus NAT

If you check non-Linux networking newsgroups, you’ll probably run across frequent mention of a technique called network address translation (NAT). NAT and IP masquerading are similar techniques. IP masquerading is more common in the Linux world, whereas NAT is more common in Windows. I therefore describe IP masquerading in this chapter. If you prefer to use NAT, you can do it in Linux. I suggest you check the Web page http://linas.org/linux/load.html for more information on NAT for Linux.

## The Basic Goal: Linking Networks

Figure 20.1 shows the core of an IP masquerading or NAT configuration. One computer serves as a router between two networks: an internal private network and a larger one (called the Internet in Figure 20.1 because the larger network usually is the Internet). The larger network doesn’t see the smaller network quite as it is, though. Instead, the router performs some sort of translation on packets as they traverse the networks, thus altering the outside’s view of the private network. Figure 20.1 depicts a NAT configuration in which two of the internal computers receive the same address as the router itself, as far as the outside world is concerned, whereas two other computers each receive unique addresses unrelated to their internal identities. In an IP masquerading setup, all the computers would appear under the same external IP address.

## Characteristics of IP Masquerading

IP masquerading is the simpler of the two techniques. When you configure IP masquerading, all requests coming from the intranet and targeted at the Internet will appear to the Internet server to come from the IP masquerading computer. To the outside world, it looks as if there’s one computer, not many. If the internal network generates a lot of Internet traffic, it might appear to be a very busy single computer, but only one nonetheless. Consequences of this approach include

- IP masquerading serves as an effective firewall for the private network. If outsiders can’t locate an internal computer, outsiders can’t break into the internal computer. (Of course, the masquerading computer must be secure, which is a complex topic itself.)
