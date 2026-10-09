# To avoid confusion, use nisdomainname, not domainname

tip The *domainname* and *nisdomainname* utilities do the same thing: They display or set the system’s NIS domain name. Use *nisdomainname* to avoid confusion when you are also working with DNS domain names.

# You must set the local system’s NIS domain name

tip If you do not set the local system’s NIS domain name, when you start *ypbind*, it logs an error and quits.

# /etc/yp.conf: SPECIFIES AN NIS SERVER

Edit */etc/yp.conf* to specify one or more NIS servers (masters and/or slaves). As explained by comments in the file, you can use one of three formats to specify each server:

+   * *domain* *nisdain* *server* *server_name*
+   * *domain* *nisdain* *broadcast* (do not use)
+   * *ypserver* *server_name*

where *nisdain* is the name of the NIS domain that the local (client) system belongs to and *server_name* is the hostname of the NIS server that the local system queries. It is best to specify *server_name* as an IP address or a hostname from */etc/hosts*. If you specify a hostname that requires a DNS lookup and DNS is down, NIS will not find the server. The second format puts *ypbind* in broadcast mode and is less secure than the first and third formats because it exposes the system to rogue servers by broadcasting a request for a server to identify itself.

Following is a simple *yp.conf* file for a client in the *mgs* domain with a server at 192.168.206.181:

```
$ cat /etc/yp.conf
domain mgs server 192.168.206.181
```

You can use multiple lines to specify multiple servers for one or more domains. Specifying multiple servers for a single domain allows the system to change to another server when its current server is slow or down.

When you specify more than one NIS domain, you must set the system’s NIS domain name before starting *ypbind* so the client queries the proper server. Specifying the NIS domain name in */etc/sysconfig/network* before starting the *ypbind* service takes care of this issue (page 774).

# START ypbind

The *ypbind* daemon is *ypbind-mt* renamed—that is, a newer, multithreaded version of the older *ypbind* daemon. Enable and start *ypbind* as explained on page 773.