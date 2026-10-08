
## CHAPTER 13 Testing and Reporting

Similar commands should work with the port number for most standard services. For example, if you run the `telnet your_mail_server.com 25` command (substitute the name of the target e-mail server for your_mail_server.com) and get a Connection refused message, there may be a bad port number or perhaps a firewall that's blocking the connection to that out-server. If there's no response at all, the telnet command is likely getting through to the target server, but not getting a response. That suggests nothing is listening on port 25. One of the limitations of telnet is that it can only connect to systems that use TCP ports. Later in this chapter, you'll look at the `nc` command, which can connect to systems that use TCP and UDP ports.

If some server is listening on port 25, you'll see it in the output of a netstat command with appropriate switches. It can also work with systems that communicate on both TCP and UDP ports.

### The netstat Command

The netstat command is a powerful tool. With a variety of switches, it can help you get into and better understand the networking system. Knowledgeable Linux users should already know that the `netstat -r` command displays the routing table that applies to the current system. With the `-n` switch, the netstat command works in numeric format: it does not require access to Domain Name Service (DNS) or the `/etc/services` files.

The netstat command can tell you. The `-t` switch specifies TCP ports. The `-u` switch specifies UDP ports. With the help of the `-a` switch, netstat can tell you all connections on the local system. So put those switches together. Figure 13-2 displays the start of the output to the `netstat -at` command.

Active Internet connections (servers and established)

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 1 | 127.0.0.1:2288 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:902 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:742 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:139 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 1 | 127.0.0.1:5980 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 127.0.0.1:5901 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 127.0.0.1:5902 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:111 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 1 | 127.0.0.1:30003 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 192.168.122.1:533 | 0.0.0.0:* | LISTEN |

FIGURE 13-2

Identify what your system listens to with netstat -at.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_410_0.png)

### TABLE 13-1 Output from netstat -atun

| COLUMN | DESCRIPTION |
| --- | --- |
| Proto | Protocol, typically TCP or UDP. On some systems, protocols associated with with IPv6 communication may be shown as TCP6 and UDP6. |
| Recv-Q | Received communication in the queue, in bytes, usually 0. |
| Send-Q | Transmitted communication in the queue that is not yet acknowledged, in bytes, usually 0. |
| Local Address | Local IP address and port number. See explanation that follows for more information. |
| Foreign Address | Remote IP address and port number. Unless there's an established connection, it's normally set to IPv4 address and port number 0.0.0.0:*, which is listening for connections from any IPv4 address. It may also be set to IPv6 address and port number ::*. See explanation that follows for more information. |
| State | Connection state, normally LISTEN or ESTABLISHED. A network service that is in the LISTEN state has not made a connection. |

> TIP
IPv4 address 0.0.0.0 is known as the default address, a placeholder for any address.

This is a lot of output, indicative of a system that's probably listening for too many connections. The output is described in Table 13-1, with columns listed from left to right. To see the actual column headers, you'll have to pipe the output to the `less` command pager. Alternatively, if a bastion host is configured on the local system, you'll see a list of such listen connections be seen in a normal output, and you'll see an example of such later in this section.

With Table 13-1 in mind, take another look at the output from netstat -at command shown in Figure 13-2. Take the first couple of lines of output, one at a time:

The first line is a TCP connection associated with port 2208, listening for requests from systems with any IP address (0.0.0.0). An Internet search might send you into a panic, as there are entries that suggest that port is a common backdoor for black-hat hackers. But it is also used by the Hewlett-Packard Linux Imaging and Printing Project, and may be necessary for communication with such printers. In addition, since the local address is set to the loopback address of 127.0.0.1, the system might be listening just to the loopback adapter.

```
tcp 0 127.0.0.1:2208 0.0.0.0:* LISTEN
```

To confirm, you can run the variation on the telnet command described earlier, as it would apply to port 2208:

```
$ telnet localhost 2208
```

As the localaddress is normally associated with 127.0.0.1 in the `/etc/hosts` file, that connection should work. Try it with the IP address of the local address. If the netstat status is true, the connection should be refused. The same command, when run from a remote system, may lead to a message that suggests the connection was refused, typical of an iptables-based firewall.

Now take the second line of output, which listens for TCP traffic on port 902:

```
tcp 0 0 0.0.0.0:902 0.0.0.0:* LISTEN
```

In this case, the `/etc/services` file is a bit misleading because port 902 is the standard for systems that are controlled over a network. That's confirmed by the output to `telnet remote_ip_address 902` command, as shown here:

The number of lines in Figure 13-2 goes on for some As suggested by quantity of output, the associated system is potentially not secure. In contrast, take a look at Figure 13-3, where the `netstat -ant` command is applied to a more secure system. The displayed output is easier to explain. The first line, which specifies port 22, is associated with SSH server. The second line, associated with the localhost address and port 25, illustrates as a Mail Transfer Protocol (SMTP) server as Postfix or sendmail that is yet listening to anything.

