# Specify Your Name Servers

You can specify any DNS name servers you need to connect to the network or resolve names to IP addresses on your local network by creating entries in the `/etc/resolv.conf` file. Two key types of entries are needed in this file:

+   - **domain:** The domain entry specifies the domain name of your local network. For instance, if your local network has the domain name `juxta.com`, the first line of `resolv.conf` could be:
+   
+     `domain juxta.com`
+   - **nameserver:** The nameserver entry specifies the name of a DNS server. You need one entry for each DNS server you have available to use in the order of preference. Therefore, your primary name server should be listed first, the secondary server listed second and so on. For instance, if you have two name servers, a primary at 192.168.147.200 and a secondary at 192.168.147.201, then you would have two nameserver entries:
+   
+     `nameserver 192.168.147.200`
+     `nameserver 192.168.147.201`

# Edit Your Local hosts File

As discussed earlier in this chapter when we covered configuring network in Red Hat Linux 6.2 using the `netconf` tool, most systems use a local `/etc/hosts` file as the first source of hostname to IP address mapping information.

To use this file, make sure that your name server search path is correctly configured. For instance, if you want name server lookups to first check your local hosts file and then attempt lookups against your DNS servers, then you need the following entry in the `/etc/host.conf` file:

```
order hosts,bind
```

This entry indicates that hosts lookups start with the hosts file and then move on to bind, the Berkeley Internet Name Daemon (or DNS).

Once the search path is defined, you need to create entries in the `/etc/hosts` file for those hosts which you frequently access. Each entry takes the following form:

```
`<IP address> <hostname> <alias> <alias> ...`
```

At a minimum, each entry needs the IP address and the primary hostname. In addition, you can specify one or more aliases which represent alternate names for the host in question. For instance, consider the following series of entries from an `/etc/hosts` file:

```
127.0.0.1       localhost.localdomain    localhost
192.168.147.30  linux.juxta.com           linux
192.168.147.50  foo.juxta.com
```