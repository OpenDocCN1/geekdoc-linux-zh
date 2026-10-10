necessarily be set up to service nonlocal requests reliably. Later in this chapter you will learn how to assign multiple name servers, if necessary.

+   * **IPv4 Address**—This is the IP address you’re assigning to your Ethernet card. It needs to be on the same subnet as your IPv4 gateway, as matched against your netmask. This was discussed in Chapter 21.
+   * **Netmask**—This is used to determine whether a packet’s destination is on the local network. Set the field to **255.255.255.0** for a Class C network, which is the most commonly used netmask in most home configurations. Consult your network administrator to make sure what this number should be.
+   * **Extra options to ifconfig**—You most likely won’t need to put anything in here unless you’re a power user looking to tweak the performance of your interface card. Anything you put in here, such as specifying particular media types or duplex modes, will be added to the ifconfig command line that sysinstall issues in the background. You learn more about this command in “Using ifconfig to Apply Network Settings,” later in this chapter.

After you’ve set all these options, select OK. The network settings will be applied to the card on the fly. Whatever you were doing in sysinstall continues—in this example, sysinstall connects to your selected FTP server. If the network configuration isn’t successful, there’s likely a problem with the network settings you entered, and you’ll have to go back in and troubleshoot your settings. If you’re in an enterprise network, ask your network administrator to give you the correct settings.

This process works in much the same way if you’re doing a first-time installation of FreeBSD. You are presented with this configuration screen early in the install process. If you’re doing a network installation, it will use the settings to pull down the system distribution.

# Copying with ISA Ethernet Cards

Most PCI Ethernet cards are very trouble free. All you really need to do, especially if you have one of the commonly used cards supported in the GENERIC kernel, is plug it in, power up the machine, and watch the kernel identify the card in the boot process:

```
fxp0: <Intel PLC 10/100 Ethernet> port 0xe000-0xe0ff mem
0xff8fe000-0xff8fefff irq 11 at device 8.0 on pci1
fxp0: Ethernet address 00:00:b7:c7:74:f1
fxp1: <Intel Pro 10/100B/100+ Ethernet> port 0xdf00-0xdf3f mem
0xff700000-0xff7fffff,0xff8f0000-0xff8fffff irq 11 at
device 9.0 on pci1
fxp1: Ethernet address 00:d0:b7:bd:5d:13
```