Take a closer look at the third line, with associated with ESTABLISHED connection:

```
tcp 0 0 192.168.1.22:1922 192.168.1.22:5612 ESTABLISHED
```

It's a TCP connection on port 22, from the noted 192.168.1.22:1. The next two lines are associated with TCP6 over IPv6, as symbolized by the `tcp6` line. They's IPv6 status corresponds to the first two lines.

Active connections (servers and established)

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 0.0.0.0:22 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 127.0.0.1:25 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 192.168.1.22:1922 | 192.168.1.22:5612 | ESTABLISHED |
| tcp6 | 0 | 0 | *:22 | *:* | LISTEN |
| tcp6 | 0 | 0 | *:25 | *:* | LISTEN |
| udp | 0 | 0 | 0.0.0.0:* | 0.0.0.0:* | LISTEN |

![](img/c0608a8c8a0777903dfec4ff61fdffa1_412_0.png)

### PART 3 | Building a Layered Security Strategy

The final lines use one UDP port 68, normally associated with the Bootstrap Protocol (BOOT). If this system can get IP address from the local system or does not need to use Dynamic Host Configuration Protocol (DHCP), you may want to disable or uninstall associated software. Now take a command with the `-p` switch to identify the process in question, which confirms the association between that port and the DHCP client.

### The lsof command

While lsof lists open files, one can focus on network-related processes with the `-i` switch. Add the `-n` to get IP addresses in numeric format, and you can quickly get a view of network-related processes on the local system: If you've got a lot of active services, the output could be substantial. One example is shown in Figure 13-4. Compare the output to the `netstat` command described. Not only does `-ni` organize connections by service, but it also includes process identifier (PID).

| PID | USER | FD | TYPE | DEVICE | SIZE | NAME |
| --- | --- | --- | --- | --- | --- | --- |
| 3037 | michael | 3u | IPv4 | | | 10.168.0.2:3627->10.168.0.6:50 (ESTABLISHED) |
| 5144 | root | 6u | IPv4 | | | 17517 127.0.0.1:80 (LISTEN) |
| 5144 | root | 6u | IPv4 | | | 17509 10.0.0.1:80 (LISTEN) |
| 5144 | root | 6u | IPv6 | | | [fe80::27ff:17ff:fe6b:f6b0]:80 (LISTEN) |
| 5163 | daemon | 4u | IPv4 | | | 13324 *:nnprc (LISTEN) |
| 5163 | daemon | 5u | IPv4 | | | 13326 *:sunprc (LISTEN) |
| 5163 | map | 4u | IPv4 | | | 13294 *:1024 |
| 5182 | rpc.stat | 5u | IPv4 | | | 13332 *:9664 |
| 5182 | rpc.stat | 5u | IPv6 | | | 13334 *:4267 (LISTEN) |
| 5896 | avahi-dae | 8u | IPv4 | | | 14154 *:mdns |
| 5896 | avahi-dae | 8u | IPv4 | | | 14155 *:4313 |
| 6987 | mysqld | 6u | IPv6 | | | 14452 127.0.0.1:3306 (LISTEN) |
| 6204 | cuspsd | 2u | IPv4 | | | 14532 *:LISTEN (LISTEN) |
| 6204 | cuspsd | 6u | IPv4 | | | 14533 *:LISTEN (LISTEN) |
| 6254 | cuspsd | 6u | IPv4 | | | 14536 *:udp |
| 6254 | hddtemp | 6u | IPv4 | | | 14572 127.0.0.1:7634 (LISTEN) |
| 6470 | master | 6u | IPv4 | | | 14952 *:ntmp (LISTEN) |
| 6472 | root | 7u | IPv4 | | | 14953 *:netbios-ns |
| 6472 | root | 7u | IPv4 | | | 15110 *:netbios-dm |
| 6472 | root | 15u | IPv4 | | | 21862 100.168.1.105:137-netbios-ns |
| 6472 | root | 16u | IPv4 | | | 21863 100.168.1.105:138-netbios-dm |
| 6474 | root | 6u | IPv4 | | | 15139 *:microsoft-ds |
| 6474 | smbd | 20u | IPv4 | | | 15148 *:netbios-ssn (LISTEN) |
| 6655 | xinetd | 5u | IPv4 | | | 15340 *:fwmare-auth (LISTEN) |
| 6655 | xinetd | 6u | IPv4 | | | 15341 *:swat (LISTEN) |
| 6655 | xinetd | 6u | IPv4 | | | 15342 *:kernel (LISTEN) |
| 6655 | xinetd | 10u | IPv4 | | | 15344 *:eklogin (LISTEN) |
| 6737 | asterisk | 7u | IPv4 | | | 15443 127.0.0.1:5080 (LISTEN) |

FIGURE 13-4

The lsof -ni command connections on a multipurpose service:
