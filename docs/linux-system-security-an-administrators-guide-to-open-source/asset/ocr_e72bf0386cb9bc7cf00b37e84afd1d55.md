# **Table 16.2** Options to **ipchains** (Continued)

|
|-|
| **Option** | **Description** |
|-|
| -l or<br>   --log | Causes packets matching the rule to<br>be logged via **klogd** to selector **kern.info**.<br>Very useful option for initial setup and<br>debugging. Be careful with this option,<br>however, as it logs *every* packet that<br>matches. |
|-|
| -n or<br>   --numeric | When listing rules, suppresses name<br>translation. Ordinarily, **ipchains** will<br>attempt to convert IP addresses to<br>hostnames, port numbers to services, etc. |
|-|
| -P [!] *protocol*<br>   may be used instead of **-p** | Specifies the protocol for the rule, which may<br>be any name or number listed in */etc/*<br>*/protocols*, such as **tcp**, **udp**, or **ip**. The<br>keyword **all**, meaning all protocols, may<br>also be used. It is the default. The **all**<br>protocol may not be used with -C.<br>A preceding ! reverses the meaning. |
|-|
| -s [!] *address*/***mask* [!] [*port*:***port*]<br>   --source may be used instead of **-s** | Identical to **-d** except that this is the source<br>address. Also, unlike **-d**, ICMP type numbers<br>may be specified in lieu of ports. |
|-|
| --sport [!] [*port*:***port*]<br>   --source-port may be used instead of<br>   --sport | Allows for the separate specification of a<br>source port or port range. |
|-|
| -v or<br>   --verbose | When listing rules, this option adds<br>additional information including, but not<br>limited to, the interface address, rule<br>options, and packet and byte counters. |
|-|
| -x or<br>   --exact | Displays the exact packet and byte counts.<br>Ordinarily, **ipchains** rounds to the nearest<br>1000 (**k**), 1,000,000 (**M**), or multiples of 1000**M**<br>(**G**). |
|-|
| [!] -y or<br>   --syn | Only matches TCP packets that have the<br>SYN bit set and the ACK and FIN bits<br>cleared. Such a TCP packet represents a<br>connection attempt. The ! negates the<br>meaning; that is, it will match return<br>packets for an existing connection. Read<br>through *Rules for Allowing* ***tcp*** *from the*<br>*Internal Network* *to the Internet* on page 474<br>and, in particular, *FTP Rule 3* on page 476<br>for more details about this option. |
|-|
| --line-numbers | Available with **ipchains** Version 1.3.9 and<br>later. Lists the number of each rule. Must be<br>used with **-L**. |