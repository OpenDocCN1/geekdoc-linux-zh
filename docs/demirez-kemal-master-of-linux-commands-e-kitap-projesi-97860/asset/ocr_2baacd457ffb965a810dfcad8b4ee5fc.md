```
root@kemal:~# ettool -S wlan0
NIC statistics:
rx_packets: 157215
rx_bytes: 9599806
rx_duplicates: 4718
rx_fragments: 112112
rx_dropped: 4733
tx_packets: 40927
tx_bytes: 5265203
tx_fragments: 40927
tx_filtered: 0
tx_retry_failed: 3
tx_retries: 0
beacon_loss: 0
sta_state: 4
txrate: 36000000
rxrate: 24000000
signal: 0
channel: 0
noise: 1844674403709551615
ch_time: 1844674403709551615
ch_time_busy: 1844674403709551615
ch_time_ext_busy: 1844674403709551615
```

We can configure our network in two ways. First, it can be done automatically with a DHCP server (modem performs this work in your local area network). Second way is to configure the network by entering the value manually. To obtain network settings from the DHCP server automatically dhclient eth0 command is used. If you want to make manual adjustments, Let's say to set your local ip address as to 192.168.1.12, you should use ifconfig eth0 192.168.1.12 (for wireless network ifconfig wlan0 192.168.1.12) command.

```
root@kemal:~# ifconfig wlan0 192.168.1.12
root@kemal:~# ifconfig
```

wlan0 Link encap:Ethernet Hwaddr 54:e6:fc:95:6f:ec
net addr:192.168.1.12 Bcast:192.168.1.255 M
inet6 addr: fe80::56e6:fc:fe95:6f/64 Scope