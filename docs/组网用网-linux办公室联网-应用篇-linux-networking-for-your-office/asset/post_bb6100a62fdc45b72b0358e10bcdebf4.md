
![](img/5d4d3092919d1d16884788127447cc6d_518_0.png)

**Figure 21.3** Each firewall blocks specific types of intrusion attempts.

> **Note:** You can configure a single Linux computer to function as both a packet filter and a proxy server. This "killing two birds with one stone" approach may be suitable for a small network, but you should be aware that this approach also makes a breach of security on the firewall itself much more serious because the intruder does not need to overcome the second firewall's security.

You can add firewalls in a chain of sorts, each providing additional protection. For instance, you could insert a second packet filter in the chain shown in Figure 21.3 between the proxy server and the internal network, or between that network and a second internal network. Such a multi-layered approach can provide increasing levels of security as you move inward. You can place machines containing insensitive data, such as Web servers, behind no firewall, or perhaps just behind an initial packet filter. To get from there to a payroll computer might require traversing several more firewalls, each configured uniquely. Some such configurations are said to contain demilitarized zones (DMZs) near the Internet. A DMZ is a lightly protected area that's used for easy access to the Internet, whereas areas that lie behind additional firewalls may not be very useful for most Internet accesses, though they can gain full access to internal networking services. A DMZ can be particularly useful for running high-visibility servers.

> **Tip:** It's important that each firewall be configured uniquely in a multi-tiered layout. If a cracker can break one firewall, another with similar configuration may pose little challenge.

Another use for multiple firewalls is in segmenting a large internal network. For instance, you might want to isolate the sensitive computers in a research and development laboratory from the accounting computers or from the data entry computers staffed by temporary workers. A large organization might therefore have several firewalls.

## When Should You Use a Firewall?

Firewalls are useful security tools, but they aren't panaceas. A poorly configured firewall can actually do more harm than good by lulling you into a false sense of security. This is particularly true if you neglect security on your internal network because you think your network is protected by the firewall. On the other hand, firewalls can provide real protection and convenience. For instance:

- You can block port scans and attempts to use internal services originating from outside your intranet.
- You can deny access to known "troublemaker" sites.
- Firewalls can slow down an attacker. If an attacker takes a month to breach your firewall's security, that's one extra month in which your data are safe. Better yet, the effort involved may deter the intruder from trying.
- If you configure your firewall to log suspicious activity, you may be able to detect a break-in attempt before it succeeds. Monitoring such activity from a single computer is much less time-consuming than monitoring it from an entire network. (See "Using swatch to Monitor Log Files," p. 553, for one approach to system log monitoring.)

Overall, a firewall can be a useful component of a security policy for a site. It is only one component, though; you must also tend to the security of the computers on your intranet. You might choose to implement less stringent security on most of the machines on your intranet than you do on your firewall, but you shouldn't ignore security on these machines altogether.

## Setting Up a Packet Filter

A packet filter can be fairly unobtrusive to legitimate users, and can provide a great deal of security, particularly if your needs for connectivity with the outside world are limited to a handful of protocols. You can configure a packet filter much as you do IP masquerading, and in fact it's possible to configure a system to do both IP masquerading and packet filtering. (In this case, though, the packet filtering is likely to be done to protect the IP masquerading router itself, rather than the internal network because IP masquerading by its nature blocks connection attempts from the outside world.)

> **Note:** One alternative to using ipchains to configure a packet filter firewall is to use xinetd, which I describe in Chapter 24. The xinetd utility replaces inetd and can be configured to ignore requests for a service from one NIC while granting those requests to another. As such, xinetd is more flexible than inetd but less flexible than ipchains. xinetd's advantage is that it's much easier to configure than a packet filter firewall using ipchains.

### Kernel Options Needed for Packet Filtering

The first step in configuring a packet filter is to set up your kernel to support the necessary options. For the most part, these options are the same as those required for IP masquerading, and they're set in the kernel's Networking options configuration area:

- Network firewalls—This option is required for packet filtering.
- IP: advanced router—For a basic firewall, you can leave this option set to N, but if you want to delve into routing esoterica, you may want to set it to Y and then set subsequent options to best suit your installation.
- IP: firewalling—Again, this is a required option for packet filtering.
- IP: firewall packet netlink device—This feature allows you to monitor incoming packets with your own custom software. It's not needed for a basic firewall, but can be extremely useful for more advanced firewalls.
- IP: transparent proxy support—This feature allows you to configure a computer as a proxy server in a way that can be relatively transparent to machines on your intranet. It's not required for packet filtering, but you may want to enable it if you want to experiment with more advanced proxy server configurations.
