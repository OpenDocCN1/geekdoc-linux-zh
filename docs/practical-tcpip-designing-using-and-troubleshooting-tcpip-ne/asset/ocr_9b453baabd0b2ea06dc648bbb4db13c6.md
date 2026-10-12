# ### 5.11 ICMP redirects implementations; automatic routing protocols

# **Linux route command and routing table flags**

The Linux manpage documents two flag types (in addition to the U, G, and H entries we saw in Module 5.2) that indicate whether the entry was created:

+   a. normally (manually, or via **iconfig** or the default gateway setting), or
+   b. automatically by some component of the system itself.

The flags are shown in Table 5.1. However, most current versions of Linux *don't* include the routes created by ICMP redirects in the default listing. The manpage is describing what happens on other versions of UNIX. To see these extra entries on Linux you have to use the command
```c
route -n -C
```
which displays the *routing table cache*. (But this doesn't display the D flag either.)

| Flag | If present | If absent |
| :--- | :--- | :--- |
| **D** | D**ynamic**: this entry was created automatically from an ICMP redirect or by a routing daemon (see below) | normal (manually configured) entry |
| **M** | **M**odified by an ICMP redirect or a routing daemon | normal (manually configured) entry |

Table 5.1 Two Linux manpage flags

# **ICMP redirect notes**

There are a few more features relating to ICMP redirects that you may need to know:

+   1. the RFCs say that routers may legitimately choose to ignore redirects. If Alice is configured as a router, what we described in the previous module may not work
+   2. Windows-NT doesn't show ICMP-created routes in its routing tables. There's no convenient way to display them
+   3. after ten minutes Windows-NT removes ICMP-created routes, so if this machine is still sending to that destination, the ICMP redirect procedure will be repeated every ten minutes
+   4. when a Linux host (Alice) receives an ICMP redirect to use a router (Rupert), if Alice doesn't have Rupert already in her ARP cache she won't successfully create the route until she receives the same ICMP redirect a second time. (This doesn't make much difference to the efficiency of the network, but it does clutter the **tcpdump** traces when you're trying to see what's happening.)

# **Automatic routing protocols – RIP, OSPF, BGP**

(Strictly this doesn't belong here, but it explains what a routing daemon is and how you could get **M**– or **D**–flagged entries in your routing tables.)