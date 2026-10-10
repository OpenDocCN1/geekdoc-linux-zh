# ## PPP Over Ethernet (PPPoE)

Many xDSL users must set up nonpersistent PPP-based connections over an Ethernet interface; this is the case, for instance, when an ADSL modem connected to the FreeBSD machine via Ethernet does the dialing. PPPoE can be used in FreeBSD with only a few minor additions to the user PPP configuration file.

Create a new /etc/ppp/ppp.conf file as follows, replacing fxp0 with the name of your Ethernet device connected to the xDSL modem (if necessary), myisp with a keyword identifying your ISP, and yourname and yourpassword with your username and password used for logging in via PPP:

```
default:
    set device PPPoE:fxp0:myisp
    set speed sync
    set mru 1492
    set mtu 1492
    set cstrts off
    enable lqr
    add default HISADDR
    set timeout 0
    set redial 0 0

    # Network Address Translation (NAT)
    nat enable yes
    nat log yes
    nat same_ports yes
    nat unregistered_only yes
    enable dns

myisp:
    set authname yourname
    set authkey yourpassword
```

When you want to connect to the Internet, you can then run ppp from the command line, then enter dial myisp. You should then see output indicating a successful connection, after which you should be able to access the network.

# ## Troubleshooting PPP

If you are having trouble getting PPP to work, here are a few suggestions for troubleshooting.