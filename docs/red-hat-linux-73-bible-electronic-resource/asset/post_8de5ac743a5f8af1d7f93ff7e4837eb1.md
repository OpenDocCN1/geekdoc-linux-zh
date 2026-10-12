
**CROSS-REFERENCE:** DNS is discussed in Chapter 16. Configuring your own DNS server is described in Chapter 25.

If you did not identify your IP address during installation of Red Hat Linux, you can do so at a later time using the Network Configuration window (*neat* command). This procedure lets you attach a particular IP address to your Ethernet interface, so your computer knows what address to listen for, or get its name and address from a DHCP server.

**NOTE:** A computer can have more than one IP address because it can have more than one network interface. Each network interface must have an IP address (even if that address is assigned only temporarily). So, if you have two Ethernet cards on your computer (eth0 and eth1), each needs its own IP address. Also, the address 127.0.0.1 represents the local host, so users on the local computer can access services in loopback.

To define your IP address for your eth0 interface, follow this procedure:

- 1. Start the Network Configuration. As root user from a Terminal window, type *neat*. The Network Configuration window appears.
- 2. Click the Devices tab. A listing of your existing network interfaces appears.
- 3. Double-click the eth0 interface. A pop-up window appears, enabling you to configure your eth0 interface. Figure 15-8 shows the Network Configuration window and the pop-up Ethernet Device window configuring eth0.

![](img/1744bde8c889adfab3fc911e1687fecf_634_0.png)

**Figure 15-8:** Configure your LAN interface using the Network Configuration window.

- 4. Select “Activate device when computer starts” to have the network interface start at boot time.
- 5. Click the Protocols tab. You should at least see TCP/IP.
- 6. Click TCP/IP and select Edit. On the TCP/IP Settings window that appears, you can enter the following information:
  - **Automatically obtain IP address settings with:** Make sure that the check box is off next to this box if you are setting your own IP address. (If you were getting your IP address from a DHCP server, this box would be on and the rest of the information would be obtained automatically.)
  - **Address:** Type the IP address of this computer into the Address box. This number must be unique on your network.
  - **Subnet Mask:** Enter the netmask to indicate what part of the IP address represents the network. (Netmask is described earlier in this chapter.)
  - **Default Gateway Address:** If there is a computer or router connected to your LAN that is providing routing functions to the Internet or other network, type the IP address of the computer into this box.
- 7. Click OK in the TCP/IP Settings window to save the current configuration.
- 8. Click OK in the Ethernet Device window to close that window.
- 9. Click Apply in the Network Configuration window to apply the changes.

## Adding other host addresses

You can use the Network Configuration window to add host names and IP addresses to the Ethernet LAN for the computers on your network as well. This adds host name and IP address pairs to your /etc/hosts file (which you could also edit manually, if you prefer).

**NOTE:** If you are using a DHCP server to centralize assignments of your IP addresses, you probably want to centralize host name look-ups as well. In this way, you don't have to change every computer's /etc/hosts file every time a computer is added or removed from your network. Refer to Chapter 23 for information on how to do this.

To add host names and addresses, do the following:

- 1. Start the Network Configuration. As root user from a Terminal window, type neat. The Network Configuration window appears.
- 2. Click the Hosts tab. A list of IP addresses, host names, and aliases appears.
- 3. Click Add. A pop-up window appears asking you to add the IP address, host name, and aliases for a host that you can reach on your network. Figure 15-9 shows the Network Configuration window and the pop-up window for adding a host.

![](img/1744bde8c889adfab3fc911e1687fecf_636_0.png)

**Figure 15-9:** Add hosts to /etc/hosts using the Network Configuration.

- 4. Type in the IP address number, host name, and, optionally, the host alias.
- 5. Click OK.
- 6. Repeat this process until you have added every computer on your LAN.
- 7. Click Apply to apply the changes.
- 8. Click Close to exit.

Now, when you use programs such as ftp, ssh, or other TCP/IP utilities, you can use a host name to identify the computers that you want to communicate with. (Strictly speaking, you don’t have to set up your /etc/hosts file. You could use IP addresses as arguments to TCP/IP commands. But names are easier to work with.)

