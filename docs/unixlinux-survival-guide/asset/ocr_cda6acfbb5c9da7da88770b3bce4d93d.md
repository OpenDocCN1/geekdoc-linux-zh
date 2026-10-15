mail. If there are not that many failed attempts, this should not be a problem, though. This approach has another advantage: the list of failed logins will be not only on the machine, but also, provided one does not use an IMAP server, in the system administrator’s mailbox for safekeeping.

# 5.2.3 Files Common to All Systems on Your Network

The configuration files in use by a *NIX system come in variants. One variant is completely independent of the underlying operating system, for example, hosts; the second variant is used only on specific *NIX brands and might even differ between releases of the operating system. The maintenance of the configuration files can be time-consuming if the used systems deploy more files from the second variant.

The hosts file should be identical and current on all systems connected to the same network. It should contain all systems and the aliases used like loghost, if the log files should be stored on one specific server. Even if DNS (Domain Name System) is used for name resolution inside the network, if that DNS server should fail or needs to be shut down for some time, then all systems could use the hosts file for internal name resolution. The latter implies that the entry in nsswitch.conf uses the right order, hosts: files dns, and not the other way round. This file should be identical on all systems connected to the network, as well.

The hosts file contains the link between an IP address and a name for the system using the IP address. The system is not restricted to one name only, though. Listing 5.16 presents an entry.

# LISTING 5.16 An Entry in the hosts File

```
192.168.0.100    unixhost.example.domain unixhost mailserver
```

This entry allows the system using this file to draw the following conclusions: unixhost.example.domain, unixhost, and mailserver can be found by using the IP address 192.168.0.100. If a program or a process tries to find the system named mailserver, then the name can be resolved to 192.168.0.100. If the name cannot be found in the hosts file, then the configuration file nsswitch.conf is used to find other means to resolve the name, in that case sending a query to the IP address of the DNS server found in resolv.conf (see Listing 5.17).

# LISTING 5.17 The File resolv.conf

```
nameserver 192.168.0.200
domain example.domain
search example.domain
```