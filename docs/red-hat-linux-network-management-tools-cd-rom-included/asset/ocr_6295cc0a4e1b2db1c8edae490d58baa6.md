series of probe packets took 4.25 milliseconds (or .004 seconds), and the third series took 2.89 milliseconds (or .028 seconds).

The second line details the second routing hop and shows that **traceroute** reached the destination system *vermeer* with slower RTT times than the first (see Figure 4.4). When the second probe was sent, the router decremented the TTL, and then passed this packet to *vermeer*. Because the **traceroute** is attempting to access an unused port, *vermeer* responds with the PORT UNREACHABLE error. In fact, as a general rule on large (and sometimes small) internets, performance between systems and networks will and can vary a significant amount even from one moment to the next.

There is no restriction on what constitutes a destination; it can be any kind of device that ranges from a simple host system to an Internet router. The only requirement is that it must support IP.

# Reading traceroute Output

Due to variations and problems with router devices along certain paths, the general fluctuations of network routes can lead to unpredictable and strange **traceroute** output. As a result, certain codes might appear after the timing information is displayed. Table 4.16 lists these codes and their associated meanings.

Table 4.16 traceroute display codes
| Code | Meaning |
|:-----|:----------|
| * | No response to probe packets |
| ! | TTL in the received packet is set to 1 |
| !H | Destination host is unreachable |
| !N | Destination network is unreachable |
| !P | Destination protocol is unreachable |
| !S | The source route option has failed. In practice, this shouldn't happen, and if it does, it indicates a bug or problem with the router that generated the error |