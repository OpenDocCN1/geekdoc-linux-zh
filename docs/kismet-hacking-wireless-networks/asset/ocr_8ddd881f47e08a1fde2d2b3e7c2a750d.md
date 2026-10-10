2.6.16 kernel revision, it is possible to build a Linux kernel with all of the support you need compiled into it. Depending on your personal preference, this can be done by either compiling support directly into the kernel or by building the appropriate kernel modules.

# Preparing the Kernel for Monitor Mode

There are several ways to generate a new kernel configuration, the easiest of which is probably using the *menuconfig* option.

```
# cd /usr/src/linux
# make menuconfig
```

Once the menu configuration opens, enable Generic IEEE 802.11 Networking Stack, IEEE 802.11 Wireless Encryption Protocol (WEP) encryption (802.1x), IEEE 802.11i Counter-Mode/CBC-Mac Protocol (CCMP) support, and IEEE 802.11i Temporal Key Integrity Protocol (TKIP) encryption:

```
Networking --->
    ---> Networking support
        Networking options --->
<>    Generic IEEE 802.11 Networking Stack
<>    IEEE 802.11WEP encryption (802.1x)
<>    IEEE 802.11i CCMP support
<>    IEEE 802.11i TKIP encryption
```

The 802.11i CCMP and TKIP support are not necessary for monitor mode; however, they are required for penetration testing of WiFi Protected Access (WPA)-encrypted networks.

Next, you need to configure your kernel to support your Wireless Fidelity (WiFi) card. Regardless of your type of card, you need the following options:

```
Device Drivers --->
Network device support --->
[*] Network device support

    Wireless LAN (non-hamradio) --->
[*] Wireless LAN drivers (non-hamradio) & Wireless Extensions
```

Next you need to compile in support for your specific card(s). First you need to decide if you want to compile your drivers into the kernel or install them as kernel