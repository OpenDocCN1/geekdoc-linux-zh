**TABLE 17.4 The journalctl matches parameter**

| Match | Description |
| :--- | :--- |
| *Fields* | Matches specific fields in the journal |
| *Kernel* | Only displays kernel journal entries |
| *PRIORITY=value* | Matches only entries with the specified priority |
| *_UID=user id* | Matches only entries made by the specified user ID |
| *_HOSTNAME=host* | Matches only entries from the specified host |
| *_TRANSPORT=trans* | Matches only entries received by the specified transport method |
| *_UDEV_SYSNAME=dev* | Matches only entries received from the specified device |
| *OBJECT_PID=pid* | Matches only entries made by the specified application process ID |

The `journalctl` command is great for when you are looking for specific event entries in the journal; it allows you to filter out events using the matches and determine how to display them using the options, as shown in Listing 17.3.

# **Listing 17.3: Output from the journalctl command**

```
`[rich@localhost ~]$ journalctl -r _TRANSPORT=kernel`  
`-- Logs begin at Fri 2019-02-08 12:47:04 EST, end at...`  
`Feb 08 12:48:36 localhost.localdomain kernel: TCP: lp registered`  
`Feb 08 12:48:17 localhost.localdomain kernel: fuse init (API version 7.22)`  
`Feb 08 12:47:43 localhost.localdomain kernel: virbr0: port 1(virbr0-nic)`  
`Feb 08 12:47:43 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_UP):`  
`Feb 08 12:47:43 localhost.localdomain kernel: virbr0: port 1(virbr0-nic)`  
`Feb 08 12:47:35 localhost.localdomain kernel: e1000: enp0s8 NIC Link is Up`  
`Feb 08 12:47:32 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_CHANGE)`  
`Feb 08 12:47:32 localhost.localdomain kernel: ip_set: protocol 6`  
`Feb 08 12:47:32 localhost.localdomain kernel: IPv6: ADDRCONF(NETDEV_UP)`  
`...
```

That makes digging through journal files much easier!  
Exercise 17.1 walks you through monitoring the system logs in real time and watching as you send a message to the logging facility on your Linux system.