# Chapter 27 ✦ Running a File Servers 731

The Samba software package contains a variety of daemon processes, administrative tools, user tools, and configuration files. To do basic Samba configuration, start with the Samba Server Configuration window, which provides a graphical interface for configuring the server and settings to share.

Most of the Samba configuration you end up in the /etc/samba/smb.conf file. If you need to access features that are not available through the Samba Configuration window, you can edit /etc/samba/smb.conf by hand or use SWAT, a Web-based interface, to configure Samba.

Daemon processes consist of smbd (the SMB daemon) and nmbd (the NetBIOS name server). The smbd daemon makes the file-sharing and printing services you add to your Linux system available to Windows client computers. The Samba package supports the following client computers:

+   * Windows 9x
* Windows NT
* Windows ME
* Windows 2000
* Windows XP
* Windows for workgroups
* MS Client 3.0 for DOS
* OS/2
* Dave for Macintosh computers
* Samba for Linux

For administrative tools for Samba, you have several shell commands at your disposal: testpar and testprns, with which you can check your configuration files; smstatus, which tells you what computers are currently connected to your shared resources; and mblookup command, with which you can query computers.

Samba uses the NetBIOS service to share resources with SMB clients, but the underlying network must be configured for TCP/IP. Although other SMB hosts use TCP/IP, NetBEUI, and IPX/SPX to transport data, Samba for Linux supports only TCP/IP. Messages are carried between host computers with TCP/IP and are then handled by NetBIOS.

# Getting and Installing Samba

You can get Samba software in different ways, depending on your Linux distribution. Here are a few examples: