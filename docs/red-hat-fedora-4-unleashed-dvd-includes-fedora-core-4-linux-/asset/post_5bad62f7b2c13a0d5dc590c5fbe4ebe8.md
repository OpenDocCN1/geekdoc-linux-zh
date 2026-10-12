
- Manually editing the system's `/etc/nsswitch.conf` configuration file to specify the methods and order of name resolution
- Manually editing the system's `/etc/hosts` file which lists specific hostnames and IP addresses
- Manually editing the system's `/etc/resolv.conf` configuration file to add nameserver, domain, or search definition entries

Successful DNS lookups depend on the system's networking being enabled and correctly configured. You can learn more about how to accomplish that in Chapter 17, “Network Connectivity.”

When an application needs to resolve a hostname, it calls system library functions to do the name resolution. If the GNU C library installed is version 2 or greater, then the `/etc/nsswitch.conf` configuration file is used. Older versions of the library use `/etc/host.conf`. Fedora uses the newer GNU C library, but `/etc/host.conf` is still provided for applications that have been statically linked with other libraries. The two files should be kept in sync.

### Understanding the /etc/host.conf File

The file `/etc/host.conf`, known as the resolver configuration file, specifies which services to use for name resolution and what order they are to be used. This file has been superseded by `/etc/nsswitch.conf`, but is still provided for applications that use other libraries.

By default with Fedora, this file contains

```
order hosts,bind
```

The order shown here is to first consult `/etc/hosts` for a hostname. If the hostname is found in `/etc/hosts`, use the IP address specified there. If it is not found in `/etc/hosts`, then try and resolve the name using DNS (BIND).

One other option is available, although not set by default. This is nis, which is Sun's Network Information Service.

### Understanding the /etc/nsswitch.conf File

The file `/etc/nsswitch.conf` is the System Databases and Name Service Switch configuration file. It contains methods for many types of lookups, but here we are concerned with DNS resolution, so the line we are interested in is the hosts line. This line defines the methods to be used for resolving hostnames and the order in which to apply them. The methods used are

- db—Local database files (*.db)
- files—Use the local file `/etc/hosts`
- dns—Use BIND
- nis—Use Sun's NIS (Network Information Service)
- nisplus—Use Sun's NIS+

The default line with Fedora Core is `hosts: files dns`

With this default, the same methods and order are specified as in the default `/etc/host.conf`. First, `/etc/hosts` is searched, and then DNS is used. Another example would be `hosts: files dns nisplus nis`

In this example, name searches that fail in `/etc/hosts` and with DNS will continue to the NIS services (nisplus and nis). NIS included with Fedora Core is the ypserv daemon.

When you are testing your configuration, you may want to halt name searching at a specific point. You can use the entry `[NOTFOUND=return]`. For example, to stop searching after looking in `/etc/hosts`, you would use the line `hosts: files [NOTFOUND=return] dns nisplus nis`

### Understanding the /etc/hosts File

The file `/etc/hosts` contains a table of local hosts (hostnames and IP addresses) used for local DNS-type lookups. The file is used if the keyword `hosts` is included in the order line of `/etc/host.conf`.

Using `/etc/hosts` to provide hostnames and hostname aliases can be effective when used on small networks. For example, a short `/etc/hosts` might look like this:

```
...
192.168.1.3	wind.maximumhoyt.com	wind webserver #always breaks
192.168.1.4	marvin.maximumhoyt.com	marvin mailserver
192.168.1.5	titan.maximumhoyt.com	titan cvshost
192.168.1.6	hp.maximumhoyt.com	hp
...
```

This example shows a short list of hosts. The format of the file is an IP address, a hostname/domain name, and aliases (such as `marvin` and `mailserver`). Using this approach, a system administrator would maintain and update a master hosts list, and then replicate the complete `/etc/hosts` file to every computer on the LAN. Users are then able to access other systems by simply using the hostname alias (such as `marvin`). The format of `/etc/hosts` is easy to understand and easy to maintain, and can be used in conjunction with DNS, and in conjunction with a Dynamic Host Configuration Protocol (DHCP) server on the same network.

