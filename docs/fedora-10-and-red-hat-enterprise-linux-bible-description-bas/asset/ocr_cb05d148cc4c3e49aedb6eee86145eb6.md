# Configuring Print Servers

You've configured a printer so that you and the other users on your computer can print to it. Now you want to share that printer with other people in your home, school, or office. Basically, that configuring your computer as a print server.

The printers that are configured on your Linux system can be shared in different ways with other computers on your network. Not only can your computer act as a Linux print server, it can also look to client computers like an SMB print server. In other words, a Windows client would just use your printer as a printer from another Windows machine.

After a local printer is attached to your Linux system, and your computer is connected to your local network, you can use the procedures in this section to share it with client computers using Linux (UNIX) or SMB interface.

> CROSS-REFERENCE: See Chapter 26 for information on configuring Linux as an AppleTalk server package.

# Configuring a shared CUPS printer

After a local printer is added to your Linux computer, making it available to other computers on your network is fairly easy. A TCP/IP network connection exists among the computers sharing your printer, you can simply grant permission to individual hosts or from remote hosts to access your computer's printing service. The procedures for setting up local printers are discussed earlier in this chapter.

To share a local printer as a print server with other computers on your network, do the following:

+   1. From the desktop panel, select System -> Administration -> Printing. The Printer configuration window opens.
2. Right-click the icon of the printer you want to share. (If the printer is not yet configured, refer to the "Setting Up Printers" section earlier in this chapter.)
3. Select the Share box on the menu to select appears in the box.
4. If you only selected users to access your printer, select Properties from the menu and then on the Access Control item. Select Deny printing for everyone except these users, type each user you want to allow to use the printer, and Click Add to add each selected users to be excluded from denied and allowed to print.
5. Select Settings from the Server menu at the top of the Printer configuration window. From the Basic Server Settings screen that appears, select the Publish printers connected to this system check box.
6. Click OK to make the changes permanent.