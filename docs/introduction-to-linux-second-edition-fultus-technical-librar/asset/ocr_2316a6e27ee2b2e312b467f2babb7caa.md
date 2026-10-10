# 10.2.3.3 **PCMCIA commands**

On your laptop which you usually connect to the company network using the onboard Ethernet connection, but which you are now to configure for dial-in at home or in a hotel, you might need to activate the PCMCIA card. This is done using the `cardctl` control utility, or the `pcardctl` on newer distributions.

A usage example:

```
```
cardctl insert
```
```

Now the card can be configured, either using the graphical or the command line interface. Prior to taking the card out, use this command:

```
```
cardctl eject
```
```

However, a good distribution should provide PCMCIA support in the network configuration tools, preventing users from having to execute PCMCIA commands manually.

# 10.2.3.4 **More information**

Further discussion of network configuration is out of the scope of this document. Your primary source for extra information is the man pages for the services you want to set up. Additional reading:

+   *   The Modem-HOWTO <http://www.tldp.org/HOWTO/Modem-HOWTO.html>: Help with selecting, connecting, configuring, trouble-shooting, and understanding analog modems for a PC.

+   *   LDP HOWTO Index, section 44 <http://www.tldp.org/HOWTO/HOWTO-INDEX/networking.html#NETGENERAL>: categorized list of HOWTOs about general networking, protocols, dial-up, DNS, VPNs, bridging, routing, security and more.

+   *   Most systems have a version of the `ip-cref` file (locate it using the `locate` command); the PS format of this file is viewable with for instance `gv`.

# 10.2.4 **Network interface names**

On a Linux machine, the device name `lo` or the `local loop` is linked with the internal 127.0.0.1 address. The computer will have a hard time making your applications work if this device is not present; it is always there, even on computers which are not networked.

The first ethernet device, `eth0` in the case of a standard network interface card, points to your local LAN IP address. Normal client machines only have one network