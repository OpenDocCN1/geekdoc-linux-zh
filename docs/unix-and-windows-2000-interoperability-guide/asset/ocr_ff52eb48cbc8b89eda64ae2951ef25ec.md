# ARP

Here you see that all four cache entries are labeled *dynamic*: that is, they are acquired automatically, without user intervention. Dynamic entries last for a maximum of 10 minutes. You can see the expiration time of unreferenced entries by changing the value of the following Registry entries in

```
HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\ArpCacheLife\ArpCacheMinReferencedLife
```

Notice that the hardware addresses are given as six hexadecimal bytes separated by dashes. HP-UX requires the use of colons:

# 4.1.1.2 HP-UX

HP-UX also has the *arp -a* command, but the output is different.

```
# arp -a
houyhhnmm.book.local (10.0.0.3) at 0:8:0:a36:f7 ether
aix1.book.local (10.0.0.5) at 8:5a:d8:e1-a9 ether
```

Notice that HP-UX provides the host name as well as the IP address for each entry. Also, note that the hardware addresses are given as six hexadecimal bytes separated by colons. By default, dynamic ARP cache entries stay in the cache for five minutes. To change this parameter, use the *ndd -set /dev/arp arp_cleanup_interval* command, specifying the interval in milliseconds. For example, the first command will set the ARP cleanup interval to six minutes; the second will display the new value:

```
# ndd -set /dev/arp arp_cleanup_interval 360000
# ndd -get /dev/arp arp_cleanup_interval
```

# 4.1.2 Deleting ARP Cache Entries

# 4.1.2.1 Windows 2000

In Windows 2000, do *arp -a* to find the entry you want to delete and then supply only the IP address to the *arp -d* command. For example:

```
C:\arp -a
```

| Interface: 10.0.0.3 on Interface 0x2 Type |
| Internet Address Physical Address dynamic |
| 10.0.0.5 08-00-5a-d8-e1-a9 dynamic |
| 10.0.0.4 08-00-09-83-31-b dynamic |
| 10.0.10.1 00-60-b0-6a-8e-9c dynamic |

```
C:\arp -d 10.0.0.4
C:\>arp -a
```