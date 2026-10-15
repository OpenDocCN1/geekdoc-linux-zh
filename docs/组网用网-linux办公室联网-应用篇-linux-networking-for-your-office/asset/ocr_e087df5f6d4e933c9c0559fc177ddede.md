```
```text
# Our nameservers:
nameserver 192.168.3.100
nameserver 192.168.3.100
```
```

If you were to use this file and try to access services on a computer called polk, the system would perform DNS searches on polk, polk.threeroomco.com, polk.room1.threeroomco.com, and polk.room2.threeroomco.com. Note that multiple name searches can have some disadvantages. They take time, for one thing, though that's usually not a major problem because the individual transfers are so quick. More importantly, if you specify too many domains in the search line, you might get an unintended match to a mistyped name. For instance, if threeroomco.com has a machine called server, and if room2.threeroomco.com has a machine called server, an attempt to access server may actually access server.room2.threeroomco.com if you mistype the name. This specific situation calls out for renaming the computers within the organization, but if you start including external domains in your DNS search path, the problem becomes much more serious.

DNS is mainly used for finding the names of remote systems, and particularly those that are on distant networks. Linux includes another mechanism, the /etc/hosts file, for finding its own name and the names of local systems. The contents of /etc/hosts are described in the section titled “The /etc/hosts File.” How does Linux know whether to use /etc/hosts or DNS, though? The answer lies in the /etc/host.conf file, which has several commands:

+   - **order**—order specifies the order in which different name resolution services are tried. You normally want a line reading `order hosts,bind` in your `/etc/host.conf` file. This specifies that the `/etc/hosts` file is tried first, followed by DNS services (BIND is the name of the package that supplies DNS, and it's covered later in this chapter, in the section “Setting Up a DNS Server”).

> > **NOTE**
> >
> > A third type of name resolution is known as *Network Information System* (NIS), and Linux can be configured to use it. NIS can provide for unified login information on a network, as well as name resolution services. If your network has an NIS server, you can configure Linux to use it, though this topic is beyond the scope of this book. If your system is configured to use NIS, you can list it on the order line in `/etc/host.conf`.

+   - **multi**—multi indicates whether a host in `/etc/hosts` can have several IP addresses. You normally want this line to read `multi on` to permit such a situation.