
Next is paging activity. The first field ("re") shows the pages that were reclaimed. These pages made it to the free list but were later referenced and had to be salvaged.

Next you see the number of faults in three categories: interrupts per second, which usually come from hardware ("in"), system calls per second ("sy"), and context switches per second ("cs").

The final output is CPU usage percentage for user ("us"), system ("sy"), and idle ("id"). This is not as complete as the iostat output, which also shows nice entries.

If you are running an I/O-intensive workload, you may indeed see a lot of activity in runnable processes ("r"), blocked processes ("b"), and the runnable but swapped ("w") processes. If you have many runnable but swapped processes, then you probably have an I/O bottleneck.

## Network Statistics with netstat

netstat provides information related to network statistics. Because network bandwidth has as much to do with performance as the CPU and memory in some networks, you want to get an idea of the level of network traffic you have.

I use two forms of netstat to obtain network statistics. The first is netstat -i, which shows the state of interfaces that are autoconfigured. Although netstat -i gives a good rundown of the primary LAN interface, such as the network it is on, its name, and so on, it does not show useful statistical information.

The following shows the output of netstat -i:

```
# netstat -i
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Col
lan0 1497 151.150 a4410.e.h.c 242194 120 107665 23 19884
```

netstat provides a concise output. Put another way, most of what you get from netstat is useful. Here is a description of the nine fields in the netstat example:

- **Name**: The name of your network interface (Name), in this case, "lan0."
- **Mtu**: The "maximum transmission unit," which is the maximum packet size sent by the interface card.
- **Network**: The network address of the LAN to which the interface card is connected (151.150).
- **Address**: The host name of your system. This is the symbolic name of your system as it appears in the /etc/hosts file if your networking is configured to use /etc/hosts.

Below is the statistical information. Depending on the system you are using, or revision of OS, you may not see some of these commands:

- **Ipkts**: The number of packets received by the interface card, in this case, "lan0."
- **Ierrs**: The number of errors detected on incoming packets by the interface card.
- **Opkts**: The number of packets transmitted by the interface card.
- **Oerrs**: The number of errors detected during the transmission of packets by the interface card.
- **Col**: The number of collisions that resulted from packet traffic.

netstat provides cumulative data since the node was last powered up; therefore, you might have a long elapsed time over which data was accumulated. If you are interested in seeing useful statistical information, you can use netstat with different options. You can also specify an interval to report statistics. I usually ignore the first entry, because it shows all data since the system was last powered up. This means that the data includes non-prime hours when the system was idle. I prefer to view data at the time the system is working its hardest. The following examples show running netstat -l and specifying the lan interface for Solaris, HP-UX, and AIX. These outputs are nearly identical, although the name of the network interface does vary among UNIX variants. The netstat command is run at an interval of five seconds. The Linux version of this command, which is not shown, does not allow me to specify an interval.

### Solaris example

```
# netstat -I le0 5
```

| | input | | output | | | input (Total) | | output |
|---|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | cols | packets | errs | packets | errs | cols |
| (le0) | 18998 | 1189 | 1653100 | 118993180 | 0 | 3474777 | 1189 | 1663100 |
| 12: | 0 | | 0 | 185 | 0 | 1 | 0 | 0 |
| 13: | 0 | | 0 | 273 | 0 | 8 | 0 | 0 |
| 14: | 0 | | 0 | 153 | 0 | 3 | 0 | 0 |
| 15: | 0 | | 0 | 154 | 0 | 3 | 0 | 0 |
| 16: | 0 | | 0 | 124 | 0 | 3 | 0 | 0 |
| 17: | 0 | | 0 | 378 | 0 | 2 | 0 | 0 |
| 18: | 0 | | 0 | 389 | 0 | 4 | 0 | 0 |
| 19: | 0 | | 0 | 286 | 0 | 2 | 0 | 0 |

### HP-UX example (10.x)

```
# netstat -I lan0 5
```

