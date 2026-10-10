with the correct Linux kernel, and/or that your hardware is supported (by checking your distribution vendor's Web site).

![](bbox=[0.03, 0.13, 0.12, 0.2])

> SuSE, Inc. maintains an excellent hardware compatibility database and other information about its distributions. Start at http://www.suse.com.

# Creating Network Interfaces

Creating a network interface means configuring Linux to work with your hardware, and then properly assigning an IP (Internet Protocol) address to your card. You do not need to use a network interface if you only use your computer as a stand-alone workstation. When you connect to the Internet, a different kind of interface, known as a PPP (Point-to-Point Protocol) interface, is created.

Networking interfaces under Linux are created in memory, and are generally numbered and named in the order in which they are created. For example, the first PPP interface you create is named ppp0, while the first Ethernet interface you create will be named eth0.

# Using the netcfg Client

The netcfg client included with many Red Hat-based Linux systems may be used to create a variety of new network interfaces. Start the client (as root) from the command line, like this:

```
# netcfg &
```

After you press Enter, click the Interfaces button on the main dialog box. A new dialog box appears. Click the Add button, and you see a dialog box as shown in Figure 3.7. Select the desired interface, and then click the OK button. You are presented with an appropriate dialog box to further configure the interface.

# Using YaST2 and YaST

The SuSE Linux yast command and yast2 clients may be used to create new interfaces. For example, you can use yast to jump right into configuring a network interface from the command line, like this:

```
# yast --mask network
```

After you press Enter, you see a dialog box as shown in Figure 3.8.