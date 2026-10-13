# TRACEROUTE

If you were able to ping hosts on your local network, but are unable to determine whether you’ve selected a good host on the Internet, you can switch to traceroute. The traceroute utility will show you the path packets take to reach a particular destination. The nice thing about traceroute is that even if the remote host is down, you’ll see the systems the packets will travel through between your system and where the network finally stops.

Again, you’ll want to choose a remote system so you can see where the packets are trying to go, and you’ll want to start with an IP address:

```
traceroute -n 209.127.112.153
```

If you see packets stop at your gateway, you know you have a problem with your gateway. If the packets travel beyond your gateway, the part of the network you have sway over is working, and you’ll just have to wait for other administrators to work on the rest.

The traceroute utility has a number of options that are beyond the scope of this book, but can enable you to determine what might be going wrong. One option you will want to use is the -n option, which tells traceroute to use the numeric designation of hosts rather than trying to resolve the names. This is just in case the problem lies in hostname resolution.

# NETSTAT

The netstat utility is also a multifaceted utility. Originally, if you wanted anything from routing information to open connections to servers bound to ports, you needed to use netstat. You still need to use netstat for most of those things, but routing information can now be obtained from route.

The netstat utility is more of a “now that things are running, what’s going on” kind of tool. It will show you what ports are connected to from where, and what ports are ready to accept connections. It will show you the state of connections. Many of the things it will show will probably be confusing, but many are also extraneous. Executing netstat with no options will show you the state of active network connections. By default, netstat resolves both hostnames and service names. If you don’t want names resolved but want to see numbers, use the -n option.

If you want to see all bound services, not just active connections, use the -a option. Adding the -v switch to netstat with or without the -a will show you which network protocols are not supported. The -r option will show you routing, and when combined with -e or -ee will provide some slightly different parameters. This text will not cover the routing support for netstat because route already provides that information.

Running netstat -avn will give you something like the output shown in Listing 22.3.

```
LISTING 22.3  netstat -avn

Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:1024            0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:512             0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:2049            0.0.0.0:*               LISTEN
```