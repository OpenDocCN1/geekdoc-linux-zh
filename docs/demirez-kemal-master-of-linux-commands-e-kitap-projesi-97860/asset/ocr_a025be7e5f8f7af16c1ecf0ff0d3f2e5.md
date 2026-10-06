# Kemal Demirez | 235

```
root@kemal:~# ifconfig
wlan0      IEEE 802.11g SSID:"Ibrahim"
               Mode:Managed Frequency:2.412 GHz Access Point: 64:66:B3:55:90:79
               Bit Rate:36Mb/s TX-Power:20 dBm
               Retry short limit:7 RTS:off thr:off
               Encryption:off
               Power Management:off
               Link Quality=40/70 Signal=-70 dBm
               RX invalid mid:0 RX invalid crypt:0 RX invalid frag:0
               TX excessive retries:3 Invalid misc:4638 Missed beacon:0
lo                no wireless extensions.
eth0              no wireless extensions.
```

If you are using wired connection, you should use ifconfig eth0 to configure the network. If you are using a wireless connection, you must use ifconfig wlan0 command to see the wireless network configuration information.

```
root@kemal:~# ifconfig wlan0
wlan0      Link enc:Ethernet HWaddr 54:e6:fc:95:gf:ec
               inet addr:192.168.1.3 Cast:192.168.1.255 Mask:255.255.255.0
               inet6 addr:fe80::566:ff:fe05/64 Scope:link
               UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
               RX packets:66876 errors:0 dropped:0 overflows:0 frame:0
               TX packets:39762 errors:0 overflows:0 carrier:0
               collisions:0 txqueuel:1000
               RX bytes:8711302 (8.3 MiB) TX bytes:4917685 (4.7 MiB)
```

Get the information about the Ethernet and wireless drivers in wired or wireless connection you can use ettool -i eth0 and ettool -i wlan0 commands.

§