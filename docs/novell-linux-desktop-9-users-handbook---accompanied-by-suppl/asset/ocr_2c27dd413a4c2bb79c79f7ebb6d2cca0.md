# 35 About Printing and NLD

# NOTE

HP DirectJet technology is only one of the possible hardware solutions for connecting a printer to a network. However, it is the industry leader in terms of large network implementations.Other possibilities for smaller networks include the USB Fast Ethernet Print Server from D-link and Netgear's USB Mini Print Server.

# KEY TERM

CUPS—Short for Common UNIX Print System, CUPS provides the set of print drivers and the printing architecture that make it easy to configure printers and to print from Linux (such as NLD) and UNIX systems.

# KEY TERM

SAMBA—An open source protocol that duplicates the capability of Microsoft's SMB (Server Message Block) protocol.In simpler terms, SAMBA provides the bridge that allows Linux systems as NLD to talk to computers running Microsoft Windows (and SMB). This means that Linux systems can share files and printers transparently.

When you add a printer that is remote to your system (meaning on another computer on the network), you need certain information to complete the installation. In the case of CUPS printers (attached to other NLD or Linux computers), you need to know the URI (Uniform Resource Identification) for the printer. You can enter this information in two formats:

```
http://hostname:631/ipp/
```

or

```
ipp://hostname/ipp/
```

The hostname is the name given to the computer during installation. You need the hostname of the remote computer that is serving as the connection for the remote printer. You can quickly find the hostname of your computer or another NLD (Linux) computer by opening a terminal window (select Programs, System Tools, Terminal). The prompt in the terminal shows your username@hostname. Where the hostname is the name of the computer.

# NOTE

Unless you have a small office or home network of NLD or other systems and serve as the network administrator, you really need to talk to your network administrator and get some help setting up connections to remote printers on the network. The network administrator can even do this for you, saving you time and headaches.