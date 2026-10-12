![](bbox=[0.12, 0.15, 0.2, 0.28])

The NIS domain is different from the DNS domain names discussed earlier in this chapter. Pick an NIS domain name that's not related to the DNS domain name. Doing so makes it harder for crackers to guess your NIS domain name (if they know the NIS domain name, there is a risk that they can get the NIS password database).

# NIS configuration-file setup

The ypbind daemon, described in the next section, needs information about the NIS domains and NIS servers to do its job. It finds this information in the /etc/yp.conf configuration file. The ypbind daemon reads the /etc/yp.conf file when it starts up or when it receives the SIGHUP signal (as it does, for example, when you restart ypbind with the kill -HUP command).

To specify one or more NIS servers for the local domain (which you have already set with the domainname command), all you need in /etc/yp.conf are lines such as the following:

```
ypserver nisadmin
ypserver 192.168.0.4
```

You can use a name such as nisadmin if that name is listed in the /etc/hosts file (that way, ypbind can resolve the name into an IP address without having to use NIS). Otherwise, you should specify the NIS server's IP address.

In /etc/yp.conf, you can also specify specific NIS servers for specific NIS domains, like this:

```
domain sales server nissales
domain admin server nisadmin
```

A third type of entry in the /etc/yp.conf file specifies that ypbind should use IP broadcast in the local network to find an NIS server for a specified domain. To do so, add a line such as the following to /etc/yp.conf:

```
domain admin broadcast
```

# NIS client-daemon setup

Every computer in an NIS domain, including the server, runs the ypbind daemon. Various NIS client applications, such as ypwhich, ypcat, and yppoll, need the ypbind daemon to obtain information from the master NIS server. More precisely, the C library contacts the ypbind daemon to locate the NIS server for the domain. Then the C library contacts the server directly to obtain administrative information. The client applications get the information through functions in the C library.