• To mark a packet of interest to you, click the middle mouse button. This will highlight the packet, making it easier to find later. (If you only have a two-button mouse, and you indicated during installation that it should emulate a three-button mouse, you can click both mouse buttons together to emulate the middle mouse button.)

# ## Using Ethereal Filters

If you are monitoring a busy server or a busy network, Ethereal can gather so much data that it can become almost unusable. If you know what you are looking for, however, you can filter what packets are captured based on values you enter.

Filters in Ethereal are implemented using the pcap library (type `man pcap` to read about it). The filter expressions you can use with Ethereal are described on the `tcpdump` man page. Here are some examples of filters that you could enter into the Filter box when you capture Ethernet data with Ethereal:

```
```
host 10.0.0.15
```
```

The host primitive lets you only capture packets that are either to or from a particular host computer (by IP address or host name). By preceding host with `src` or `des`, you can indicate that you only want packages sent from a particular source or to a particular destination host.

```
```
tcp port 80
```
```

You can enter a protocol name (such as `tcp`, `ether`, `udp`, or `ip`) to limit captured packets to those that are assigned to that protocol. As shown in the previous example, with `tcp` you could also indicate a port number (such as 80, to monitor traffic to and from your Web server).

You can filter for certain special activities on the network, using such things as the `gateway`, `broadcast`, or `multicast` primitives. Entering `gateway host` lets you find packets sent to a gateway host that is neither a Source nor Destination for the packet (which is determined because the Ethernet address doesn't match either of those IP addresses). Enter `ether broadcast` to monitor broadcast packets on your Ethernet network, such as announcements from name servers announcing availability. Likewise, you could filter for multicast packets on `ether` or `ip` protocols (`ether multicast`).

The Info column gives you details about the intention of the packet. For example, you can see the type of service that was requested (such as `http` for Web service or FTP for file transfer). You can see what information is being broadcast and determine when attempts to find particular host computers are failing. If you believe someone is using your network improperly, you can see which sites they are visiting and the services they are requesting.