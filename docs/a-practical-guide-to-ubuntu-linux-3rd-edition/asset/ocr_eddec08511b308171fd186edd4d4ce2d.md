# To avoid confusion, use nisdomainname, not domainname

> The domainname and nisdomainname utilities do the same thing: They display or set the system's NIS domain name. Use nisdomainname to avoid confusion when you are also working with DNS domain names.

# You must set the local system's NIS domain name

> If the /etc/defaultdomain file is not present, the NIS server and client will not start.

# /etc/yp.conf: SPECIFIES AN NIS SERVER

Edit /etc/yp.conf to specify one or more NIS servers (masters and/or slaves). You can use one of three formats to specify each server:

```
    domain nisdomain server server_name
    domain nisdomain broadcast (do not use)
    ypserver server_name
```

where *nisdomain* is the name of the NIS domain that the local (client) system belongs to and *server_name* is the hostname of the NIS server that the local system queries. It is best to specify *server_name* as an IP address or a hostname from /etc/hosts. If you specify a hostname that requires a DNS lookup and DNS is down, NIS will not find the server. The second format puts *ypbind* in broadcast mode and is less secure than the first and third formats because it exposes the system to rogue servers by broadcasting a request for a server to identify itself. Under Ubuntu Linux, if you do not specify an NIS server, or if the server you specify is not available, an NIS client runs in broadcast mode.

Following is a simple *yp.conf* file for a client in the *mgs* domain with a server at 192.168.0.10:

```
    $ cat /etc/yp.conf
    domain mgs server 192.168.0.10
```

You can use multiple lines to specify multiple servers for one or more domains. Specifying multiple servers for a single domain allows the system to change to another server when its current server is slow or down.

When you specify more than one NIS domain, you must set the system's NIS domain name before starting *ypbind* so the client queries the proper server. Specifying the NIS domain name in /etc/defaultdomain before running the *ypbind* init script takes care of this issue (page 746).

# TESTING THE SETUP

After starting *ypbind*, use *nisdomainname* to make sure the correct NIS domain name is set. Refer to " /etc/defaultdomain: Specifies the NIS Domain Name " on page 746 if you need to set the NIS domain name. Next use *ypwhich* to check whether the system is set up to connect to the proper server; the name of this server is set in /etc/yp.conf (page 747):

```
    $ ypwhich
    plum
```