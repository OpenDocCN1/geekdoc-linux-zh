# browseable

This parameter, if set to Yes, causes a share to appear in Network Neighborhood browse lists under Windows. It's generally best to set this parameter to Yes.

# create mask and ndirectory mask

These parameters set the permissions on files and directories that users create via Samba. In example, these are set at high values, so that all users can read and write each other's files. Of course, you may want to restrict permissions rather than expand them. The default values are 0744 and 0755, respectively.

There is a special name that deserves explicit mention: [homes]. If you use this share, you should omit the path parameter, and Samba provides a share that corresponds to the user's home directory. For instance, if Jennie logs onto the server, the share appears on the client as JENIE and shows the user's home directory files. This share is extremely useful and popular on servers for storing individual users' files (as opposed to shared printer programs).

In addition to file sharing, Samba supports printer sharing, as discussed in Chapter 13. The easiest way to enable printer sharing is to create a [printers] share, which should have the print ok = Yes parameter set. This causes Samba to share each of the printer queues defined in /etc/printcap. Because Linux printer queues are normally defined as PostScript printers, you should treat them as PostScript printers from the Windows clients.

> TIP Apple LaserJet drivers tend to work well with printers that use Ghostscript on Linux printing.

# Using Samba as a Client

Samba includes two clients: smclient and smbmount. The first of these is a program that allows you to perform file transfers in a manner similar to a text-mode FTP program. By contrast, smbmount allows you to mount a share on the Linux directory tree, which you can mount an NFS share using the mount command. (In fact, since Samba 2.0.6, you can use mount instead of smbmount.) There are also GUI front-ends to these packages, so that you can browse an SMB/CIFS network from Linux much as you can from Windows.

All of the Samba client programs rely upon settings in the [global] section of smb.conf to control aspects of their operation, such as the claimed NetBIOS and group names of the computer. You should therefore be sure these features are set correctly before using Samba as a client.