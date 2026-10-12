
ONBOOT=yes
DEMAND=yes

The `DEMAND` option will override the `ONBOOT` option, so the dial-up will not be started until someone actually makes a request to use the Internet. Then the dial-up will occur.

Because it can take a bit of time for dial-up connections to be established, operations may fail while dialing occurs. In particular, DNS requests can time out in 30 seconds, which may not be long enough to establish a dial-up connection. If you have three DNS servers configured for each client, you have a 90-second timeout period. As a result, the modem connection may be running before the request fails.

At this point, you should set up the client computers to use your Red Hat Linux router for their Internet connections.

## Configuring network clients

In this example, there are a variety of Red Hat Linux and Windows operating system clients on a LAN. One Red Hat Linux computer has a connection to the Internet and is willing to act as a router between the Internet and the other computers on the LAN (as described in the previous section). To be able to reach computers on the Internet, each client must be capable of doing the following things:

- Resolve the names it requests (for example, www.redhat.com) into IP addresses.
- Find a route to get from the local system to the remote system, using the local system's existing network interfaces.

Each Red Hat Linux client computer knows how to find another computer's address based on the contents of `/etc/host.conf`, `/etc/hosts`, and `/etc/resolv.conf` files. The contents of the `host.conf` file, by default, is the following:

```
order hosts,bind
```

This tells your system to check for any host names that you request by first checking the contents of the `/etc/hosts` file and then checking with name servers that are identified in the `/etc/resolv.conf` file. In our case, we will put the addresses of the few hosts we know about on our private network (whether on the LAN, direct connection, or other network interface) in the `/etc/hosts` file. Then, we will add addresses of name servers that we get from our Internet service provider to the `/etc/resolv.conf` file.

Next, each client machine must know how to get to the Internet. You do this by adding a default route that identifies the location of the router to the client computer. (Often, this router is indicated on the client as the gateway or gateway device.) This default route is used to try to access any address that the client doesn't specifically know how to reach (that is, hosts that aren't on the local LAN or other direct interface). You can add the default route using the `route` command. Here is an example:

```
# route add default gw 10.0.0.1 eth0
```

To make the default route permanent on the client Red Hat Linux system, do the following:

1. Set the default route to point to the router. This entails setting the GATEWAY or GATEWAYDEV value in the `/etc/sysconfig/network` file as described in the previous procedure. (This time, the address will point to the LAN interface of the router.)
2. Restart your network interfaces by typing the following as root user:

```
# /etc/init.d/network restart
```

3. When the computer comes back up, type the following:

```
# netstat -r
```

| Destination | Gateway | Genmask | Flags | MSS | Window | irtt | Iface |
|---|---|---|---|---|---|---|---|
| 10.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 0 | eth0 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| default | 10.0.0.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

You can see that the default gateway was set to the host at the IP address 10.0.0.1 on the eth0 Ethernet interface. Assuming that router is ready to route your packets to the Internet, your Red Hat Linux client is now ready to use that router to find all IP addresses that you request that you do not already know where to find. (The netstat -r command provides the same output as the /sbin/route command.)

## Configuring Windows network clients

If you have some Microsoft systems on your LAN, you need to configure them so that they can connect to the Internet through your router. To set up the Windows operating system computers on your private network to access the Internet through your routing computer, you have to add only a few pieces of information to each Windows system. Here’s how to do this from Windows ME and most other Windows systems:

1. Choose Start → Settings → Control Panel.
2. Open the Network icon in the Control Panel.
3. Double-click the interface shown that supports connecting to the Linux router. (For a LAN, it may look like this: TCP/IP → 3Com EtherLink III.)
4. Click the IP address tab, and then either leave the “Obtain an IP address automatically” button selected (if you are using DHCP to get the IP address, as described in Chapter 23) or select the “Specify an IP address” button (if you intend to add a static IP address). In the second case, you then need to type in the IP address and subnet mask for the host computer.
5. Click the Gateway tab, type the IP address of your Linux router, and then click Add.
6. Click the DNS Configuration tab, type in the number of the DNS server that you use to resolve addresses on the Internet, and then click Add. Repeat this step if you have multiple DNS servers.
7. Click OK.
8. You may need to reboot your computer at this point, if Windows requires you to do so.

