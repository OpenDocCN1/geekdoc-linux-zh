# Configuring the Client

Let's walk through the process of configuring a Linux client to use a DNS server. We'll assume that we are using the DNS server on serverA and we are configuring serverA itself to be the client. This may sound a bit odd at first, but it is important for you to understand that just because a system runs the server does not mean it cannot be a client! Think of it as running a web server—just because a system runs Apache doesn't mean you can't run Firefox on the same machine and access the web sites hosted locally on the machine via the loop-back address (127.0.0.1)!

Breaking out the steps to configure the client, we see the following:

+   Edit /etc/resolv.conf and set the nameserver entry to point to your DNS server.
Per our example:

```
search example.org
nameserver 127.0.0.1
```

+   Look through the /etc/nsswitch.conf file to make sure that DNS is consulted for hostnames resolutions:

```
[root@serverA ~]# grep "hosts" /etc/nsswitch.conf
```

If you don't have dns listed, in this output, use any text editor to include dns on the host line.

+   Test the configuration with the dig:

```
[root@serverA ~]# dig +short serverA.example.org
192.168.1.1
```

Notice that you didn't have to specify the name server to use with dig (such as dig @localhost +short serverA.example.org) for the preceding query. This is because dig will by default use (query) the DNS server specified in the local /etc/resolv.conf file.

# Summary

This chapter covered all the information you'll need to get a basic DNS server infrastructure up and running. We also discussed:

+   Name resolution over the Internet
Obtaining and installing the BIND name server
The /etc/hosts file
The process of configuring a Linux client to use DNS
Configuring DNS servers to act as primary, secondary, and caching servers