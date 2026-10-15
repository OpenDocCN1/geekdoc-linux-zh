
FIGURE 22.5 Use the SWAT Shares page to set up sharing of a portion of your Linux file system.

![](img/e464b828c497c99e41f61d4c55f1c0db_554_0.png)

![](img/e464b828c497c99e41f61d4c55f1c0db_554_1.png)

FIGURE 22.6 Configure a Samba share by editing the share defaults.

## Network and Remote Printing with Ubuntu

Chapter 12, “Printing with Ubuntu,” discussed how to set up and configure local printers and the associated print services. This section covers configuring printers for sharing and access across a network.

Offices all over the world benefit from using print servers and shared printers. In my office, I have two printers connected to the network via a Mac mini with Ubuntu PPC so that my wife can print from downstairs using a wireless link, and I can print from my three computers in my office. It is a simple thing to do and can bring real productivity benefits, even in small settings.

### Creating Network Printers

Setting up remote printing service involves configuring a print server and then creating a remote printer entry on one or more computers on your network. This section introduces a quick method of enabling printing from one Linux workstation to another Linux computer on a LAN. You also learn about SMB printing using Samba and its utilities. Finally, this section discusses how to configure network-attached printers and use them to print single or multiple documents.

### Enabling Network Printing on a LAN

To set up printing from one Linux workstation to another across a LAN, you need root permission and access to both computers, but the process is simple and easy to perform.

First, log in or ssh to the computer to which the printer is attached. This computer will be the printer server. Use the hostname or ifconfig commands to obtain the hostname or IP address and write down or note the name of the printer queue. If the system uses LPRng rather than CUPS, you need to edit the file named /etc/lpd.perms. Scroll to the end of the file and look for the remote permission entry:

```
# allow local job submissions only
REJECT SERVICE=X NOT SERVER
```

Remote printing is not enabled by default, so you must comment out the service reject line with a pound sign (#):

```
# allow local job submissions only
#REJECT SERVICE=X NOT SERVER
```

Save the file, and then restart the lpd daemon.

This enables incoming print requests with the proper queue name (name of the local printer) from any remote host to be routed to the printer. After you finish, log out and go to a remote computer on your LAN without an attached printer.

### TIP

LPRng, like CUPS, can be configured to restrict print services to single hosts, one or more specific local or remote users, all or part of a domain, or a LAN segment (by specifying an IP address range). An entry in /etc/lpd.perms, for example, to allow print requests only from hosts on 192.168.2.0, would look like this:

```
ACCEPT SERVICE=X REMOTEIP=192.168.2.0/255.255.255.0
```

The lpd.perms man page (included as part of the LPRng documentation) contains an index of keywords you can use to craft custom permissions. Don't forget to restart the lpd daemon after making any changes to /etc/lpd.perms (or /etc/lpd.conf).

If the computer with an attached printer is using Ubuntu and you want to set up the system for print serving, again use the gnome-cups-manager client to create a new printer.

To enable sharing, you must follow a few steps, because by default CUPS is not set up to share printers across a network.

First, edit your /etc/cups/cupsd.conf file using the following command:

```
$ sudo gedit /etc/cups/cupsd.conf
```

In this example I have used gedit, but feel free to substitute in your favorite text editor.

Then, look for the section that begins with <Location /> and modify it so that it reads as follows:

```
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
</Location>
```

This tells CUPS to share your printers across the network 192.168.0.*, for example. Make sure and change this to match your own network settings.

Next you need to edit the /etc/cups/cups.d/ports.conf file to tell CUPS to listen on a specific port.

Modify this line

```
Listen localhost:631
```

to this

```
Listen 631
```