At this point, try accessing a Web site from your Internet browser on the Windows computer. If the Internet connection is up on your Red Hat Linux computer, you should be able to connect to the Internet through your LAN connection to the Red Hat Linux computer.

## Setting up Red Hat Linux as a Proxy Server

You have a LAN set up, and your Red Hat Linux computer has both a connection to the LAN and a connection to the Internet. One way to provide Web-browsing services to the computers on the LAN without setting up routing is to configure your Red Hat Linux computer as a proxy server.

The Squid proxy caching server software package comes with Red Hat Linux. In a basic configuration, you can get the software going very quickly. However, the package is full of configuration features that let you adapt it to your needs. You can control which hosts have access to proxy services, how memory is used to cache data, how logging is done, and a variety of other features. Here are the basic proxy services available with Squid:

- **HTTP** — Allowing HTTP proxy services is the primary reason to use Squid. This is what lets client computers access Web pages on the Internet from their browsers (through your Red Hat Linux computer). In other words, HTTP proxy services will find and return the content to you for addresses that look similar to this: www.whatever.com.
- **FTP** — This represents File Transfer Protocol (FTP) proxy services. When you enable HTTP for a client, you enable FTP automatically (for example, ftp://ftp.whatever.com).
- **Gopher** — The gopher protocol proxy service was one of the first mechanisms for organizing and searching for documents on the Internet (it predates the Web by more than a decade). It isn’t used much anymore. However, if you need to use it, gopher is supported when you enable HTTP for a client.

Besides allowing proxy services, Squid can also be part of an Internet cache hierarchy. Internet caching occurs when Internet content is taken from the original server and copied to a caching server that is closer to you. When you, or someone else in the caching hierarchy, requests that content again, it can be taken from the caching server instead of having to be retrieved from the original server.

You don’t have to cache Internet content for other computers to participate in caching with Squid. If you know of a parent caching-computer that will allow you access, you can identify that computer in Squid and potentially speed your Web browsing significantly.

Caching services in Squid are provided through your Linux system’s ICP port. Besides ICP services, you can also enable Simple Network Management Protocol (SNMP) services. SNMP enables your computer to make statistics and status information about itself available to SNMP agents on the network. SNMP is a feature for monitoring and maintaining computer resources over a network.

> **CAUTION:** SNMP poses a potential security risk if it is not configured properly. Use caution when configuring SNMP with Squid.

The squid daemon process (`/usr/sbin/squid`) can be started automatically at system boot time. After that is set up, most of the configuration for Squid is done in the `/etc/squid/squid.conf` file. The sample `squid.conf` file (`/etc/squid/squid.conf.default`) contains lots of information about how to configure Squid (the file contains more than 1800 lines of comments, examples, and default settings).

For further information about the Squid proxy server, refer to the Squid Web Proxy Cache home page (www.squid-cache.org).

## Starting the squid daemon

When you install Red Hat Linux, you have an opportunity to install Squid. If you are not sure whether or not Squid was set up, there are a couple of ways to check. First, type the following as root user:

```
# ps x | grep squid
```

If the squid daemon is running, you should see an entry that looks similar to the following:

```
774 ?        S      0:00 squid -D
```

If you don’t see a Squid process running, the daemon process may not be set up to start automatically. To set up the daemon to start at boot time, type the following:

```
# chkconfig squid on
```

At this point, the squid daemon should start automatically when your system boots. By default, the squid daemon will run with the -D option. The -D option enables Squid to start without having an active Internet connection. If you want to add other options to the squid daemon, you can edit that start-up script. First, make a copy (`cp /etc/init.d/squid /etc/init.d/squid.default`) and then edit the `/etc/rc.d/init.d/squid` script. Look for the line that looks similar to the following:

```
SQUID_OPTS="-D"
```
