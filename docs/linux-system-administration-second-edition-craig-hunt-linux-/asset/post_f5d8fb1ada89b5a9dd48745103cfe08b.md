
# # The Proxy Server

While a packet-filtering firewall handles filtering at the network level, a proxy server works at the application level. The filtering firewall knows nothing of which application sent the packet—only the IP address of the machine that sent it and the destination IP—but the proxy server receives data directly from an application that is set up to talk to that specific proxy on that particular port. For example, Netscape may be configured to send all requests to a proxy server that will get the requested page and return it to the Netscape application. The proxy server may also maintain a cache of the last pages visited and check each page against that cache before going onto the Internet to retrieve the requested page.

The proxy server can reside on your firewall machine (the topology looks the same as in Figure 15.2 shown earlier), on a different machine inside the firewall (as in Figure 15.4), or connected to the Internet and the local area network without the benefit of a firewall. It is usually preferable to have as little outside the firewall as possible, so putting the proxy server on a different machine that is protected by the firewall is a good idea. Sometimes the proxy is combined with the firewall, as shown in Figure 15.5.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_411_0.png)

In this setup, the proxy server intercepts any Web requests coming from clients within the firewall and checks them against an access control list, which details the sites for which access must be denied. If the requested Web page is not on this list, the request is processed normally, going either directly out on the Web or through a firewall for further processing. If the request successfully passes through the ipchains or iptables filtering on the firewall, the retrieved Web page is sent back to the requestor. If the requested Web page is on the control list, the requesting machine receives a message indicating that the URL is not accessible or not valid. Many big companies set up a proxy server to allow their users Internet access and also allow themselves to monitor the traffic.

A proxy server is much more resource-intensive than a filtering firewall, since it creates a new process for each user who connects to it. If you have a lot of traffic, you'll need at least a Pentium II with 64MB of memory, two network cards, and a 2GB or larger hard drive. This should handle around 50 concurrent users. Understand again that this is the bare minimum system that should be used. More common are Pentium III or Pentium IV proxy servers with 128–264MB of memory, two network cards, and 20–30GB hard drives.

Proxy servers are useful, but their usefulness is limited to a small subset of the available network services. Proxy servers are primarily used for HTTP. Linux systems can run a wide variety of network services, and most Linux systems run several services by default. It is a good idea to turn off any service that you don't intend to use; each service is a door that could potentially be opened by a hacker scanning for open ports. If inetd (covered in Chapter 12) is used, you can add a pound sign (#) to the start of each line in /etc/inetd.conf corresponding to the service you wish to disable any services under inetd control. For services not under inetd control, use a tool like chkconfig.

## chkconfig

In addition to services controlled through inetd or similar super servers, many services run directly, linking up to ports without using a super server. You can usually shut these down by adjusting their startup scripts, as described in Chapter 3. More commonly, however, is the use of chkconfig to shut them down. The syntax of chkconfig is as follows:

```bash
chkconfig --list [name]
chkconfig --add [name]
chkconfig --del [name]
chkconfig [--level [levels]] [name] [on|off|reset]
```

The command `chkconfig --list` without an argument will list all services and whether they are on or off as appropriate. The service state will be listed by runlevel if not governed by xinetd or inetd. An example is listed in Listing 15.10.

### Listing 15.10: Sample chkconfig Output

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| syslog | off | off | on | on | on | on | off |
| crond | off | off | on | on | on | on | off |
| netfs | off | off | off | off | off | off | off |
| network | off | off | on | on | on | on | off |
| random | off | off | on | on | on | on | off |
| rawdevices | off | off | off | off | off | off | off |
| xfs | off | on | on | on | on | on | off |
| xinetd | off | off | off | on | on | on | off |
| reconfig | off | off | off | on | on | on | off |
| anacron | off | off | on | on | on | on | off |
| httpd | off | off | on | off | off | off | off |
| apmd | off | off | on | off | off | off | off |
| atd | off | off | off | off | off | off | off |
| named | off | off | on | on | off | off | off |
| keytable | off | on | on | on | on | on | off |
| gpm | off | off | on | on | on | on | off |
| ipchains | off | off | on | on | on | on | off |
| pcmcia | off | off | on | off | off | off | off |
| kdump | off | off | on | on | on | on | off |
| kudzu | off | off | off | on | on | on | off |
| linuxconf | off | on | on | on | on | on | off |
| lpd | off | off | on | on | on | on | off |
| nfs | off | off | off | off | off | off | off |
| nfslock | off | off | off | off | off | off | off |
| sshd | off | on | on | on | on | on | off |
| identd | off | off | on | on | on | on | off |
| portmap | off | off | off | on | on | on | off |
| ypsfrd | off | off | off | off | off | off | off |
| rstated | off | off | off | off | off | off | off |
| rusersd | off | off | off | off | off | off | off |
| rwall | off | off | off | off | off | off | off |
| rwhod | off | off | off | off | off | off | off |
| smb | off | off | off | off | off | off | off |
| sendmail | off | off | on | on | on | on | off |
| rhnsd | off | off | on | on | on | on | off |
| yppbind | off | off | off | off | off | off | off |
| yppasswdd | off | off | off | off | off | off | off |
