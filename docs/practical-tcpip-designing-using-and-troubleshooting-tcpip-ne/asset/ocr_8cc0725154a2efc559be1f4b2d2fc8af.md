the cache for the time-to-live (TTL) duration returned in the DNS result, which is often 24 hours.

The trace below shows a **host** program lookup on Linux, showing that the TTL for hostname **badxxx** is 60 seconds. The hostname exists but the host doesn't, deliberately.

```
alice% host -v badxxx.example.com
Query about badxxx.example.com for record type A
Query done, 1 answer, authoritative status: no error
badxxx.example.com       60    IN    A     192.0.2.5
```

Now from a Windows PC, Dave, we try to view the shared resources on **badxxx**, using the command `**net view \badxxx**`. The trace for this is shown below, lines 1–11. We repeated the command after about 20 seconds; we see the DNS query is not repeated (lines 15–19). Finally, after about 80 seconds we tried again. This time (lines 23–29) the DNS lookup is issued, as expected, because we've exceeded the TTL and the entry has been removed from the cache.

The **ping** requests are generated automatically by the resolution system on Dave. (We've filtered out ARPs and several other packets where Dave unsuccessfully sends a NetBIOS query to **badxxx** for a list of its resources.)

| No. | Time | Source | Destination | Protocol | Info |
|-----|------|--------|-------------|----------|------|
| 1 | 0.00 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 2 | 0.74 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 3 | 1.49 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 6 | 2.24 | dave | carol | DNS | Standard query A badxxx.example.com | |
| 7 | 2.25 | carol | dave | DNS | Standard query response A 192.0.2.5 | |
| 10 | 2.25 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |
| 11 | 4.27 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |
| 15 | 23.7 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 16 | 24.4 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 17 | 25.2 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 18 | 25.9 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |
| 19 | 28.3 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |
| 23 | 79.2 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 24 | 79.9 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 25 | 80.7 | dave | 192.0.2.127 | NBNS | Name query NB BADXXX | |
| 26 | 81.4 | dave | carol | DNS | Standard query A badxxx.example.com | |
| 27 | 81.4 | carol | dave | DNS | Standard query response A 192.0.2.5 | |
| 28 | 81.4 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |
| 29 | 83.9 | dave | 192.0.2.5 | ICMP | Echo (ping) request | |

3. don't confuse this with the normal DNS lookup that Windows TCP/IP programs such as **ping** and **telnet** perform. Here we're talking about resolving (NetBIOS) names. Windows treats NetBIOS names and DNS names differently. (In practice you rarely have to worry about this distinction, but we explain it in more detail in Appendix 22.)