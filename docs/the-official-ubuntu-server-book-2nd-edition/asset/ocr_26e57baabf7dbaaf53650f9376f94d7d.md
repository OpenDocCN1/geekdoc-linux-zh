ubuntu2 *can* access web1, then I know the problem is more likely on ubuntu1. To start, let’s assume that ubuntu2 can access web1, so we will focus our troubleshooting on ubuntu1.

**_Is It Plugged In?_** The first troubleshooting steps to perform are on the client. You first want to verify that your client’s connection to the network is healthy. To do this you can use the `ethtool` program (installed via the `ethtool` package) to verify that your link is up (the Ethernet device is physically connected to the network), so if your Ethernet device was at eth0:

```
```text
$ sudo ethtool eth0
Settings for eth0:
    Supported ports: [ TP ]
    Supported link modes:   10baseT/Half 10baseT/Full
                            100baseT/Half 100baseT/Full
                            1000baseT/Half 1000baseT/Full
    Supports auto-negotiation: Yes
    Advertised link modes:  10baseT/Half 10baseT/Full
                            100baseT/Half 100baseT/Full
                            1000baseT/Half 1000baseT/Full
    Advertised auto-negotiation: Yes
    Speed: 100Mb/s
    Duplex: Full
    Port: Twisted Pair
    PHYAD: 0
    Transceiver: internal
    Auto-negotiation: on
    Supports Wake-on: pg
    Wake-on: d
    Current message level: 0x000000ff (255)
    Link detected: yes
```
```

Here on the final line you can see that Link detected is set to yes so ubuntu1 is physically connected to the network. If this were set to no you would need to physically inspect ubuntu1’s network connection and make sure it is connected. Since it is physically connected, I can move on.

# NOTE — Slow Network Speeds

`ethtool` has uses beyond simply checking for link. It can also be used to diagnose and correct duplex issues. When a Linux server connects to a network, typically it autonegotiates with the network to see what speeds it can use and whether the network supports full duplex. The Speed and Duplex lines in the example `ethtool` output illustrate what a 100Mb/s, full duplex network should report. If you notice slow network speeds on a host, its