Two disadvantages of using `/etc/hosts` become readily apparent on a large network: maintenance and replication. Maintaining huge lists of IP addresses, hostnames, and aliases—along with ensuring that changes are regularly updated to every host on the network—can be a challenge.

The `/etc/hosts` file can be edited with a text editor, or by using the `system-config-network` GUI configuration tool which can be launched from the Network menu item in the System Settings menu. The Hosts tab allows editing the file.

## Understanding the /etc/resolv.conf File

The file `/etc/resolv.conf` specifies how DNS searches are made. The file contains a list of nameservers (DNS servers to connect to) and some options.

For example, a simple, but usable `/etc/resolv.conf` generally contains at least two nameserver entries, specifying a primary and secondary nameserver. This example uses fictitious internal IP addresses:

```
nameserver 192.168.1.1
nameserver 192.168.1.2
search mydomain.com
```

The IP addresses listed in the `/etc/resolv.conf` file are usually assigned by an ISP and represent the remote nameservers. Other optional keywords, such as `domain` and `search`, are used to specify a local domain and search list for queries; the two terms are mutually exclusive, however (and we will explain these terms shortly). If you have both, the last one listed will be used.

The information in `/etc/resolv.conf` can be configured from the `system-config-network` tool by launching the tool from the Network menu item in the System settings menu. The DNS tab allows you to enter or edit the DNS information, as shown in Figure 26.1.

![](img/774d40fd20903495c5cd00e2efad3f33_742_0.png)

**FIGURE 26.1** The GUI Network Configuration tool is one of Fedora Core’s best-designed GUI tools, permitting extensive network configuration.

## Understanding the Changes Made by DHCP

If your system is set to use DHCP, when the DHCP connection is made any existing `/etc/resolv.conf` is saved as `/resolv.conf.predchclient` and a new `/etc/resolv.conf` is created with the DNS information supplied by DHCP. When DHCP is released, the saved file is moved back as `/etc/resolv.conf`.

## Essential DNS Concepts

We begin with a look at the ideas behind DNS, prior to discussing the details of the software used to implement it. An understanding at this level is invaluable in avoiding the majority of problems administrators commonly experience with DNS, as well as in diagnosing and quickly solving the ones that do occur. The following overview omits several small details in the protocol because they are not relevant to the everyday tasks of a DNS administrator. If you need more information about DNS, consult the DNS standards, especially RFC 1034. (The RFCs related to DNS are distributed with BIND. Fedora Core installs them in `/usr/share/doc/bind-*/rfc/`.)

The domain namespace is structured as a tree. Each domain is a node in the tree and has a name. For every node, there are *resource records (RRs)*—each of which stores a single fact about the domain. (Who owns it? What is its IP address?) Domains can have any number of children, or subdomains. The root of the tree is a domain named `.` (similar to the `/` root directory in a file system.)

Each of the resource records belonging to a domain store a different type of information. For example,

- **A (Address)**—Records store the IP address associated with a name.
- **NS (Nameserver)**—Records name an authoritative nameserver for a domain.
- **SOA (Start of Authority)**—Records contain basic properties of the domain and the domain’s zone.
- **PTR (Pointer)**—Records contain the real name of the host to which the IP belongs.
- **MX (Mail Exchanger)**—Records specify a mail server for the zone.

Each record type is discussed in detail later in this chapter.

Every node has a unique name that specifies its position in the tree, just as every file has a unique path that leads from the root directory to that file. That is, in the domain name, one starts with the root domain `.`, and prepends to it each name in the path, using a dot to separate the names. The root domain has children named `com.`, `org.`, `net.`, `de.`, and so on. They, in turn, have children named `ibm.com.`, `wiw.org.`, and `gmx.de.`.

In general, a fully qualified domain name (FQDN) is one that contains the machine name, and the domain name, such as

```
foo.example.com.
```
