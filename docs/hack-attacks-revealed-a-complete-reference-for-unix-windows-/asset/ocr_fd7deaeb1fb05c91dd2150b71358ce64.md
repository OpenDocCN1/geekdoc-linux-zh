| | sgnp | 705 | acctinfo |
|---|---|---|---|
| 161 | snmp | 706 | acctslave2 |
| 162 | snmp-trap | 707 | acctdisk |
| 315 | load | 750 | kerberos |
| 500 | sytek | 751 | kerberos_mast |
| 512 | biff | 752 | passwd_server |
| 513 | who | 753 | userreg_serve |

# Port: 7

Service: echo

**Hacker's Strategy**: This port is associated with a module in communications or a signal transmitted (echoed) back to the sender that is distinct from the original signal. Echoing a message back to the main computer can help test network connections. The primary message-generation utility executed is termed PING, which is an acronym for Packet Internet Groping. The crucial issue with port 7’s echo service pertains to systems that attempt to process oversized packets. One variation of a susceptible echo overload is performed by sending a fragmented packet larger than 65,536 bytes in length, causing the system to process the packet incorrectly, resulting in a potential system halt or reboot. This problem is commonly referred to as the “Ping of Death” attack. Another common deviant to port 7 is known as “Ping Flooding”. It, too, takes advantage of the computer’s responsiveness, using a continual bombardment of pings or ICMP Echo Requests to overload and congest system resources and network segments. (Later in the book, we will cover these techniques and associated software in detail.) An illustration of an ICMP Echo Request is shown in Figure 4.1.

```
```
C:\>ping TigerTools.net

Pinging TigerTools.net [207.155.252.91] with 32 bytes of data:

Reply from 207.155.252.9: bytes=32 time=176ms TTL=245
Reply from 207.155.252.9: bytes=32 time=176ms TTL=245
Reply from 207.155.252.9: bytes=32 time=176ms TTL=245
Reply from 207.155.252.9: bytes=32 time=176ms TTL=245

Ping statistics for 207.155.252.9:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
    Approximate round trip times in milli-seconds:
    Minimum = 113ms, Maximum = 176ms, Average = 135ms
```
```

![](bbox=[0.12, 0.82, 0.45, 0.84])

# Port: 11

Service: systat