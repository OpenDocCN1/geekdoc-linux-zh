# Chapter 15 • Managing Network Connections

network names, which appear in the output following the string ESSID, so typing iwlist scan | grep ESSID will pare down the output.

iwconfig This utility connects and disconnects you from specific networks. It uses many options, and you may need to study its man page to understand it fully. In many cases, typing something like the following will do the trick:

```
iwconfig wlan0 ssid NoWires channel 1 mode key s:N1mP7mHNw
```

This example connects to the NoWires network running on channel 1 using the password N1mP7mHNw.

# OBTAINING WI-FI DRIVERS

Unfortunately, Linux driver support for Wi-Fi hardware is weak. If you don't see your Wi-Fi hardware when you try to configure it, you may need to track down suitable drivers. You can begin this task with a tool called lspci, which is described in Chapter 5, “Managing Hardware.” This command with no options to see a list of available hardware, and search that list for a wireless network adapter. For instance, your laptop's lspci outputs the following line:

```
0300.0 Network controller: Realtek Semiconductor Co., Ltd.m RTL8191SEVB Wireless LAN Controller (rev 10)
```

This line identifies the Wi-Fi adapter as a Realtek RTL8191SEVB. A search for Realtek's website turns up a driver; however, this driver has to be compiled locally, which is a topic that's beyond the scope of this book. You might not be lucky enough to find a driver in this way.

An alternative to a native Linux driver is to use a Windows driver. This unusual option is possible using a package called ndiswrapper(http://ndiswrapper.sourceforge.net/), which enables you to install Windows drivers in Linux. Unfortunately, not all distributions provide ndiswrapper in their standard package sets, but you can usually find a binary package in an add-on repository.

If all options fail, you may need to buy new networking hardware. Many USB Wi-Fi adapters are available, but you should research them to find one that has good Linux support. You can also replace the built-in adapters on some laptops.