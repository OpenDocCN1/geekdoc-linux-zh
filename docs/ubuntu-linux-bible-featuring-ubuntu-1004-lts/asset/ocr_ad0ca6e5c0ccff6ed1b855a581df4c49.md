# Part II: Ubuntu for Desktop Users

ESSID: "vwh*
Mode:Master
Frequency:2.427 GHz (Channel 4)
Quality=52/100 Signal level=34/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 6 MB/s; 9 MB/s
11 MB/s; 12 MB/s; 18 MB/s; 24 MB/s; 36 MB/s
48 MB/s; 54 MB/s

Cell 03 - Address: 00:06:25:78:CE:3F
ESSID: "vwh*
Mode:Master
Frequency:2.437 GHz (Channel 6)
Quality=57/100 Signal level=40/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s

This command is useful for verifying that a wireless interface is actually working and that it can communicate with an access point. The information provided by iwlist command is useful in public areas, where you will usually detect more wireless networks, as in the following example from one of my laptops while I was on vacation:

```
$ sudo iwlist eth0
Password:
Scan completed :
Cell 01 - Address: 00:09:5B:36:22:38
ESSID: "Wireless"
Mode:Master
Frequency:2.412 GHz (Channel 1)
Signal level=220/153 Noise level=12/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 02 - Address: 00:12:17:A6:E8:C8
ESSID: "linksys"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Signal level=83/153 Noise level=13/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 03 - Address: 00:12:17:A6:E8:C8
ESSID: "linksys"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Signal level=81/153 Noise level=13/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 04 - Address: 00:12:17:79:CF:D3
ESSID:"linksysR79cfd3"
Mode:Master
Frequency:2.437 GHz (Channel 6)
```