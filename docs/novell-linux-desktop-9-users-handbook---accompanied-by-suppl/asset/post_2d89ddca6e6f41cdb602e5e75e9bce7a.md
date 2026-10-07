
## CHAPTER 5: Configuring NLD Hardware and System Settings

## 5 Close Mouse Preferences Dialog

After you have completed your changes to the mouse configuration, you can close the Mouse Preferences dialog, click the Close button.

## 35 About Printing and NLD

NLD makes it easy for you to configure printers and manage your print jobs. This includes adding and removing printers (adding or removing printers requires the root password) and selecting paper size and paper tray options. You can also view and manage print jobs on the desktop.

Most printers (directly connected to the PC) are automatically installed during the NLD installation. You can change the configuration of an installed printer at any time, and you can add new printers as needed.

To be honest, printing from Linux/UNIX systems has not always been a picnic. However, NLD takes advantage of a printing system known as CUPS (Common UNIX System). CUPS makes it easy to add and configure printers that are attached directly to your computer or are made available to you by other computers on a network, such as others running NLD (or other flavors of Linux).

### NOTE
> CUPS is a portable print system, meaning that it isn't part of the operating system. It is designed to work "with" your operating system including NLD and other Linux distributions. (CUPS is also being developed for the Windows environment.) CUPS actually provides the software drivers for the printers that you want to use. For more information about CUPS and the printer driver download library, check out http://www.cups.org.

CUPS also makes it possible to connect to printers attached directly to the network using HP Direct technology (the printer basically has its own network card). And if you work in an environment where you can share printers with Microsoft Windows users, you can take advantage of SAMBA (a protocol that allows Linux systems to share files and printers with Windows systems). You certainly don't have to know much about SAMBA to take advantage of it. The Gnome Add Printer utility makes it easy for you to select a printer on a Windows workgroup or network and then helps you to configure the basic SAMBA settings to attach to the printer.

### NOTE
HP DirectJet technology is only one of the possible hardware solutions for connecting a printer to a network. However, it is the industry leader in terms of large network implementations. Other possibilities for smaller networks include the USB Fast Ethernet Print Server from D-link and Netgear's USB Mini Print Server.

### KEY TERM
CUPS—Short for Common UNIX Print System, CUPS provides the set of print drivers and the printing architecture that make it easy to configure printers and to print from Linux (such as NLD) and UNIX systems.

### KEY TERM
SAMBA—An open source protocol that duplicates the capability of Microsoft's SMB (Server Message Block) protocol. In simpler terms, SAMBA provides the bridge that allows Linux systems as NLD to talk to computers running Microsoft Windows (and SMB). This means that Linux systems can share files and printers transparently.

When you add a printer that is remote to your system (meaning on another computer on the network), you need certain information to complete the installation. In the case of CUPS printers (attached to other NLD or Linux computers), you need to know the URI (Uniform Resource Identification) for the printer. You can enter this information in two formats:

```
http://hostname:631/ipp/
```

or

```
ipp://hostname/ipp/
```

The hostname is the name given to the computer during installation. You need the hostname of the remote computer that is serving as the connection for the remote printer. You can quickly find the hostname of your computer or another NLD (Linux) computer by opening a terminal window (select Programs, System Tools, Terminal). The prompt in the terminal shows your username@hostname. Where the hostname is the name of the computer.

### NOTE
Unless you have a small office or home network of NLD or other systems and serve as the network administrator, you really need to talk to your network administrator and get some help setting up connections to remote printers on the network. The network administrator can even do this for you, saving you time and headaches.

In cases where you want to take advantage of a printer hosted by a Microsoft Windows-based computer on a small office or home network, you need to know the name of the Windows computer and the name of the workgroup that the Windows computer is a member of. You also need to know a username and password that has been set up on the Windows computer so that you can establish the connection to the remote printer.

You can add and configure printers (both local and remote) using the GNOME Add a Printer utility, which is accessed using the New Printer icon in the Printers window (which is opened using the Printers icon in the Settings dialog box). The GNOME Add Printer utility actually walks you through the steps of setting up a printer.

### NOTE
Printers identified during the NLD installation should be "preinstalled" on the system in most cases.

You do have the option of adding and deleting printers using the YaST configuration utility, available through the Administrator Settings. We will assume, however, in the printer information installation follows that, you are a typical user with access to the root password and will use the GNOME Add a Printer utility to connect to a printer.

One thing about printers: You can set up a local or network printer. A local printer is attached directly to your computer (by a cable). The printer can be attached as a parallel port (historically, the "typical" printing port on personal computers), a serial port (a communications port that can be used for other devices such as external modems), or a USB port (most computers have multiple USB ports). Many new printers make it possible to connect it to your computer via a USB port.

Make sure that you have the printer physically connected to the computer before you add the printer to the NLD configuration. Having the printer ready to go after it is set up via CUPS also allows you to immediately check your printer installation by printing a test page.

## 36 Add and Configure a Printer

The Settings dialog provides access to the Printers window, which is launched using the Printer icon in the Hardware pane. The Printers window allows you to add a printer, change a printer's settings, and open a printer's queue to view pending jobs.

## BEFORE YOU BEGIN

![](img/6e85ebc4ce06a64c82109523b60183ba_114_0.png)

## 3 Enter Root Password

![](img/6e85ebc4ce06a64c82109523b60183ba_114_1.png)

## 5 Select Printer Driver
![](img/6e85ebc4ce06a64c82109523b60183ba_114_2.png)

## 6 Configure New Printer Settings

### 1. Open Printers Window
In the Settings dialog box (select System, Personal Settings) double-click the Printers icon. The Printer window opens.

### 2. Start GNOME Add a Printer Utility
The Printers window shows currently installed printers. To add a printer with the GNOME Add a Printer Utility, double-click the New Printer icon.

### 3. Enter Root Password
The Run as Root dialog opens. Enter the root password and then click OK. The GNOME Add a Printer utility opens.

### 4. Select Printer Connection
On the Step 1 specify the connection for the printer. If the printer is a local user, select the Printer Port drop-down list to choose the port type (parallel, serial, or USB).

In cases where you have attached a new printer and the printer is listed in the detected printer list, select the Use a Detected Printer option button and then select the printer in the list.

If you just connected a new plug-and-play printer to your computer and you don't see it listed in the detected printer list, try rebooting the system and see whether the printer shows up after that.

If you are installing a network printer, select the Network Printer button. Use the drop-down list to select the connection type for the network printer:

- CUPS Printer (IPP)—Use this connection for network printers connected to other NLD or Linux systems on the network. If you select this connection type, you need the URI for the computer hosting the printer.
- Windows Printer (SMB)—Use this connection for network printers attached to PCs (or servers) running the Microsoft Windows operating system. You need the Windows computer name, the workgroup (or domain) name for the computer, and a username and password configured on the Windows computer.
