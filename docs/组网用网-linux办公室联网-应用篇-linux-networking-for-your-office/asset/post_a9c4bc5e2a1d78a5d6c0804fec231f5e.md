
- Failed connections—If the ISP's line is busy or otherwise down, your connection attempts will fail. If the client system is in a different room from the IP masquerading computer, or if the modem's volume is turned down, you may not realize what's happened because you won't hear the busy signal from the modem.
- Dropped connections—Dial-on-demand automatically drops connections after a period of inactivity. This period varies from one connection type to another, and you may want to adjust the values, as described in Chapter 8, to best match your needs. With some protocols, you may need to exit from the client program and start it up again if dial-on-demand closes the PPP link.
- Speed—PPP links over modems are typically much slower than always-up connections via T1, cable modem, DSL link, or other technologies.

Overall, the combination of dial-on-demand with IP masquerading can be useful for low-cost access for a very small network with modest Internet access needs. A larger network or one with more substantial access needs should look into another access method, either using IP masquerading or several IP addresses for direct connections for all (or at least several) computers.

## Bandwidth Limitations

IP masquerading funnels all data for an entire intranet through a single computer. If your network generates a lot of traffic (either incoming or outgoing), you may begin to see the performance limitations of this design. This is particularly true if your link to the outside world is over a low-end connection like a PPP dialup link. Even a DSL or T1 line may be inadequate to the task if your intranet is large enough or if that network generates enough traffic.

For instance, suppose your intranet consists of six computers plus the IP masquerading machine. If the computer polk attempts to download the latest Red Hat Linux over a 56kbps PPP dialup, polk will demand most of the available bandwidth for several hours—probably over a day, in fact. The user of polk may initially see transfer speeds of, say, 50KB/s, which is about as high as can be expected on an average V.90 modem link. Now, suppose that tyler's user tries to download the latest Debian Linux distribution while the Red Hat download is still in progress. The total bandwidth of the modem doesn't change, so polk and tyler will split that bandwidth, and each will get only 25KB/s. Meanwhile, the other four users will find that their Web browsing and other network accesses are unusually slow.

IP masquerading doesn't magically produce more bandwidth; it's just a way to share the bandwidth that's provided to a single computer. You should definitely consider this when planning your network connection.

## Note

The same comments apply to using any computer as a firewall, router, or bridge of any type. Typically, bandwidth is limited by the slowest networking link in a configuration, be that a 56kbps PPP link, a 640kbps DSL link, a 10Mbps Ethernet link, or something else. This limited bandwidth must be divided among all the computers that use it. If your hardware is particularly high-speed, the bottleneck may become an oversubscribed ISP or even the Internet backbone. At busy times of busy days, this becomes true even of 56kbps dialup lines, as you’ve probably experienced when browsing the Web at such times.

## Being a Good Netizen

IP masquerading’s limitations apply not only to the technical side, but also socially. In particular, many ISPs object to the use of IP masquerading. This is because a typical ISP expects users to consume a certain amount of bandwidth and, in the case of dial-up technologies, a certain number of hours of online time. When you subscribe with an ISP for, say, 640kbps DSL service, your ISP expects that you will not be using the full 640kbps of bandwidth 24 hours a day, 7 days a week. Instead, the ISP expects that you’ll consume brief bursts of 640kbps and average some fraction of that amount. Ten, twenty, or a hundred subscribers together may consume 640kbps of bandwidth for an extended period of time at peak hours. If you use more bandwidth than the ISP expects, that drives up the ISP’s costs. Hence, many ISPs impose limits of various sorts on the use of services.

## Always-On and On-demand Connections

Some connection technologies, such as DSL and cable modems, are always-on technologies, meaning that you’re always connected to the Internet, assuming the hardware is always powered up. You might not be using the bandwidth at any given time, however.

An ISP providing always-on service expects to provide the basic connectivity 24 hours a day, but does not expect you to transfer data continuously during that period. Other technologies, like PPP, are generally used in an on-demand fashion, in which the physical connection is formed and broken as the need for transfers arises. An ISP providing on-demand services may have more subscribers than hardware to connect the subscribers because chances are not everybody using the service will want to use it at once. Even when connected, subscribers probably won’t use 100% of their bandwidth.

In an always-on environment, ISPs tend to sell services without temporal usage limits, but sometimes forbid the running of certain servers, or meter the service by the megabyte transferred. On-demand ISPs often limit access by time because the number of connection ports (such as modems) is an important limiting factor to the service. On-demand ISPs also often forbid certain activities, although this is more often to prevent undesirable behavior, such as spamming, than to control costs.
