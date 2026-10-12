
tenths of a second. Each successive timeout causes the timeout value to be doubled (up to 60 seconds maximum). You should increase this value if you believe that timeouts are occurring because of slow response from the server or a slow network.

- `retrans=#` — Sets the number of minor retransmission timeouts that occur before a major timeout. When a major timeout occurs, the process is either aborted (soft mount) or a Server Not Responding message appears on your console.
- `retry=#` — Sets how many minutes to continue to retry failed mount requests, where # is replaced by the number of minutes to retry. The default is 10,000 minutes (which is about one week).
- `bg` — If the first mount attempt times out, try all subsequent mounts in the background. This option is very valuable if you are mounting a slow or sporadically available NFS file system. By placing mount requests in the background, Red Hat Linux can continue to mount other file systems instead of waiting for the current one to complete.

> **NOTE:** If a nested mount point is missing, a timeout to allow for the needed mount point to be added occurs. For example, if you mount `/usr/trip` and `/usr/trip/extra` as NFS file systems, if `/usr/trip` is not yet mounted when `/usr/trip/extra` tries to mount, `/usr/trip/extra` will time out. Hopefully, `/usr/trip` will come up and `/usr/trip/extra` will mount on the next retry.

- `fg` — If the first mount attempt times out, try subsequent mounts in the foreground. This is the default behavior. Use this option if it is imperative that the mount be successful before continuing (for example, if you were mounting `/usr`).

Any of the values that don’t require a value can have `no` appended to it to have the opposite effect. For example, `nobg` indicates that the mount should not be done in the background.

## Unmounting NFS file systems

After an NFS file system is mounted, unmounting it is simple. You use the `umount` command with either the local mount point or the remote file system name. For example, here are two ways you could unmount `maple:/tmp` from the local directory `/mnt/maple`.

```
# umount maple:/tmp
# umount /mnt/maple
```

Either form will work. If `maple:/tmp` is mounted automatically (from a listing in `/etc/fstab`), the directory will be remounted the next time you boot Red Hat Linux. If it was a temporary mount (or listed as `noauto` in `/etc/fstab`), it will not be remounted at boot time.

> **TIP:** If you get the message “device is busy” when you try to unmount a file system, it means that the unmount failed because the file system is being accessed. Most likely, one of the directories in the NFS file system is the current directory for your shell (or the shell of someone else on your system). The other possibility is that a command is holding a file open in the NFS file system (such as a text editor). Check your Terminal windows and other shells, and `cd` out of the directory if you are in it, or just close the Terminal windows.

## Other cool things to do with NFS

You can share some directories to make it consistent for a user to work from any of several different Linux computers on your network. Some examples of useful directories to share are:

- `/var/spool/mail` — By sharing this directory from your mail server, and mounting it on the same directory on other computers on your network, users can access their mail from any of those other computers. This saves the user from having to download messages to their current computer or from having to log in to the server just to get mail. There is only one mailbox for each user, no matter where it is accessed.
- `/home` — This is a similar concept to sharing mail, except that all users have access to their home directories from any of the NFS clients. Again, you would mount `/home` on the same mount point on each client computer. When the user logs in, that user has access to all the user’s startup files and data files contained in the `/home/user` directory.

> **TIP:** If your users rely on a shared `/home` directory, you should make sure that the NFS server that exports the directory is fairly reliable. If `/home` isn’t available, the user may not have the startup files to log in correctly, or any of the data files needed to get work done. One workaround is to have a minimal set of startup files (`.bashrc`, `.xdefaults`, and so on) available in the user’s home directory when the NFS directory is not mounted. Doing so allows the user to log in properly at those times.

- `/project` — Although you don’t have to use this name, a common practice among users on a project is to share a directory structure containing files that people on the project need to share. This way everyone can work on original files and keep copies of the latest versions in one place.
- `/var/log` — An administrator can keep track of log files from several different computers by mounting the `/var/log` file on the administrator’s computer. (Each server may need to export the directory to allow root to be mapped between the computers for this to work.) If there are problems with a computer, the administrator can then easily view the shared log files live.

