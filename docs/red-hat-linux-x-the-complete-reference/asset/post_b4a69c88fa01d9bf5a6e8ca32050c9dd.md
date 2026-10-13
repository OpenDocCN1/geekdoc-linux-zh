
corresponding options. The smbmount command takes as its arguments the Samba server and shared directory, followed by the local directory where you want to mount the directory. The following example mounts the myreports directory onto the /mnt/myreps directory on the local system:

```
smbmount //turtle.mytrek.com/myreports /mnt/myreps -U dylan
```

To unmount the directory, use the smbumount command with the local directory name, as shown here:

```
smbumount /mnt/myreps
```

To mount the home directory of a particular user on the server, specify the homes service and the user's login name. The following example mounts the home directory of the user larisa to the /home/chris/larisasstuff directory on the local system:

```
smbmount //turtle.mytrek.com/homes /home/chris/larisasstuff -U larisa
```

You can also use smbmount to mount shared folders on Windows clients. Just specify the computer name of the Windows client along with its folder. If the folder name contains spaces, enclose it in single quotes. In the following example, the user mounts the windata folder on lizard as the /mylinux directory. For a folder with access to anyone, just press ENTER at the password prompt.

```
$ smbmount //lizard/windata /mylinux
Password:
$ ls /mylinux
_hi_mynewdoc.doc_myreport.txt
```

To unmount the shared folder when you are finished with it, use the smbumount command.

```
smbumount /mylinux
```

Instead of using smbmount explicitly, you can use the mount command with the file system type smbfs. mount will then run the /sbin/mount.smbfs command, which will invoke smbclient to mount the file system:

```
mount -t smbfs //lizard/windata /mylinux
```

You could also specify a username and password as options, if user-level access is required:

```
mount -t smbfs -o username=chris passwd=mypass //lizard/windata /mylinux
```

You can also use the smbfs type in an /etc/fstab entry to have a Samba file system mounted automatically:

```
//lizard/windata /mylinux smbfs defaults 0 0
```

## Sharing Windows Directories and Printers with Samba Clients

To manage directory shares, open the Computer Management tool in the Administrative window in the Control Panel. Click Shared Folders and there you can see the Shares, Sessions, and Open folders. To add a new share, click the Shares folder and then click the Action menu and select New File Share. The Sessions and Open folders' Action menus let you disconnect active sessions and folders.

To allow share-level open access by users on other clients or on the Samba server, be sure to enable the guest user on your Windows client. It is not enabled by default. Access the Users and Passwords tool in the Control Panel to set up the guest user. Guest access is particularly important for providing access to a printer connected to a Windows client. The Linux system that wants to access a printer on a Windows system will configure the printer on its own system as a remote Samba printer. The user normally entered to access the printer is guest. For the Linux system to access the Windows printer, that Windows system has to have a guest user.

### Sharing Windows Directories

To share a directory, right-click the directory and select Sharing from the pop-up menu (Sharing And Security on Windows XP). Click Share This Folder and then enter the share name, the name by which the directory will be known by Samba. You can specify whether you want to allow others to change files on the share. You can also specify a user limit (maximum allowed is the default). You can further click the Permissions button to control access by users. Here, you can specify which users will have access, as well as the type of access. For example, you could allow only read access to the directory.

### Sharing Windows Printers

To share a printer, locate the printer in the Printers window and right-click it, selecting the Sharing As option. This opens the Sharing panel, where you can click the Shared As button and enter the name under which the printer will be known by other hosts. For example, on the Windows client named lizard, to have a printer called Epson Stylus Color shared as myepson, the Sharing panel for this printer would have the Shared As button selected and the name myepson entered. Then when the user double-clicks the lizard icon in the Computers Near Me window, the printer icon labeled myepson will appear.

For a Linux system to use this printer, it will have to be first configured as a remote Windows printer on that Linux system. For printers using the LPRng print server, you can do this easily with redhat-config-printer (Printing on the System Settings menu and window), and for printers using the CUPS print server, you use the CUPS Print Configuration tool (Extra System Tools menu).

To configure your remote printer, you give the printer a name by which it is known on your Linux system, the Windows client computer name, the name of the printer as it is accessed on the Windows client, along with the username for access (usually guest). Once configured, your printing commands can access it using just the printer name, as they would any other printer. For example, the myepson printer installed on the Windows client has to also be installed for CUPS on the Linux system operating as the Samba server. For the CUPS print server, you can use redhat-config-printer to configure your Windows printer. You can give the printer the same name, if you wish, and then in the Queue Type panel select Windows Printer (SMB). For the Share, you enter //lizard/myepson; for User, enter guest; and for Workgroup, enter the Windows client's workgroup (usually WORKGROUP).

For the CUPS print server, you can also use the CUPS Print Configuration tool and add the printer. For device, select Windows Printer via Samba. For the device URL, enter the share name with the smb: protocol, smb://lizard/myepson. Also, to enable CUPS to use Samba, you need to link the samba spool directory to the CUPS smb directory.

```
ln -s /usr/bin/smbspool  /usr/lib/cups/backend/smb
```

Once it is installed, you can restart the CUPS server. Then an lpr command can access the remote Windows printer directly. The next example prints the mydoc file on the Windows client's Epson printer.

```
lpr -P myepson mydoc
```

### Windows Clients

To access Samba resources from a Windows system, you will need to make sure that your Windows system has enabled TCP/IP networking. This may already be the case if your Windows client is connected to a Microsoft network. If you need to connect a Windows system directly to a TCP/IP network that your Linux Samba server is running on, you should check that TCP/IP networking is enabled on that Windows system. This involves making sure that the Microsoft Network client and the TCP/IP protocol are installed, and that your network interface card (NIC adapter) is configured to use TCP/IP. The procedures differ slightly on Windows 2000 and XP, and Windows 95, 98, and ME.

Once connected, your Samba shares and printers will appear in the Windows network window. If you are going to use a share frequently, you can assign it a disk label. Right-click the share and select Map Network Drive, and select the drive label you want to use. On XP, you can further select whether you want the drive automatically mounted when you log in. Follow the instructions on your particular Windows system for accessing remote shared resources such as printers and directories.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_924_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abcchm.html

## Chapter 38: Administering TCP/IP Networks

### Overview

Linux systems are configured to connect into networks that use the TCP/IP protocols. These are the same protocols that the Internet uses, as do many local area networks (LANs). In Chapter 19, you were introduced to TCP/IP, a robust set of protocols designed to provide communications among systems with different operating systems and hardware. The TCP/IP protocols were developed in the 1970s as a special DARPA project to enhance communications between universities and research centers. These protocols were originally developed on Unix systems, with much of the research carried out at the University of California, Berkeley. Linux, as a version of Unix, benefits from much of this original focus on Unix. Currently, the TCP/IP protocol development is managed by the Internet Engineering Task Force (IETF), which, in turn, is supervised by the Internet Society (ISOC). The ISOC oversees several groups responsible for different areas of Internet development, such as the Internet Assigned Numbers Authority (IANA), which is responsible for Internet addressing (see Table 38-1). Over the years, TCP/IP protocol standards and documentation have been issued in the form of Request for Comments (RFC) documents. Check the most recent ones for current developments at the IETF Web site at www.ietf.org.
