# ## 2.5 Viewing and manipulating ARP entries

TCP/IP keeps a record of (IP address, MAC address) pairs in its *ARP cache*. It is only a cache and not a permanent store: once an entry reaches a certain age, TCP/IP deletes it. This stops the cache growing forever, and gets over the problem of how to detect whether the MAC address changes for a given IP address (e.g. if you have to replace a broken network card). On the other hand, it means the ARP dialog is repeated every so often, getting the same answer each time. (However, the load this imposes on the network is negligible.)

The arp command lets you view and manipulate the ARP cache (see Table 2.1).

# Table 2.1

| | Linux | Windows-NT |
|---|---|---|
| view the cache | arp<br>arp *host*<br>arp -a<br>arp -a *host* | arp -a<br>arp -a *ipnum* |
| **show addresses as numbers instead of names** | ... -n ... | |
| **delete an entry** | arp -d *host* | **arp -d *ipnum*** |
| **add ("set") an entry** | **arp -s *host macaddr*** | **arp -s *ipnum macaddr*** |

# **Notes:**

+   1.  on Linux, arp by default prints host addresses as names and numbers ("**arp -a**") or just names ("**arp**"). As usual this works correctly only if you have DNS configured, which we don't cover until Chapter 7. Use option "-n" to prevent arp trying to convert the IP numbers to names
+   2.  on Linux, the "-a" format display (Figure 2.8a) is slightly different to the one without "-a". We always use "-a", because it works on both Linux (Figure 2.8b) and NT (Figure 2.8c)
+   3.  on Linux, *host* can be either an IP number or a hostname; on Windows you can use only IP numbers. See your manpages for more detailed descriptions
+   4.  we've never needed to add entries, so you're unlikely to need to use "**arp -s**"
+   5.  On Windows-NT, by default entries are deleted from the ARP cache after two minutes if they are not used, or ten minutes if they are used; the timeout period can be edited in the Registry, although it's hard to see why you would ever want to do that. On Linux, entries are usually deleted after about five minutes. (You can check the details of your implementation by ensuring an entry for a machine is present by pinging it, then running "**arp -a**" at intervals, to see when the entry vanishes.)