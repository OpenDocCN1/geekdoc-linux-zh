# BEFORE DNS: THE /ETC/HOSTS FILE

Not all sites run DNS servers. Not all systems need DNS servers. In sufficiently small sites with no Internet connectivity, it's reasonable for each host to keep its own copy of the table matching all of the host names in the local network with their corresponding IP addresses. This table is stored in the /etc/hosts file.

> **TIP:** Even if hosts that have access to a DNS server, you may want to keep a hosts file locally, where a particular host can look up an IP address before going out to the DNS server. (Don't worry if the uses of this file aren't obvious at first. You'll find them over time—like me when I say they are widely varied.)

The /etc/hosts file keeps its information in a simple tabular format. The IP address is in the first column, and all the related host names are in the second column. Only white space separates the entries. Pound symbols (#) at the beginning of a line represent comments. Here's an example:

```
# Host table for Steve's internal network

127.0.0.1 local: local: localdomain # localhost
192.168.1.1 ford # Steve's Linux box (router)
192.168.1.2 oid # Linux kernel basking testbed
192.168.1.3 toybox # Heidi's Mac (MacOS/NeOS)
192.168.1.4 spacer # Steve's Solaris 7 Toy
192.168.1.5 tynmac # The portable
192.168.1.6 bsod # Win98 because SJSU requires it
```

In general, your /etc/hosts file cannot contain at the very least the necessary host-to-IP mappings to allow your system to boot up if the DNS server is not responding.

# Using NIS to Distribute the Hosts File

The /etc/hosts file is an excellent candidate for distribution via NIS (Network Information Service, which, simply put, is a mechanism by which you can keep a centralized database of tabular information. See Chapter 19.) Any UNIX host capable of connecting to and reading tables from an NIS server can of course use this information. The benefit to you is simple: You can maintain a centralized list of hosts that all workstations in your network can access. When you update the central list, all hosts on the network can see it. Some sites even prefer maintaining this hosts list via NIS instead of DNS, since NIS host tables are easier to manage.

If you do elect to take advantage of NIS distribution for your hosts file, it's very important that you still maintain the minimum number of entries in the locally managed /etc/hosts file. You always want your system to have what it needs to come up in the event it cannot contact the NIS server.