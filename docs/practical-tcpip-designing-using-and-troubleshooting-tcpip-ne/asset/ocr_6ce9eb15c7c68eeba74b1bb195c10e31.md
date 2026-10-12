added, will be used first, as you'll see if you do “`route -n`”; run **`tcpdump -e -n`** to check which router is being used (by seeing which MAC address your PC sends the packets to).

```
route add default gw 192.0.2.99 non-existent gateway
route add default gw 192.0.2.1 real gateway
```

(One of our Linux systems ARPs for the non-existent gateway for 5–10 minutes, and then switches to the second gateway successfully, whereas another different version of Linux tries the non-existent gateway seemingly forever.)

# Windows

The Windows **Control Panel > Network** applet makes it look as though the default gateway is specific to an interface; it isn’t – it’s a routing table entry and not an interface parameter. The NT Resource Kit recommends you specify default gateways on one network card only to avoid confusion.

You can set multiple default gateways on a single interface using the **Advanced** button in the **Control Panel > Network > TCP/IP Properties** window. Windows uses “dead gateway detection” (see Notes) to decide when to switch from one to another. This is activated only by certain protocols (TCP) so testing it out with **ping**, etc. is difficult.

Because very few sites have multiple Internet connections we don’t discuss this topic further, other than in the Notes at the end of the chapter.