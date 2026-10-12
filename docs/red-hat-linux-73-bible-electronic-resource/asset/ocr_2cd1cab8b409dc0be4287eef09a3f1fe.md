+   * **Printer server** — You can print to a printer connected to Linux that is configured as a Samba print server.
+   * **Web server** — You can display Web pages served from your Linux server via your Netscape Navigator, Internet Explorer, or other Web browser window.
+   * **File server** — You can find file folders shared from Linux (by using the Samba facility) and use them from your Network Neighborhood.

These are just a few examples of the types of services that can be accessed easily from your Windows system once the services have been properly configured on the Red Hat Linux server. (Most of the remaining chapters of this book describe how to configure these services.)

# ## Checking your Ethernet connection

After your LAN has been set up, your Ethernet cards installed, and host names and addresses added, there are several methods you can use to check that everything is up and working. For example, you can check your boot messages to make sure that your board was detected and that you can use the `ping` command to make sure you can connect to other computers.

# ## Did Linux find your Ethernet driver at boot time?

Type the following right after you boot your computer to check that Linux found your card and installed the Ethernet interface properly:

```
```bash
dmesg | grep eth
```
```

The `dmesg` command lists all the messages that were output by Linux at boot time. The `grep eth` command causes only those lines that contain the word *eth* to be printed. The first message shown below appeared on my laptop computer with the Netgear card. The second example is from my computer with the EtherExpress Pro/100 card:

```
```
eth0: NE2000 Compatible: port 0x300, irq3, hw_addr 00:80:C8:8C:8E:49
eth0: OEM 182557/182558 10/100 Ethernet at 0xccc0, 00:90:27:4E:67:35,
IRQ 17.
```
```

The message in the first example shows that a card was found at IRQ3 with a port address of 0x300 and an Ethernet hardware address of 00:80:C8:8C:8E:49. In the second example, the card is at IRQ 17, the port address is 0xccc0, and the Ethernet address is 00:90:27:4E:67:35.

> > **NOTE:** If the eth0 interface is not found, but you know that you have a supported Ethernet card, check that your Ethernet card is properly seated in its slot.

# ## Can you reach another computer on the LAN?

Try communicating with another computer on the LAN. The `ping` command can be used to send a packet to another computer and to ask for a packet in return. You could give `ping`