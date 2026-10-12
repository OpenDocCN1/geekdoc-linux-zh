when using either Telnet or FTP to log in. The syntax for this file is first a keyword to identify what the file needs to do and then an IP address or domain, with each field separated by spaces. The file has four available fields in which you can enter variables.

The first field is *search*. The *search* field defines the domains that will be searched, in order, for a given host. Several internal processes, one of which is mail, use this option. This field tells the system the name to use to address the localhost when sending and receiving mail. The *domain* field identifies the host's local domain. If both the *domain* and *search* field appear in this file, then the last one is used. Red Hat Linux systems prefer the *search* option when setting up default *resolv.conf* files.

The next field is *nameserver*, which is similar to the *domain* field. This parameter may be the IP address of the local DNS server or it can include several name server addresses, both within and outside of the network. If this field lists multiple name servers, the system will query each in the order they are arranged. If the first does not respond, the next is then queried. Red Hat recognizes as many as three name servers.

The last field is *sortlist*. This feature enables you to sort the returned domain names in a specific order. If one class C domain should take preference over a related class B domain, then the class C is placed first on the list.

Here is a sample */etc/resolv.conf* file. In the *sortlist* field, the IP address is connected to the netmask using the typical *IP/netmask* syntax. As you can see, the classes correspond with their netmasks.

```
search astronomy.org nasa.gov
nameserver 10.10.10.254
nameserver 10.10.10.253
sortlist 10.10.10.0/255.255.255.0 10.1.0.0/255.255.0.0
```

# Configuring Hosts

The sixth variable used in networking that you need to be familiar with is */etc/host.conf*. This file lists the order in which the different name services will be searched when resolving hostnames. For example, if you wish to have your */etc/hosts* file looked at first before querying the name servers or DNS servers, you would place an order query on the first line followed by the command to resolve the hostnames, with the two elements separated by a comma. The line