
# Part II: Ubuntu for Desktop Users

# FIGURE 22-6

Setting external program preferences for Wicd

![](img/1a233c34336fbf5a85d6eb785e401709_849_0.png)

# FIGURE 22-7

Configuring advanced settings for Wicd

![](img/1a233c34336fbf5a85d6eb785e401709_849_1.png)

## Command-Line Tools for Wireless Networking

The wireless-tools package, which is installed on Ubuntu systems by default, provides several commands for probing and configuring wireless interfaces and networks. You can execute the man wireless command to get information about the wireless-tools package, learn how and where it is installed by various Linux distributions, and view a list of the commands that this package provides.

The wireless-tools commands that I find most valuable are the iwconfig iwlist commands. The iwconfig command displays much more than the ifconfig command

```
$ iwconfig wlan0
wlan0      IEEE 802.11b/g SSID:"vwh" Nickname:"acx v0.3.36"
            Managed Frequency:2.437 GHz Access Point: 00:06:25:78:CE:3F
            Bit Rate:5.5 Mb/s Tx-Power:15 dbm Sensitivity:1/3
            Retry min limit:7 RTS thr:off
            Power Management:off
            Link Quality:31/100 Signal level=3/100 Noise level=0/100
            Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0
            Tx excessive retries:0 invalid misc:0 Missed beacon:0
```

As you can see, much of the information as provided by the ifconfig command, but it also includes wireless-specific information. The iwconfig command can also be used to set various wireless configuration options from the command line—see the online page for iwconfig (using the command man iwconfig) for more information.

The iwlist command enables you to scan for wireless networks and examine various characteristics of a wireless interface. For example, scanning for wireless networks around my home using the iwlist wlan0 scan displays the following information:

```
$ iwlist wlan0 scanning
wlan0      Scan completed:
            Cell 01   Address: 00:18:01:F4:0A:08
                       ESSID:"PY3N*"
                       Mode:Master
                       Frequency:2.462 GHz (Channel 11)
                       Quality:37/100 Signal level=12/100 Noise level=0/100
                       Encryption key:on
                       Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 6 Mb/s; 9 Mb/s
                              11 Mb/s; 12 Mb/s; 18 Mb/s; 24 Mb/s; 36 Mb/s
                              48 Mb/s; 54 Mb/s
            Cell 02   Address: 00:03:93:E9:89:22
ESSID: "vwh*"
Mode:Master
Frequency:2.427 GHz (Channel 4)
Quality=52/100 Signal level=34/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 6 MB/s; 9 MB/s
11 MB/s; 12 MB/s; 18 MB/s; 24 MB/s; 36 MB/s
48 MB/s; 54 MB/s

Cell 03 - Address: 00:06:25:78:CE:3F
ESSID: "vwh*"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Quality=57/100 Signal level=40/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
```

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
Signal level:49/153 Noise level:13/153
Encryption key:off
Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 18 Mb/s; 24 Mb/s; 36 Mb/s; 54 Mb/s
```

As you can see, much of the information as provided by the ifconfig command, but it also includes wireless-specific information. The iwconfig command can also be used to set various wireless configuration options from the command line—see the online page for iwconfig (using the command man iwconfig) for more information.

The iwlist command enables you to scan for wireless networks and examine various characteristics of a wireless interface. For example, scanning for wireless networks around my home using the iwlist wlan0 scan displays the following information:

This command is useful for verifying that a wireless interface is actually working and that it can communicate with an access point. The information provided by iwlist command is useful in public areas, where you will usually detect more wireless networks, as in the following example from one of my laptops while I was on vacation:

As you can see, much of the information as provided by the ifconfig command, but it also includes wireless-specific information. The iwconfig command can also be used to set various wireless configuration options from the command line—see the online page for iwconfig (using the command man iwconfig) for more information.

The iwlist command enables you to scan for wireless networks and examine various characteristics of a wireless interface. For example, scanning for wireless networks around my home using the iwlist wlan0 scan displays the following information:

## Installing Microsoft Windows Drivers

This section explains how to install Microsoft Windows drivers using the graphical ndisgtk utility, which puts a friendly wrapper around the ndiswrapper utilities, kernel module, and Ubuntu network configuration. You can also install Windows drivers for use with the ndiswrapper kernel module by using the command sudo ndiswrapper -i name-of-INF-file from any command-line environment and then manually modifying some configuration files, but I prefer the graphical one-stop-shopping approach provided by the ndisgtk utility.
