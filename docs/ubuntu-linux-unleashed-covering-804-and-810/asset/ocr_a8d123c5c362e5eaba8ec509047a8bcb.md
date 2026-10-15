# Network and Remote Printing with Ubuntu

Chapter 8, "Printing with Ubuntu," discussed how to set up and configure local printers and the associated print services. This section covers configuring printers for sharing and access across a network.

Offices all over the world benefit from using print servers and shared printers. In my office, I have two printers connected to the network via a Mac mini with Ubuntu PPC so that my wife can print from downstairs using a wireless link, and I can print from my three computers in my office. It is a simple thing to do and can bring real productivity benefits, even in small settings.

# Creating Network Printers

Setting up remote printing service involves configuring a print server and then creating a remote printer entry on one or more computers on your network. This section introduces a quick method of enabling printing from one Linux workstation to another Linux computer on a LAN. You also learn about SMB printing using Samba and its utilities. Finally, this section discusses how to configure network-attached printers and use them to print single or multiple documents.

# Enabling Network Printing on a LAN

If the computer with an attached printer is using Ubuntu and you want to set up the system for print serving, again use the system-config-printer client to create a new printer.

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
```