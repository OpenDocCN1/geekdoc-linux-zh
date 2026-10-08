![](bbox=[0.12, 0.08, 0.87, 0.54])

This starts the DHCP service (dhcldient) on our tunnel (ha) and then puts the service into the background (&).

To get the clients to connect to our new Evil Twin AP, we need to knock them off the legitimate AP. We can do this the same way we did above in our WPA2 attack. We use the aireplay-ng command and send de-authentication frames into the AP (sometimes, this can DoS some of the older AP hardware).

This will make the legitimate AP unavailable to the clients, and they will connect to the Evil Twin instead!

```
kali > aireplay-ng -deauth 1000 aa:bb:cc:dd:ee:ff wlan0mon -ignore-
```