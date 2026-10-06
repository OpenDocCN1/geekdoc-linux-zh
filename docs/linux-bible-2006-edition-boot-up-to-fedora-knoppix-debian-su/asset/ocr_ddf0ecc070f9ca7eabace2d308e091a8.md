# Chapter 5 ╣ Getting on the Internet   185

10. Click File↔ Save to save the changes.

11. Click File↔ Quit to exit.

Now, when you use programs such as ftp, ssh, or other TCP/IP utilities, you can use any host name that is identified by your local computer, exists in your search path, or can be resolved from the public Internet DNS servers. (Strictly speaking, you don't have to set up your /etc/hosts file. You could use IP addresses as arguments to TCP/IP commands. But names are easier to work with.)

# Understanding Your Internet Connection

If your Ethernet interface to the Internet is not working, there are ways to check what's happening that will work on many Linux distributions. Use the following procedure to find out how network interfaces are working:

+   1. Open a shell (if you are using a graphical interface, open a Terminal window).

+   2. Type the following right after you boot your computer to verify whether Linux card was found and installed the Ethernet interface properly:
dmesg | grep eth | less
dmesg command lists all the messages that were output by Linux at boot. The grep eth command shows those lines that contain the word eth to be. Here are a couple of examples:

```
eth0 NE2000 Compatible: port 0x300, irq3, hw_addr 00:80:8C:8E:49
eth0 OEM 18255/18258 10/10 Ethernet at 0x0cc0, 00:90:27:46:67:35, IRQ 17.
```

The first message appears on my laptop computer with the Netgear card. It shows that a card was found at IRQ3 with a port address of 0x300 and an Ethernet hardware address of 00:80:8C:8E:49. The second example is from my computer with the EthernetExpress Pro/100 card. In this, it is IRQ 17, the port address is 0x0cc0, and the Ethernet address is
00:90:27:46:67:35.

If the eth interface is not found, know that you have a supported Ethernet card, type lspci -vi | grep eth to see if the Ethernet was detected on the PCI bus. if it doesn't appear, check that your Ethernet card is properly seated in its slot.

+   3. To view how network interfaces are up, run the following:

```
$ /sbin/ifconfig -
eth0 Link enc:Ethernet Haddr 00:00:B7:66:9A:46
inet addr:10.0.0.5 Bcast:10.0.0.255 Mask:255.255.255.250
 BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:326610 errors:0 dropped:0 overflows:0 frame:0
TX packets:215931 errors:0 dropped:0 overflows:0 carrier:0
collisions:5919
RX bytes:168378315 (160.5 MB) TX bytes:408533243 (38.9 MB)
```

![](bbox=[0.1, 0.705, 0.17, 0.755])