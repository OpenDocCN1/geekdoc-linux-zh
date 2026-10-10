network. For this example, though, we'll walk through each intermediary step to illustrate how you might test each level.

# ## Client or Server Problem

One quick test you can perform to narrow down the cause of your problem is to go to another host on the same network and try to access the server. In this example, you would find another server on the same network as dev1, such as dev2, and try to access web1. If dev2 also can't access web1, then you know the problem is more likely on web1, or on the network between dev1, dev2, and web1. If dev2 can access web1, then you know the problem is more likely on dev1. To start, let's assume that dev2 can access web1, so we will focus our troubleshooting on dev1.

# ## Is It Plugged In?

The first troubleshooting steps to perform are on the client. You first want to verify that your client's connection to the network is healthy. To do this you can use the ethtool program (installed via the ethtool package) to verify that your link is up (the Ethernet device is physically connected to the network). If you aren't sure what interface you use, run the /sbin/ifconfig command to list all the available network interfaces and their settings. So if your Ethernet device was at eth0

```
```
$ sudo ethtool eth0
Settings for eth0:
  Supported ports: [ TP ]
  Supported link modes:  10baseT/Half 10baseT/Full
                          100baseT/Half 100baseT/Full
                          1000baseT/Half 1000baseT/Full
  Supports auto-negotiation: Yes
  Advertised link modes:     10baseT/Half 10baseT/Full
                              100baseT/Half 100baseT/Full
                              1000baseT/Half 1000baseT/Full

  Advertised auto-negotiation: Yes
  Speed: 1000Mb/s
  Duplex: Full
  Port: Twisted Pair
  PHYAD: 0
  Transceiver: internal
```
```