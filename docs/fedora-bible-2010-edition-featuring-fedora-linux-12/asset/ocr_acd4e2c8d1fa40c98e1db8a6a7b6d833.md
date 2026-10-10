```
```
Channel 10 : 2.457 GHz
Channel 11 : 2.457 GHz
Channel 12 : 2.457 GHz
Channel 13 : 2.457 GHz
Channel 14 : 2.462 GHz
Current Frequency:2.412GHz (Channel 1)
```
```

The `freq` parameter displays the frequencies (and channels) available for communication. Note that all the available frequencies are in the `2.4` `GHz` range.

```
```
# iwl i st eth0 rate
eth0    6 available bit-rates :
1Mb/s
2Mb/s
5.5Mb/s
11Mb/s
58Mb/s
39.5Mb/s
Current Bit Rate=54Mb/s
```
```

The preceding `rate` parameter displays the transmission rates available for the wireless interface. You can see that 1, 2, 5.5, and 11 Mbps rates are available for the current interface.

```
```
# iwl i st eth0 key
eth0    2 key sizes : 40, 104bits
4 keys available :
[1] 7365-6375-31 (40 bits)
[2] off
[3] off
[4] off
Current Transmit Key: [1]
```
```

The `key` parameter lets you see the encryption keys available with the interface. It also shows the key sizes currently available. Because the card reflected in the preceding example supports 64- and 128-bit encryption, the key sizes available are 40 and 104 bits. (The encryption algorithm automatically generates the last 24 bits of each key.)

If you are troubleshooting your wireless LAN connection, some settings are more likely than others to cause problems. It is important to set the following wireless LAN settings properly — if you don’t, they may keep your network from working:

+   - **Network ID (ESSID)** — You may not be able to communicate among peer computers if the Network ID, also called network name or ESSID, doesn’t match on each of them. Network IDs are case sensitive — for example, `MyLAN` is not the same as `MyLAN`.

+   - **Encryption key** — Having encryption keys that don’t match is like trying to log in to Linux with the wrong password. Check that all nodes are using the same key. (If nodes were unable to connect, check the encryption key first because typing long hexadecimal keys can be prone to error.)