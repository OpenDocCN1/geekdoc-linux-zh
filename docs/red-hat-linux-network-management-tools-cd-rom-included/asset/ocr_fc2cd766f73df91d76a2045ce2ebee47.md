```
PING durer:
PING durer.home.com (10.0.2.10): 56 data bytes
64 bytes from 10.0.2.10: icmp_seq=0 ttl=28 time=0.9 ms
64 bytes from 10.0.2.10: icmp_seq=1 ttl=28 time=0.8 ms
64 bytes from 10.0.2.10: icmp_seq=2 ttl=28 time=0.8 ms
64 bytes from 10.0.2.10: icmp_seq=3 ttl=28 time=0.8 ms

--- durer.home.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.8/0.8/0.9 ms
```

In this case, **ping** displays no packet loss to *durér*, which happens to be a PostScript laser printer. This basically states that *durér* is alive and operating normally from an IP perspective. The default behavior of **ping** means that the user must type **Ctrl+c** to stop the output. This message generally means that the TCP/IP software is operational. Although *alive* indicates that the system is visible on the network, it no guarantee that other network services, such as FTP or Telnet, are available. This is an important distinction. The ping tool can only be used to determine basic protocol connectivity—not the availability of higher-level applications or services. In fact, some systems will answer a **ping** even before they are fully booted. Keep in mind that no single piece of software can determine that every TCP/IP application or service is installed and operating on a system.

If the host *durér* is not reachable, **ping** will display the following message after *A* is typed:

```
PING rubens.home.com (10.0.2.220): 56 data bytes
--- rubens.home.com ping statistics ---
2 packets transmitted, 0 packets received, 100% packet loss
```

Normally, **ping** issues ICMP requests forever and, if no reply is received, generates the message shown above only after the user has interrupted the command. This is somewhat unfortunate because other versions of **ping** will eventually timeout without the user having to manually interrupt the command. Luckily, a maximum number or count of the total number of requests can be specified, which has the effect of controlling **ping** so that the user doesn’t need to manually intervene. Using the **-c command-line option with an argument of 1, the** **ping** command will issue a single request to *rubens*: