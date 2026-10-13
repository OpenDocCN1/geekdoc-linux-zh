
The preceding line says to configure the interface eth0 and give it the IP address 192.168.0.2. This will be on a network defined by 192.168.0.0–192.168.0.255 and will use the broadcast address of 192.168.0.255. You can omit the broadcast address and the word BROADCAST will disappear from the third line in Listing 22.1. This is not recommended because systems are expected to reply to network broadcasts. If you are concerned with someone outside trying to cause havoc by pinging your broadcast address, you don't need to worry, because most routers are designed to drop external traffic sent to broadcast addresses.

You can turn off the interface by using the following command:

```shell
ifconfig eth0 down
```

If you have built a kernel to support the ethertap device, feel free to experiment by configuring tap0. This makes an excellent way to test features on a host with no Ethernet device. The ethertap device can be configured almost any way you’d like. Before you start using the ethertap device, read /usr/src/linux/Documentation/networking/ethertap.txt.

## ROUTE

The second utility you’ll need to be able to network beyond the local systems is route. The route utility will enable you to specify a default gateway to the Internet. If your system is connected directly to the Internet through a modem, your system should have been automatically configured by your Internet provider. Otherwise, you’ll have to tell your system where the system (gateway) is that’s connected to the Internet.

Assuming your host has IP 192.168.0.2 and the system 192.168.0.1 is connected to the Internet, you’ll need to tell your host to use 192.168.0.1 as its gateway to the Internet. You can do this as follows:

```shell
route add default gateway 192.168.0.1
```

This command tells route to add 192.168.0.1 as the default to reach the Internet. Any packets that don’t have any other route to take to reach their destination will be passed to 192.168.0.1. If you look at the output of route with no options, you’ll see where all packets will route. Listing 22.2 shows the routes on the local system.

**LISTING 22.2 — OUTPUT FROM ROUTE**

Kernel IP routing table

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
|---|---|---|---|---|---|---|---|
| 192.168.0.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| 0.0.0.0 | 192.168.0.1 | 0.0.0.0 | UG | 1 | 0 | 0 | eth0 |

This listing shows that anything destined for a system on the network 192.168.0.0 (from 192.168.0.1 to 192.168.0.255) will be put on the local wire. Anything for 127.0.0.1–127.255.255.255 will go to localhost. Anything else (designated by 0.0.0.0) will go to 192.168.0.1 for further routing.

If you don’t want a system to be able to communicate with Internet hosts, you can delete the default route:

```shell
route del default
```

## Checking Your Network

If everything is working as it should, congratulations. If not, you’ll need to try to find out what is wrong. You have several utilities you can use to look over the network. This text will take a quick look at each of the following network utilities: ping, traceroute, netstat, and fuser. You’ll also become familiar with the files /etc/hosts, /etc/resolv.conf, and /etc/nsswitch.conf in the “Name Resolution” section at the end of the chapter.

Anytime you think you have a network problem, it is always easiest to take a methodical approach to the problem. Saying “I can’t surf to http://www.calderasystems.com/” covers a lot of territory. So starting with the local system and working out is preferred.

The first step is to use the ifconfig utility to see whether your device is configured. If it’s not configured, try to configure it. You can use the /etc/rc.d/init.d/network script, but configuring it by hand will provide you any error messages on the screen. If configuring it by hand fails, you might need to insert the proper driver using modprobe. You’ll also want to make sure you have your default route set up as shown previously.

### PING

After ifconfig says the device is configured, you can try to ping it, which sends an ICMP echo-request to the device. If the device has been enabled, it will respond with an ICMP echo-reply.

When you ping something, always try first by using the IP address:

```shell
ping 192.168.0.2
```

You can stop the ping by using Ctrl+c. If the ping fails, your card is not active. If the ping responds, stop it and try again by using your hostname, both the short name and the fully qualified name.

If you don’t receive replies when using the hostnames, you might want to skip to the section that discusses the host resolution after you verify that the host you’re pinging does in fact return pings (systems can be configured not to respond to ICMP ping packets by firewall software).

If everything works to this point, try to ping another host on your network by IP address:

```shell
ping 192.168.0.3
```

If that works and you can determine a good IP address on the Internet for a system you are sure is up and running, you can ping that. If that works, your basic networking is okay, and you’ll want to skip ahead to host resolution.

### TRACEROUTE

If you were able to ping hosts on your local network, but are unable to determine whether you’ve selected a good host on the Internet, you can switch to traceroute. The traceroute utility will show you the path packets take to reach a particular destination. The nice thing about traceroute is that even if the remote host is down, you’ll see the systems the packets will travel through between your system and where the network finally stops.

Again, you’ll want to choose a remote system so you can see where the packets are trying to go, and you’ll want to start with an IP address:

```shell
traceroute -n 209.127.112.153
```

If you see packets stop at your gateway, you know you have a problem with your gateway. If the packets travel beyond your gateway, the part of the network you have sway over is working, and you’ll just have to wait for other administrators to work on the rest.

The traceroute utility has a number of options that are beyond the scope of this book, but can enable you to determine what might be going wrong. One option you will want to use is the -n option, which tells traceroute to use the numeric designation of hosts rather than trying to resolve the names. This is just in case the problem lies in hostname resolution.

### NETSTAT

The netstat utility is also a multifaceted utility. Originally, if you wanted anything from routing information to open connections to servers bound to ports, you needed to use netstat. You still need to use netstat for most of those things, but routing information can now be obtained from route.

The netstat utility is more of a “now that things are running, what’s going on” kind of tool. It will show you what ports are connected to from where, and what ports are ready to accept connections. It will show you the state of connections. Many of the things it will show will probably be confusing, but many are also extraneous. Executing netstat with no options will show you the state of active network connections. By default, netstat resolves both hostnames and service names. If you don’t want names resolved but want to see numbers, use the -n option.

If you want to see all bound services, not just active connections, use the -a option. Adding the -v switch to netstat with or without the -a will show you which network protocols are not supported. The -r option will show you routing, and when combined with -e or -ee will provide some slightly different parameters. This text will not cover the routing support for netstat because route already provides that information.

Running netstat -avn will give you something like the output shown in Listing 22.3.

**LISTING 22.3 — netstat -avn**

Active Internet connections (servers and established)

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---|---|---|---|---|
| tcp | 0 | 0 | 0.0.0.0:1024 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:512 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:2049 | 0.0.0.0:* | LISTEN |
