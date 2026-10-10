an attempt to get clients to disassociate with their current AP and associate to a rogue network.

```
alert=CHANGE,5/min,1/sec
```

This alert notes if a previously detected network suddenly changes channels. This is a good indication of an attempt at spoofing a network, since most networks don’t change channels on a regular basis.

```
alert=AIRJACKSSID,5/min,1/sec
```

This alert looks for the probe SSID name of “airjACK,” the initial SSID of airjACK tools. The airjACK tools allow for raw mode injection and reception, and are used in a number of possibly malicious tools. This alert only detects the SSID of airjACK and not the tools themselves. A skilled attacker could easily change the initial SSID to something more innocuous.

```
alert=PROBENOJOIN,10/min,1/sec
```

If a client probes for an existing network and is accepted but does not join, this is an indication of some firmware-based network discovery tools such as Netstumbler. In some situations, this can generate a great number of false positives and may not be indicative of an attack. This can also be triggered by some network client applications waiting for user input before associating.

```
alert=DISSASOCTRAFFIC,10/min,1/sec
```

If a client appears to disassociate from the AP, it should normally not be attempting to communicate with the AP right afterwards. If this alert is triggered, it is likely the client specified in the alert has been the victim of a disassociation attack where an attacker sends a forged packet to the AP indicating the client is leaving.

```
alert=NULLPROBERESP,10/min,1/sec
```

This is an indication of an attack against some firmware versions by many manufacturers that have a fatal error if they receive a SSID probe of null length (no length). This can be a sign of a Denial of Service (DoS) attack or misbehaving client.

```
alert=BSSTIMESTAMP,10/min,1/sec
```

Each packet from an AP is time-stamped and should be received in something resembling a continuous stream. It is not possible to spoof the time stamp with normal drivers, so a wildly different time stamp received is an indication that someone may be trying to spoof the AP’s SSID and/or MAC address. This may trigger some false positives in situations of high loss where not all packets are being received.