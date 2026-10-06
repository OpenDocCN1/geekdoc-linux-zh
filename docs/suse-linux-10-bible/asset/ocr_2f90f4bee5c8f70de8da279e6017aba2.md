# Chapter 9 ♦ Configuring the System with YaST 231

![](bbox=[0.191, 0.133, 0.68, 0.423])

Figure 9-7: Configuring an NTP server

It is customary to source your NTP synchronization to a secondary time server, and for primary servers to synchronize to secondary servers only for general use.

When configured, your machine will attempt to synchronize to the NTP server specified in the configuration window. If you want to synchronize to more than one server, select the Select Configuration button. Unless you are running a server that is extremely sensitive to time fluctuations, the default usually suffices.

> If you are running an SLP-aware NTP server in your network, clicking the Lookup button causes the system to attempt to discover an NTP service for you.

# Printer Configuration

One of the biggest things that annoyed Linux users in the past was the configuration of printers. In the Windows world, the addition of a printer is painless, but in Linux it seemed the process was always marred by problems with drivers and configuration options.

The Common Unix Printing System (CUPS) print drivers help to provide a unified printer architecture for Unix in general, and with distributions such as SUSE providing configuration front ends, the problems have become less apparent.