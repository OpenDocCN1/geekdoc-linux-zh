# NOTE

When you use the broadcast method, you must have an NIS server in every subnet because broadcasts do not span multiple subnets. If you are uncertain whether a particular NIS server is in the same subnet, you can find out by pinging the broadcast address. If the NIS server is one of the hosts that responds, then you know for sure that the broadcast method will work.

The other technique for client-to-server contact is specifying the host name of the server. This method works well when you need to subnet your network, but you don’t need an NIS server in every subnet. This allows a client to move anywhere inside your network and still be able to find the NIS server—however, if you need to change a client so that it points to another NIS server (to balance the network load), you’ll need to change that yourself.

+   ● Broadcast Method If you choose the broadcast technique, edit the /etc/yp.conf file so that it reads as follows:

```
domain my.nis.domainname broadcast
```

where my.nis.domainname is the name of your NIS domain. Remember that if you need failover support, you will need to have two NIS servers in every subnet in order for broadcast to find the second server.

+   ● Server Hostname Method If you want to specify the name of the NIS server directly, edit the /etc/yp.conf file so that it reads as follows:

```
domain my.nis.domainname server servername
```

where my.nis.domainname is the name of your NIS domain and servername is the name of the NIS server to which you want this client to refer. You can specify this option more than once if you want to point to redundant servers. If you specify both one or more servers by name and a broadcast option, ypbind will attempt to use the named servers first and fall back on the broadcast option only as a last resort.

# NOTE

Remember that you also have an entry for servername in the /etc/hosts file. At the time NIS is started, you may not yet have access to DNS, and you most certainly don’t have access to the NIS hosts table yet! For this reason, the client must be able to do the host name-to-IP resolution without the aid of any other services.