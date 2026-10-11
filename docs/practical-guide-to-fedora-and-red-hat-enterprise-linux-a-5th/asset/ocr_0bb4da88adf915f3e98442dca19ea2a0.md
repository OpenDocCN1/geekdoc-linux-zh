system's NIS domain is set just before it is needed. You can use the `nisdomainname` utility to set or view the NIS domain name, but setting it in this manner does not maintain the name when the system is rebooted:

```
```
# nisdomainname
(none)
# nisdomainname mgs
# nisdomainname
mgs
```
```

# **A DNS domain name is different from an NIS domain name**

> The DNS domain name is used throughout the Internet to refer to a group of systems. DNS maps these names to IP addresses to enable systems to communicate with one another.
> The NIS domain name is used strictly to identify systems that share an NIS server and is normally not seen or used by users and other programs. Some administrators use one name as both a DNS domain name and an NIS domain name, although this practice can degrade security.

# **To avoid confusion, use nisdomainname, not domainname**

> The domainname and nisdomainname utilities do the same thing: They display or set the system's NIS domain name. Use `nisdomainname` to avoid confusion when you are also working with DNS domain names.

# **You must set the local system's NIS domain name**

> If you do not set the local system's NIS domain name, when you start `ypbind`, it sends a message to `rsyslogd` (page 582) and quits.

# EDIT /etc/yp.conf TO SPECIFY AN NIS SERVER

Edit `/etc/yp.conf` to specify one or more NIS servers (masters and/or slaves). As explained by comments in the file, you can use one of three formats to specify each server:

+   `domain` `nisdomain` `server` `server_name`
+   
+   `domain` `nisdomain` `broadcast` (do not use)
+   
+   `ypserver` `server_name`

where `nisdomain` is the name of the NIS domain that the local (client) system belongs to and `server_name` is the hostname of the NIS server that the local system queries. The second format is less secure than the first and third formats because it exposes the system to rogue servers by broadcasting a request for a server to identify itself.

You can use multiple lines to specify multiple servers for one or more domains. Specifying multiple servers for a single domain allows the system to change to another server when its current server is slow or down.