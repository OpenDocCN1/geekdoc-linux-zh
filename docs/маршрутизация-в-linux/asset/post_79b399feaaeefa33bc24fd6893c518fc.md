
destination. The destination is followed by the port number (telnet here) xxxx, followed by the window size. The (DF) signifies that the do not fragment bit is set, so routers between the source and destination should not fragment the IP datagram into smaller frames during transmission.

## -n

Like the arp -n parameter, tcpdump also uses the -n to not perform name resolution on the names. Generally, -n should be used because using name resolution creates an additional load on the node and network as tcpdump tries to resolve IP addresses it is examining. Here is an example of using -i with the -n parameter.

```
[root@lefty /root]# tcpdump -i eth0 -n
Kernel filter, protocol ALL, datagram packet socket
tcpdump: listening on eth0
11:22:52.793192 > 192.168.1.101.1041 > 192.168.1.254.telnet: . 3786648:3768648(0) ack 257256729 win 7766 (DF)
11:22:52.793231 > 192.168.1.254.telnet > 192.168.1.101.1041: P 1:82(81) ack 0 win 32120 (DF)
11:22:52.939102 < 192.168.1.101.1041 > 192.168.1.254.telnet: . 0:0(0) ack 82 win 32120 (DF)
11:22:52.939142 > 192.168.1.254.telnet > 192.168.1.101.1041: P 82:288(206) ack 0 win 32120 (DF)
11:22:53.138977 < 192.168.1.101.1041 > 192.168.1.254.telnet: . 0:0(0) ack 288 win 7479 (DF)
11:22:53.139013 > 192.168.1.254.telnet > 192.168.1.101.1041: P 288:477(189) ack 0 win 32120 (DF)
6 packets received by filter
```

## -q

-q, or quiet mode, tells tcpdump to just print the Layer 4 (tcp, udp, or ICMP) protocol and port number or name. Here is a tcp (telnet) example:

```
[root@lefty /root]# tcpdump -i eth0 -nq
Kernel filter, protocol ALL, datagram packet socket
tcpdump: listening on eth0
11:26:39.114679 < 192.168.1.101.1041 > 192.168.1.254.telnet: tcp 0 (DF)
11:26:39.114780 > 192.168.1.254.telnet > 192.168.1.101.1041: tcp 81 (DF)
11:26:39.314634 < 192.168.1.101.1041 > 192.168.1.254.telnet: tcp 0 (DF)
11:26:39.314674 > 192.168.1.254.telnet > 192.168.1.101.1041: tcp 147 (DF)
4 packets received by filter
```

And here is an ICMP (ping) example using the -q in addition to other parameters:

```
[root@lefty /root]# tcpdump -i eth0 -nq
Kernel filter, protocol ALL, datagram packet socket
tcpdump: listening on eth0
11:27:59.459664 < 192.168.1.101 > 192.168.1.254: icmp: echo request
11:27:59.459708 > 192.168.1.254 > 192.168.1.101: icmp: echo reply
2 packets received by filter
```

## -t

The -t parameter instructs tcpdump to not print the timestamp on its output.

## -x

The -x parameter will cause tcpdump to print the packets out in hexadecimal.

## -w Filename

When a tcpdump output needs to be saved, the -w can be used to save the file in libpcap format, which saves space, as well as put the file in a format that can be read by many other network analyzers. The files created by tcpdump can grow quickly, so disk space should be monitored closely when saving the file.

## -r Filename

Files created with the -w option can be read by tcpdump, and further analysis can be performed on the packet. If the original tcpdump was a tcpdump -w with no filters, then the tcpdump -r can use filters to refine the output to exactly what is needed:

```
tcpdump -r savedfile -n host 192.168.1.101
11:39:52.498409 eth0 > 192.168.1.101.1041 > 192.168.1.254.telnet: . 3768803:3768803(0) ack 2572567146 win 7781 (DF)
11:39:52.498518 eth0 > 192.168.1.254.telnet > 192.168.1.101.1041: P 1:89(88) ack 0 win 32120 (DF)
11:39:52.698395 eth0 > 192.168.1.101.1041 > 192.168.1.254.telnet: . 0:0(0) ack 89 win 7689 (DF)
```

## -v

The -v (for verbose) tells tcpdump to print the time-to-live information as well as the type of service. Notice the difference between the output that follows with the -v parameter and the same command without the -v in the -r example given;

```
[root@lefty /root]# tcpdump -r savedfile -n -v host 192.168.1.101
11:39:52.498409 eth0 > 192.168.1.101.1041 > 192.168.1.254.telnet: . 3768803:3768803(0) ack 2572567146 win 7781 (DF) (ttl 128, id 37383)
11:39:52.498518 eth0 > 192.168.1.254.telnet > 192.168.1.101.1041: P 1:89(88) ack 0 win 32120 (DF) (ttl 64, id 21483)
11:39:52.698395 eth0 > 192.168.1.101.1041 > 192.168.1.254.telnet: . 0:0(0) ack 89 win 7689 (DF) (ttl 128, id 37639)
```

## tcpdump Expressions

tcpdump uses the concept of expressions to define which packets to display. The expression follows any command-line parameters that are passed to tcpdump. An expression is made up of a qualifier followed by an ID.
