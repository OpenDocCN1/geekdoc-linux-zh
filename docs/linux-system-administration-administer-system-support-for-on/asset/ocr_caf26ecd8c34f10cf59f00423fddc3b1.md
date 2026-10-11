add 100 more user accounts, the ISP can set up another Linux host for user
accounts without affecting the performance of the payroll software.

# Specific Servers

Because Linux can scale, and as your system administration tasks may grow, you

may separate out specific tasks to one computer. Machines could have a dedicated

purpose like a Web server, a mail server, a print server, or even a X server.

In an environment dependent on a large amount of daily e-mail, a Linux host

 can be used specifically as a mail server. This capability enables one host to handle

 the e-mail load without having to worry about heavy traffic from database access

 as well. Two resource-intensive application servers, such as e-mail and Web, can be

 on the same computer. However, this can severely hurt performance on one if not

 both applications.

As an X server, Linux can be powerful in a heterogeneous environment – for

 example, serving Windows 95 Xterminal-emulation software. A Linux X server

 can take client requests from Windows 95 hosts, other Linux hosts, and any other

 operating system with X emulator.

Since Linux can also be used as a print server, you may not want any other ser-

vices running on it. As a print server, Linux can send print requests to network

 printers using TCP/IP. You can also configure Samba so you can send print jobs to

 network printers from a Windows95 or NT workstation.

# Network Architecture

As with other UNIX operating systems, Linux is designed to work on a network –

 specifically, with the IP networking implementation native to Linux, using various

 servers such as X and e-mail. Even so, network architecture can affect the per-

 formance of any operating system; Linux is no exception.

To get from one network to another, the connection has to go through one hop.

 Sometimes it takes multiple hops to get from one network to another. Take a look at

 this tracertoute from shell113.ba.best.com, a host in Mountain View, California;

 to grove.ufl.edu, a host at the University of Florida in Gainesville.

```
1 core1-fe8-1-0.mv.best.net (206.184.139.129) 0.898 ms 0.630 ms 0.449 ms

 2 hss14-0-0.GW1.SCLI.ALTER.NET (137.39.133.89) 2.151 ms 1.156 ms 1.117 ms

 3 103.ATM2-0.XR2.SCLI.ALTER.NET (146.188.145.126) 1.881 ms 2.796 ms 7.516 ms

 4 194.ATM3-0.TR2.SCLI.ALTER.NET (146.188.146.22) 2.346 ms 1.497 ms 1.755 ms

 5 107.ATM8-0-0.TR2.ATLI.ALTER.NET (146.188.136.69) 72.851 ms 73.113 ms

 72.697 ms

 6 100.ATM4-0-0.XR2.ATLI.ALTER.NET (146.188.232.97) 74.769 ms 73.088 ms

 72.608 ms
```