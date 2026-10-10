You can also spot MAC addresses from the FreeBSD DHCP server. One way to do so is to use *arp*, which modifies or displays information on the computer's low-level IP address and MAC address tables. The following command locates the MAC address of another computer, provided you know its IP address or hostname:

```
$ arp 192.168.1.2
tee la.rod sbooks. com (192.168.1.2) at 00:05: 02:a 7:76:da on f xp0 (ethernet)
```

> *Note*
> *You may need to contact the target system, say by pinging it, before this command will work.*

One drawback to this method is that the computer must already have an IP address. Even a dynamic IP address assigned by the DHCP server will do (you can later reboot the computer to force it to pick up its new custom IP address); or you can temporarily configure the computer to use a static address that you assign manually. Another option is to physically examine the network card; some manufacturers write the MAC address on a sticker affixed to the card.

# ## DNS Servers

DHCP servers run in the background of many networks and go largely unnoticed unless they malfunction. Similarly, Domain Name System (DNS) servers obtrude themselves on users' awareness only when something goes wrong. These servers, as described briefly from the client's perspective in Chapter 14, translate (or *resolve*, as this translation is often called) hostnames to IP addresses and vice versa. When implemented on a small or even mid-sized network, DNS servers can be small computers. In fact, they're often run on the same hardware that hosts DHCP servers. DNS server setup entails configuring two types of files in addition to the server startup script: one file to control the server overall, and one or more files to tell the server about the domains it's to handle.

# ### When to Run a DNS Server

DNS servers provide services to two different types of users:

+   * **Internal users** Computers on your own network may call upon a local DNS server to resolve hostnames or IP addresses. The DNS server can then deliver IP addresses associated with local hostnames or contact outside DNS servers to look up an external hostname.

+   * **External users** If you operate your own domain, you're required to provide at least two DNS servers that deliver name resolution services for the domain. In practice, it's often desirable to use an outside service for this function, particularly for small domains. If you have static externally-accessible IP addresses, though, you can run your own DNS servers. Doing so gives you direct control over every