If you are working mostly with Red Hat Linux and other UNIX systems, NFS is probably your best choice for sharing file systems. If your network consists primarily of MS Windows computers, you may want to look into using Samba for file sharing.

## Setting up a Samba File Server in Red Hat Linux

Samba is a software package that comes with Red Hat Linux that lets you share file systems and printers on a network with computers that use the Session Message Block (SMB) protocol.

SMB is the protocol that is delivered with Windows operating systems for sharing files and printers. Although you can't always count on NFS being installed on Windows clients (unless you install it yourself), SMB is always available (with a bit of setup).

On the Red Hat Linux side, the Samba software package contains a variety of daemon processes, administrative tools, user tools, and configuration files. The work you need to do with Samba centers on the `/etc/samba/smb.conf` file. You can either edit `/etc/samba/smb.conf` by hand or use the SWAT program (which runs in a browser window) to set up the file.

Daemon processes consist of `smbd` (the SMB daemon) and `nmbd` (the NetBIOS name server). `smbd` is what makes the file sharing and printing services you add to your Red Hat Linux computer available to Windows client computers. The client computers this package supports include:

- Windows 9x
- Windows 2000
- Windows NT
- Windows ME
- Windows XP
- Windows for Workgroups
- MS Client 3.0 for DOS
- OS/2
- Dave for Macintosh Computers
- Samba for Linux

As for administrative tools for Samba, there are several shell commands that you can use. You can check your configuration file using the `testparm` and `testprns` commands. The `smbstatus` command will tell you which computers are currently connected to your shared resources. Using the `nmblookup` command, you can query for NetBIOS names (the names used to identify host computers in Samba).

Although Samba uses the NetBIOS service to share resources with SMB clients, the underlying network must be configured for TCP/IP. Although other SMB hosts can use TCP/IP, NetBEUI, and IPX/SPX to transport data, Samba for Linux supports only TCP/IP. Messages are carried between host computers with TCP/IP and are then handled by NetBIOS.

## Getting and installing Samba

To see if Samba is installed on your Red Hat Linux system, type the following:

```
# rpm -qa | grep samba
samba-*
samba-swat-*
samba-common-*
samba-client-*
```

You should see the name of each of the four packages above, followed by the version number (I just represented version numbers with an asterisk above). Although not installed with all installation groups in Red Hat Linux, the packages that make up Samba are spread across all three Red Hat Linux CD-ROMs. To install Samba from the CD, mount the first CD and run `rpm` as follows:

```
# mount /mnt/cdrom
# cd /mnt/cdrom/RedHat/RPMS
# rpm -ivh samba*
# umount /mnt/cdrom; cd
```

Repeat the procedure above for the other two CDs. If you prefer, you can obtain the latest version of Samba from www.samba.org. An rpm that is more recent than the one on the Red Hat CD may be available. (Follow the download links from the Samba Web site to obtain the Samba rpm.) A lot of documentation comes with Samba. Before you start trying to configure Samba, read the README file (probably located in `/usr/share/doc/samba*`). It provides a good overview of the SMB protocol and Samba.

## Quick-starting Samba

> **CAUTION**: This procedure is primarily for people who are trying out Samba for the first time in a secure environment. If you are using Samba in an environment that contains critical data and is accessible from the Internet, I urge you to consider more stringent security measures. Read the more complete descriptions of Samba in the rest of this section and refer to documents in the `/usr/share/doc/samba*/docs/` directory for information on security.

The procedure in this section steps you through an example of a Red Hat Linux system configured as a Samba server. In this example, the Linux Samba server uses “user” security to share home directories and printers with users from Windows workstations on the local LAN. The procedure consists of three basic steps:

1. Editing the smb.conf file.
2. Adding Samba users.
3. Starting the Samba service.

## Editing the smb.conf file

Using either SWAT (described in the "Configuring Samba with SWAT" section) or a regular text editor (as root user), create an `/etc/samba/smb.conf` file. Here is an example of an `smb.conf` file (with comment lines removed) that can be used to share printers and directories with several Windows systems on a single LAN:
