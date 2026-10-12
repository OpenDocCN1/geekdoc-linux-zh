![](bbox=[0.28, 0.18, 0.95, 0.58])

Figure 2-2:
You can use an Ethernet hub to set up a 10BaseT Ethernet LAN.

When you install Red Hat Linux from this book’s companion DVD-ROM on a PC connected with an Ethernet card, the Red Hat installer should automatically detect the Ethernet card and install the appropriate drivers. The installer should also let you set up TCP/IP networking.

When properly installed, the Linux kernel should load the driver for the Ethernet card every time it boots. To verify that the Ethernet driver is loaded, type the following command in a terminal window:

```
dmesg | grep `grep eth0 /etc/modules.conf | cut -d ' ' -f 3`
```

This command searches the boot messages for any line that contains the name of the first Ethernet card (the command in backquotes — `grep eth0 /etc/modules.conf | cut -d ' ' -f 3` — picks out the alias for the eth0 device from the /etc/modules.conf file).

On my PC, I have an Intel Ethernet Pro 100 (e100) card installed, so I get the following output when I type that command on my system:

```
e100: selftest OK.
e100: eth0: Intel(R) PRO/100 WfM PCI Adapter
```

You should see something similar, showing the name of your Ethernet card and other parameters.