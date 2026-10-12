The default line with Fedora Core is
`hosts: files dns`

With this default, the same methods and order are specified as in the default `/etc/host.conf`. First, `/etc/hosts` is searched, and then DNS is used. Another example would be
`hosts: files dns nisplus nis`

In this example, name searches that fail in `/etc/hosts` and with DNS will continue to the NIS services (nisplus and nis). NIS included with Fedora Core is the ypserv daemon.
When you are testing your configuration, you may want to halt name searching at a specific point. You can use the entry `[NOTFOUND=return]`. For example, to stop searching after looking in `/etc/hosts`, you would use the line
`hosts: files [NOTFOUND=return] dns nisplus nis`

# Understanding the /etc/hosts File

The file `/etc/hosts` contains a table of local hosts (hostnames and IP addresses) used for local DNS-type lookups. The file is used if the keyword `hosts` is included in the order line of `/etc/host.conf`.

Using `/etc/hosts` to provide hostnames and hostname aliases can be effective when used on small networks. For example, a short `/etc/hosts` might look like this:

```
```
...
192.168.1.3	wind.maximumhoyt.com	wind webserver #always breaks
192.168.1.4	marvin.maximumhoyt.com	marvin mailserver
192.168.1.5	titan.maximumhoyt.com	titan cvshost
192.168.1.6	hp.maximumhoyt.com	hp
...
```
```

This example shows a short list of hosts. The format of the file is an IP address, a hostname/domain name, and aliases (such as `marvin` and `mailserver`). Using this approach, a system administrator would maintain and update a master hosts list, and then replicate the complete `/etc/hosts` file to every computer on the LAN. Users are then able to access other systems by simply using the hostname alias (such as `marvin`). The format of `/etc/hosts` is easy to understand and easy to maintain, and can be used in conjunction with DNS, and in conjunction with a Dynamic Host Configuration Protocol (DHCP) server on the same network.

Two disadvantages of using `/etc/hosts` become readily apparent on a large network: maintenance and replication. Maintaining huge lists of IP addresses, hostnames, and aliases—along with ensuring that changes are regularly updated to every host on the network—can be a challenge.