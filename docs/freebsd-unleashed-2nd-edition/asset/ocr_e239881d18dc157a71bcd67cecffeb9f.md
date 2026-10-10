```
# ifconfig fxp1 64.41.131.103 netmask 255.255.255.0
# ifconfig fxp1 64.41.131.103 netmask 0xffffff00
# ifconfig fxp1 64.41.131.103 netmask your-netmask
```

You can also specify the broadcast address, although this generally isn’t useful except in really exceptional networks. Note that although the broadcast address is automatically extrapolated from the IP address and netmask if you omit it (as discussed earlier), the reverse is not true: Omitting the netmask makes ifconfig assume a Class A mask. If you have to set the broadcast address, make sure you set both it and the netmask at the same time:

```
# ifconfig fxp1 64.41.131.103 netmask 255.255.0.0 broadcast 64.41.255.255
```

In some conditions you might need to set the Maximum Transmission Unit (MTU) of the interface. The MTU indicates the largest packet size the card can send out (in bytes); this value is usually 1500 for Ethernet cards. Sometimes, you might want to set it to a smaller value to minimize latency on low-speed WAN links. Your router usually takes care of managing transfers to minimize latency, though, so don’t worry about this setting unless you have to and you know what you’re doing:

```
# ifconfig fxp1 mtu 536
```

One final trick that ifconfig can use involves the media keyword, which allows you to make the card switch between the various listed media types. This capability is very handy if you have a card with multiple interfaces (such as you saw in the “Network Components” section of Chapter 21) and you want to switch from the BNC connector to the RJ-45 (UTP) connector or from the RJ-45 to the AUI connector. If you have a 10/100 Ethernet card and an auto-sensing hub that has auto-negotiated a speed of 100Mbps full-duplex with your card, you can force it into 10Mbps mode with the media and mediaopt keywords. Take a look at what ifconfig fxp1 reports to be the supported media types (the following is a typical example):

```
media: autoselect (100baseTX <full-duplex>) status: active
supported media: autoselect 100baseTX <full-duplex> 100BaseTX
\u25c010baseT/UTP <full-duplex> 10baseT/UTP
```

This example tells you that you’re in auto-select mode. In that mode, the card negotiates the highest possible speed with the hub to which it’s connected. Set it instead to 10BaseT mode. The supported media: line tells you that the keyword for this is 10baseT/UTP, and that there’s an option of full-duplex that you can set if you choose to (using the mediaopt keyword). Options are shown in angle brackets. Displayed more clearly, the media types and options for this example are as follows:

```
autoselect
100baseTX <full-duplex>
```