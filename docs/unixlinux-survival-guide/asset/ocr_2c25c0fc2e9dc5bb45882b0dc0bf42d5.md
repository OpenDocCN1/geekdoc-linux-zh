# SCAN nmap XMAS 1 sources 1 destinations

Priority: 2 Classification: Attempted Information Leak

[sid:1228] [arachNIDS:30]

# Sources triggering this attack signature

| Source | # Alerts (sig) | # Alerts (total) | # Dsts (sig) | # Dsts (total) |
| 192.168.0.3 | 60 | 62 | 1 | 1 |

# Destinations receiving this attack signature

| Destinations | # Alerts (sig) | # Alerts (total) | # Srcs (sig) | # Srcs (total) |
| 192.168.0.5 | 60 | 62 | 1 | 1 |

# FIGURE 7.2 Alarm details.

3 different signatures are present for 192.168.0.3 as a source

+   - 1 instances of ICMP PING
+   - 1 instances of ICMP PING NMAP
+   - 60 instances of SCAN nmap XMAS

There are 1 distinct destination IPs in the alerts of the type on this page.

| WhoIs lookup at: | ARIN | RIPE | APNIC | Geektools |
| 192.168.0.3 DNS lookup at: | Amenesi | TRIUMF | Princeton |
| More lookup info | ... | ... |

```
[**] [1:469:3] ICMP PING NMAP [**]
[Classification: Attempted Information Leak] [Priority: 2]
09/16-16:51:05.190140 192.168.0.3 -> 192.168.0.5
ICMP TTL:47 TOS:0x00 ID:30504 IpLen:20 DgmLen:28
Type:8 Code:0 ID:6158 Seq:1 MDM
[xref => http://www.whitehats.com/info/ids162]
```

```
[**] [1:384:5] ICMP PING [**]
[Classification: Misc activity] [Priority: 3]
```

# FIGURE 7.3 Details of an IP address.