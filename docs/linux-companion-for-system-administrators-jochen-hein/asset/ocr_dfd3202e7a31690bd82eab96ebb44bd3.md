# THE netstat PROGRAM 393

| Flag | Description |
| --- | --- |
| A | The interface receives all multicast addresses |
| B | Broadcasts are allowed |
| D | Debugging is on |
| L | This is a loopback interface |
| M | All packets are received (promiscuous mode) |
| N | No trails are generated |
| O | This interface does not use ARP |
| P | The interface is a point-to-point connection |
| R | The interface is running |
| U | The interface is up |

Table 13.4 Flags in netstat -i.

+   - -c regenerates the requested list each second, so that changes can be detected. The program must be terminated with Ctrl-C.
- -n prevents the output of host name and service, so only the numerical values are displayed. Thus, the ‘reverse lookup’ in the name server is omitted, which may lead to long timeouts and increases network load.
- -o displays the timer status.

+   - Under UNIX, -r is equivalent to route, the kernel routing tables are displayed. Under other UNIX systems, where route cannot be used to display the routing tables of the kernel, you must always use netstat -r.
- -t displays information on TCP sockets.
- -u displays information on UDP sockets.
- -w displays information on RAW sockets.
- -x displays information on UNIX sockets.

As long as your computer is not networked, you can shut down your computer without problems. If a serial terminal is connected to your computer, you should verify before each shutdown, for example by means of w and ps aux, whether a user is active on that terminal. If however, your computer is employed as a network server, you must also consider other network connections. All active connections can be displayed via netstat -a.