| | output | | | | | (Total)-> input | | output |
|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | | packets | errs | packets | errs |
| (lan0)-> | 269841735 | 27 | 256627585 | 1 | 5092223 | 281472199 | 27 |
| 268258048 | 1 | 5092223 | 1602 | 0 | 1238 | 0 | 49 | 1673 | 0 | 1309 | 0 | 49 |
| | | | | | | 1223 | 0 | 1048 | 0 | 25 | 1235 | 0 | 1060 | 0 | 25 |
| | | | | | | 1516 | 0 | 1151 | 0 | 42 | 1560 | 0 | 1195 | 0 | 42 |
| | | | | | | 1553 | 0 | 1188 | 0 | 17 | 1565 | 0 | 1200 | 0 | 17 |
| | | | | | | 2539 | 0 | 2180 | 0 | 44 | 2628 | 0 | 2269 | 0 | 44 |
| | | | | | | 3000 | 0 | 2193 | 0 | 228 | 3000 | 0 | 2193 | 0 | 228 |
| | | | | | | 2959 | 0 | 2213 | 0 | 118 | 3003 | 0 | 2257 | 0 | 118 |
| | | | | | | 2423 | 0 | 1981 | 0 | 75 | 2435 | 0 | 1993 | 0 | 75 |

### AIX example

```
# netstat -I en0 5
```

| | input | | output | | | input | | output |
|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | cols | packets | errs | packets | errs | cols |
| (eno) | 0 | 1785925 | 0 | 0 | 0 | 47426087 | 0 | 2913405 | 0 | 0 |
| 46333531 | 0 | 1 | 0 | 0 | 0 | 204 | 0 | 2 | 0 | 0 |
| | | 203 | 0 | 1 | 0 | 0 | 298 | 0 | 1 | 0 | 0 |
| | | 288 | 0 | 1 | 0 | 0 | 204 | 0 | 12 | 0 | 0 |
| | | 293 | 0 | 1 | 0 | 0 | 191 | 0 | 1 | 0 | 0 |
| | | 191 | 0 | 1 | 0 | 0 | 191 | 0 | 1 | 0 | 0 |
| | | 150 | 0 | 3 | 0 | 0 | 151 | 0 | 3 | 0 | 0 |
| | | 207 | 0 | 3 | 0 | 0 | 218 | 0 | 15 | 0 | 0 |
| | | 162 | 0 | 3 | 0 | 0 | 162 | 0 | 3 | 0 | 0 |
| | | 120 | 0 | 2 | 0 | 0 | 120 | 0 | 2 | 0 | 0 |

With this example, you get multiple outputs of what is taking place on the LAN interface, including the totals on the right side of the output. As I mentioned earlier, you may want to ignore the first output, because it contains information over a long time period. This may include a time when your network was idle, and therefore the data may not be important to you.

You can specify the network interface on which you want statistics reported by using -I interface; in the case of the example, it was -I and either le0, lan0, or en0. An interval of five seconds was also used in this example.

Analyzing netstat statistical information is intuitive. You want to verify that the collisions (Colls) are much lower than the packets transmitted (Opkts). Collisions occur on output from your LAN interface. Every collision your LAN interface encounters slows down the network. You will get varying opinions about what is too many collisions. If your collisions have less than 5 percent of "Opkts," you're probably in good shape and better off spending your time analyzing some other system resource. If this number is high, you may want to consider segmenting your network in some way such as installing networking equipment between portions of the network that don't share a lot of data.

As a rule of thumb, if you reduce the number of packets you are receiving and transmitting ("Ipkts" and "Opkts"), then you will have less overall network traffic and fewer collisions. Keep this in mind as you plan your network or upgrades to your systems. You may want to have two LAN cards in systems that are in constant communication. That way, these systems have a "private" LAN over which to communicate and do not adversely affect the performance of other systems on the network. One LAN interface on each system is devoted to intrasystem communication. This provides a "tight" communication path among systems that usually act as servers. The second LAN interface is used to communicate with any systems that are usually clients on a larger network.

You can also obtain information related to routing with netstat (see Chapter 13). The -r option to netstat shows the routing tables, which you usually want to know about, and the -n option can be used to print network addresses as numbers rather than as names. In the following examples, netstat is issued with the -r option (this will be used when describing the netstat output) and the -rn options, so that you can compare the two outputs:
