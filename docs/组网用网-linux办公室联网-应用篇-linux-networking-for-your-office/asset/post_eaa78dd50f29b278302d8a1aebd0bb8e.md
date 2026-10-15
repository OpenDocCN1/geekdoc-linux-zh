
This command should return a series of lines like this:

```
PING 127.0.0.1 (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=255 time=0.2 ms
64 bytes from 127.0.0.1: icmp_seq=1 ttl=255 time=0.1 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=255 time=0.1 ms
```

Press Ctrl+C when you've seen enough, and you'll get statistics on the number of packets transmitted and received and the times these transfers took. You should get similar results if you use localhost in place of 127.0.0.1 when you issue the ping command. If localhost doesn't work, then you might have a problem with your /etc/hosts file.

Next, you can try the ping command on another machine. If you've configured a local network, try pinging another machine from that network. For instance, you might type

```
ping 192.168.1.2
```

Of course, the IP address you type depends on how your local network is configured. The results should be similar to the results of pinging your loopback device, though the times might be slightly longer. It shouldn't matter what operating system the target computer is running, as long as its networking features are configured correctly and it has not been configured to ignore ICMP ECHO REQUEST packets. If you've set up /etc/hosts correctly, you should be able to use the remote machine's name, such as polk, rather than the IP address.

Finally, if you're connected to the Internet through a gateway machine, you should be able to ping any computer on the Internet. Until you tell your system what to use for DNS, though, you need to use IP addresses only. As a test, try using the IP address for your ISP's or organization's DNS machine. When you've set up DNS, or if you have some IP addresses and enter them into your /etc/hosts file, you can ping outside machines by name.

Depending on the resources available on your local network, you can perform additional tests. For instance, if one of your computers runs a Telnet server, you can try using telnet on your Linux computer to log on to that machine. Alternatively, if your Linux system runs daemons for some network service, you can test the system by accessing those services from another computer. If you can successfully use ping and one or two more sophisticated tools such as telnet, ftp, or a Web browser, chances are all your networking applications, both clients and servers, will work.

## Setting the DNS Server

To access randomly selected computers on the Internet as a whole by name, you need to tell your Linux machine the IP addresses of one or more DNS servers. These servers are normally maintained by your ISP or your organization's networking department, so ask for these computers' addresses. If you're setting up your own private intranet, you might want to run DNS on your Linux computer to provide similar services to machines on that network. This task can be complex, and complete coverage of it is beyond the scope of this book, but later in the section “Setting Up a DNS Server,” you’ll find a brief outline of how to run a DNS server.

## NOTE

> If you’ll be using your intranet primarily for file and printer sharing using Samba/Windows networking or Netatalk/AppleTalk, running DNS locally might not be important. This is because both NetBIOS and AppleTalk provide their own computer naming conventions, so Internet-style names aren’t important to these services.
> If you want to access machines on your intranet for TCP/IP services such as Telnet or FTP, though, you have to enter raw IP addresses, run DNS, or maintain /etc/hosts files on all the client computers. If all your intranet’s machines are directly connected to the Internet, then your ISP or networking department’s DNS machines will handle these services, and you need not concern yourself with it, aside from configuring all of your computers as DNS clients.

## Specifying DNS Servers Manually

The primary file for configuring TCP/IP name lookups is /etc/resolv.conf. There are three types of commands in this file, in addition to comments, which are indicated by a pound sign (#):

- nameserver—A line that begins with nameserver specifies the IP address of a DNS machine. For instance, a line might read nameserver 192.168.3.100. You can specify several name servers by listing them on multiple lines.
- domain—The domain keyword indicates that the system will attempt to find the named computer in the specified domain. For instance, if the line domain biloba.com appears in /etc/resolv.conf, and if you try to access a service on host gingko, the system looks for gingko in biloba.com—that is, as gingko.biloba.com—in addition to searching for gingko by itself.
- search—The search list is similar in concept to the domain, except that you can specify several domains on a single search line, separated by spaces or tabs.

Here’s an example of an /etc/resolv.conf file:

```
# Default domain:
domain threeroomco.com
# Subnets to search:
search room1.threeroomco.com room2.threeroomco.com
```
