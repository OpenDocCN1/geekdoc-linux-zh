
a new network. For connecting to an existing network, contact your systems administrator for the information. Getting a network connected to the Internet is beyond the scope of this book, and we recommend the following starting point:

*TCP/IP Network Administration, 2nd Edition, by Craig Hunt (O'Reilly and Associates).*

If you're setting up a private network that won't ever be connected to the Internet, then you can choose any primary name + domain name you would like and have several choices for IP addresses (See Figure 8-22).

| Addresses available | Examples |
|---|---|
| 10.0.0.0 - 10.255.255.255 | 10.5.12.14 |
| 172.16.0.0 - 172.31.255.255 | 172.16.9.1, 172.28.2.5 |
| 192.168.0.0 - 192.168.255.255 | 192.168.0.13 |

## Figure 8-22: Private Address Ranges

The three sets of numbers above correspond to class a, b, and c networks respectively. The classes are used to describe the number of IP addresses available as well as the range of numbers used to described each. The numbers above have been set aside for private networks.

**Please Note:** You should not use these IP addresses if you connect to the Internet since 192.168.0.* and 192.168.255.* are not reliably considered private. If you want your network to be connected to the Internet, or think you might want to at some point in the future, do yourself a favor and get yourself non-private addresses now.

## Nameserver Specification

A nameserver and default domain are also needed to establish a network connection. The nameserver is used to translate host names such as private.network.com to their corresponding IP address such as 192.168.7.3. The default domain tells the computer where to look if a fully qualified hostname isn't specified. Fully qualified means that the

full address is given, so foo.redhat.com is the fully qualified hostname, while the hostname is simply foo. If you specified your default domain as redhat.com, then you could use just the hostname to connect successfully. For example ftp foo would be sufficient if your search domain is redhat.com, while ftp foo.redhat.com would be required if it wasn’t. To specify the nameserver, open

```
[Config] -> [Networking] -> [Name server specification (DNS)]
```

![](img/46f4935125ba89e12897afbe9d77a097_217_0.png)

## Figure 8-23: Resolver Configuration Screen

Nameservers are ranked according to the order in which they are accessed, so it’s not unusual to see nameservers referred to as primary, secondary, tertiary and so on down the list if more than one is specified. Each of these must be an IP address and not a name. The computer has no way to resolve the name until it connects to a nameserver. Screamingly obvious when stated, but occasionally overlooked when people are simply asked to supply an address for a computer. In addition

to a default domain, you can also specify search domains. Search domains work differently; they progress from one to six in a similar manner to the nameserver. However, they all take precedence over the default domain! Keep this in mind when specifying search domains. Search domains are not commonly used. The one item not yet covered is the check box for DNS usage. If you are running a small private network with no Internet connection, then using /etc/hosts files and keeping them all synchronized will work. As you add more and more machines, the complexity increases until it is easier to have a single machine run a DNS than to continue to sync /etc/hosts files. There is another reason for not using DNS, and that is if your network is going to use NIS instead. Note that NIS can be used in conjunction with DNS. So to sum it all up, unless you know why using /etc/hosts or NIS would be best for your situation, DNS is probably going to be your best choice. You can add, modify, or delete entries from the /etc/hosts file using Linuxconf. Open [Config] -> [Networking] -> [Misc] -> [Information about other hosts].

![](img/46f4935125ba89e12897afbe9d77a097_218_0.png)

Figure 8-24: /etc/hosts Screen