## Adding Windows computers to your LAN

It is likely that you have other types of computers on your LAN in addition to those running Red Hat Linux systems (at least for a few more years). The following are general steps for adding your Windows computers to the Ethernet LAN we just created:

- 1. Power down your computer and install an Ethernet card. (Most PC Ethernet cards will run on Windows.)
- 2. Connect an Ethernet cable from the card to your hub.
- 3. Reboot your computer. If your card is detected, Windows will either automatically install a driver or ask you to insert a disk that comes with the card to install the driver.
- 4. Open the Network configuration window (Start → Settings → Control Panel; then double-click the Network icon). The Network window appears.
- 5. Find the Ethernet card you just installed in the list and select it.
- 6. Click Add. The Select Network Component Type pop-up window appears.
- 7. Double-click Protocol. The Select Network Protocol window appears.
- 8. Click Microsoft, and then double-click TCP/IP. A new entry should appear in your Network window that looks similar to the following, depending on your card:
  `TCP/IP -> 3Com Etherlink III ISA`
- 9. Double-click on that new entry. The TCP/IP Properties window should appear, as shown in Figure 15-10.

![](img/1744bde8c889adfab3fc911e1687fecf_637_0.png)

**Figure 15-10:** Configure TCP/IP on Windows for your Ethernet LAN.

**NOTE:** Notice in the figure that the IP address is one of the reserved IP addresses described earlier. Because it is a Class A address, the Netmask is 255.0.0.0, which implies that there could be millions of computers on this network.

- 10. Click Specify an IP address.

**NOTE:** If you were using a DHCP server to assign IP addresses, you would click “Obtain an IP address automatically” instead. See Chapter 23 for information on setting up Red Hat Linux as a DHCP server.

- 11. Add the host name and IP address for this computer. (These should match the name and IP address that you added for this computer for Linux in your Network Configuration window.)
- 12. Click OK to exit.

At this point, your Windows computer knows to listen on the network (via its Ethernet card) for messages addressed to the IP address you have just entered. From the Windows system, you can access any of the following services configured on your Red Hat Linux system:

- **Printer server** — You can print to a printer connected to Linux that is configured as a Samba print server.
- **Web server** — You can display Web pages served from your Linux server via your Netscape Navigator, Internet Explorer, or other Web browser window.
- **File server** — You can find file folders shared from Linux (by using the Samba facility) and use them from your Network Neighborhood.

These are just a few examples of the types of services that can be accessed easily from your Windows system once the services have been properly configured on the Red Hat Linux server. (Most of the remaining chapters of this book describe how to configure these services.)

### Checking your Ethernet connection

After your LAN has been set up, your Ethernet cards installed, and host names and addresses added, there are several methods you can use to check that everything is up and working. For example, you can check your boot messages to make sure that your board was detected and that you can use the `ping` command to make sure you can connect to other computers.

### Did Linux find your Ethernet driver at boot time?

Type the following right after you boot your computer to check that Linux found your card and installed the Ethernet interface properly:

```bash
dmesg | grep eth
```

The `dmesg` command lists all the messages that were output by Linux at boot time. The `grep eth` command causes only those lines that contain the word *eth* to be printed. The first message shown below appeared on my laptop computer with the Netgear card. The second example is from my computer with the EtherExpress Pro/100 card:

```
eth0: NE2000 Compatible: port 0x300, irq3, hw_addr 00:80:C8:8C:8E:49
eth0: OEM 182557/182558 10/100 Ethernet at 0xccc0, 00:90:27:4E:67:35,
IRQ 17.
```

The message in the first example shows that a card was found at IRQ3 with a port address of 0x300 and an Ethernet hardware address of 00:80:C8:8C:8E:49. In the second example, the card is at IRQ 17, the port address is 0xccc0, and the Ethernet address is 00:90:27:4E:67:35.

**NOTE:** If the eth0 interface is not found, but you know that you have a supported Ethernet card, check that your Ethernet card is properly seated in its slot.

### Can you reach another computer on the LAN?

Try communicating with another computer on the LAN. The `ping` command can be used to send a packet to another computer and to ask for a packet in return. You could give `ping`
