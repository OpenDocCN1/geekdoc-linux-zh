
# Part IV: Fedora RHEL Network and Server Setup

## Setting Up a File Server

Samba is a software package that comes with Fedora, RHEL, and other Linux systems. Samba enables you to share files and printers on computers that use the Server Message Block (SMB) or Common File System (CIFS) protocols. SMB is the Microsoft protocol that is delivered with Windows operating systems for sharing files and printers. CIFS is an open, cross-platform protocol that is based on SMB. Samba contains free implementations of SMB and CIFS. Although you can't have NFS on Windows (unless you install yourself), SMB is always available (with a bit of setup). If Samba is not currently installed on Linux, refer to the "Getting and Installing Samba" section.

On Fedora or RHEL, the Samba package contains a variety of daemon processes, administrative tools, and configuration files. To do basic Samba configuration, you can start with the Server Configuration window. This window provides a graphical interface for configuring the server and setting directories to share. Most of the Samba configuration ends up in the `/etc/samba/smb.conf` file. If you need to access features that are not available through the Server Configuration window, you can edit `/etc/samba/smb.conf` by hand or use SWAT, a Web-based interface to configure Samba.

Daemon processes consist of smbd (the SMB daemon) and nmbd (the NetBIOS server). The smbd daemon makes the file sharing and printing services you add to your Linux system available to Windows client computers. This package supports:
- Windows 9x
- Windows 2000
- Windows Server 2003
- Windows NT
- Windows ME
- Windows XP
- Windows Vista
- Windows for Workgroups
- Windows for DOS
- OS/2
- Windows Macintosh
- Mac OS X
- Linux

As administrative tools for Samba, you have several shell commands at your disposal. You can check your configuration file using the testparm command. The smbstatus command tells you which computers are currently connected to your shared resources. Using the nmblookup command, you can query for NetBIOS names (theBIOS names used to identify host computers). Because SMB is considered a Windows technology, some of the terms used to describe Samba sound more Windows than Linux. For example, a shared directory or file system is often referred to as a share.

Although Samba uses the NetBIOS service to share resources with SMB clients, the underlying network must be configured for TCP/IP. Other SMB hosts use TCP/IP, NetBEUI, and IP/SPX to transport data; Samba for Linux supports only TCP/IP. Messages are carried between computers with TCP/IP and are then handled by NetBIOS.

If you are working extensively with Fedora, Red Hat Enterprise Linux, and other Linux and UNIX systems, NFS is probably your best choice for sharing file systems. If your network consists primarily of Microsoft Windows computers or a combination of systems, you may want to look into Samba for sharing.

the same mount point on each client computer. When the user logs in, user has access to the user's start-up files and data files contained in the `/home/user` directory.

> TIP: If users rely on shared /home directory, you should make sure that the NFS server exports the directory is fairly reliable. If /home isn't available, the user may not have the start-up files to log in correctly, or any of the data files needed to get work done. One workaround is to have a minimal set of start-up files (.bashrc, .xexports, and so on) available in the user's home directory when the NFS directory is mounted. Doing so allows the user to log in properly at those times.

- project - Although you don't have to use this, a common practice among users on a project is to share a directory containing files that the project needs to share. everyone can work on original files and keep copies of the latest versions in one. (Of, a better way to manage a project is with CVS or some other control-type software; this is a simple workaround.)
- /var/log — An administrator can keep track of log files from several computers by mounting the `/var/log` file on the administrator's computer. (Each server may need to export the directory to be mapped between the computers for this work.) If there are problems with a computer, the administrator can easily view the shared log files live.

## Getting and installing Samba

To see if Samba is installed on your Fedora or RHEL system, type the following:

```bash
# rpm -qa | grep samba
samba-*
system-config-samba
samba-swat-*
samba-common-*
samba-client-*
samba-winbind-*
```

You should see the name of each of these packages, followed by the version number (I represented version numbers with asterisk). Although not installed with installation groups in Fedora and RHEL, the packages that make Samba are all included on the DVD that comes with this book. To install Samba, insert the DVD. Then run the following (note that the device may have a name other than `cdrecorder` and that you can skip the first step if it mounts automatically):

```bash
# mount /media/cdrecorder
# cd /media/cdrecorder/Fedora/RPMS
# rpm -Uv samba*
```

If you have an Internet connection, you could try yum install samba. Before you start to configure Samba, read the README file (located in `/usr/share/doc/samba*/`). It provides a good overview of the SMB protocol and Samba.

> NOTE: The expanded Fedora software repository, other useful tools for working with Samba are now available. The samba4 package lets you search for shared SMB/CIFS resources and mount them on your computer. The fuse-smamba package lets you find and browse SMB shares on your network.

## Configuring a simple Samba server

The Server Configuration window enables you to do a basic Samba configuration and then identify which directories you want to share. To make this procedure useful, I'm setting up a particular type of shared environment (which you can modify later if you prefer). Here are the characteristics:
- A single local area network — Contains multiple Windows and Linux machines.
- User-level security — Any user who wants to share the Samba files must have a valid login and password on the Linux Samba server.
- Encrypted passwords — Many clients use encrypted passwords with Samba (SMB) by default. I'll describe how to turn on encrypted passwords for clients that don't use encrypted passwords.
- A guest user account — The guest user account will be useful later, so you can set up Samba to let users without special accounts the server’s printers via Samba.

The following procedure describes how to configure Samba and create a shared directory in Samba:

1. To open the Samba Server Configuration window, click System -> Administration -> Samba. The Server Configuration window opens. (You will likely need to enter the root password.)
2. Click Preferences -> Server Settings. The Server Settings window appears, as shown in Figure 18-3.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_820_0.png)

Figure 18-3: Define the workgroup and description for your Samba server.

3. Type the workgroup name (to match that of other computers with which you want to share files) and a short description.
4. Click the Security tab. A window appears like the one shown in Figure 18-4.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_820_1.png)

Figure 18-4: Fill in Security information for your Samba tab and click OK:
5. Provide the following information for the fields on the Security tab and click OK:
* Authentication Mode — Select User, Share, Server, ADS (Active Directory Service), or Domain. For this example, I selected User. (See the "Security options" section later in this chapter for details on each of the authentication modes.)
