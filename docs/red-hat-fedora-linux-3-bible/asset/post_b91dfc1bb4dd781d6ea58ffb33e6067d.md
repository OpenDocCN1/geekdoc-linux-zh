
Any of the values that don't require a value can have no prepended to it to have the opposite effect. For example, nobg indicates that the mount should not be done in the background.

## Using autofs to mount NFS file systems on demand

With the autofs facility configured and turned on, you can cause any NFS shared directories to mount on demand. If you know the host name and directory being shared by another host computer, you can simply change (cd) to the autofs mount directory (/net by default) and have the shared resource automatically mount and be accessible to you.

The following steps explain how to turn on the autofs facility:

1.  As root user from a Terminal window, open the `/etc/auto.master` file and uncomment the last line, so it appears as follows:

    ```
    /net   /etc/auto.net
    ```

    This causes the `/net` directory to act as the mount point for the NFS shared directories you want to access on the network.

2.  Start the autofs service by typing the following as root user:

    ```
    # service autofs start
    ```

3.  Set up the autofs service to restart every time you boot your system:

    ```
    # chkconfig autofs on
    ```

Believe it or not, that's all you have to do. Provided that you have a network connection to the NFS servers from which you want to share directories, you can try to access a shared NFS directory. For example, if you know that the `/usr/local/share` directory is being shared from the computer on your network named shuttle, do the following:

1.  Type the following:

    ```
    $ cd /net/shuttle
    ```

    If the computer named shuttle has any shared directories that are available to you, you will be able to successfully change to that directory.

2.  Type the following:

    ```
    $ ls
    usr
    ```

    You should be able to see that the `usr` directory is part of the path to a shared directory. If there are shared directories from other top-level directories, you should see those as well (such as `/var` or `/tmp`). Of course, seeing any of those directories is dependent on how security is set up on the server.

3.  Next, you could try going straight to the shared directory. For example:

    ```
    $ cd /net/shuttle/usr/local/share
    $ ls
    info man music television
    ```

    At this point, the ls should reveal the contents of the /usr/local/share directory on the computer named shuttle. What you can do with that content depends on how that content was configured for sharing by the server.

## Unmounting NFS file systems

After an NFS file system is mounted, unmounting it is simple. You use the unmount command with either the local mount point or the remote file system name. For example, here are two ways you could unmount maple:/tmp from the local directory /mnt/maple.

```
# umount maple:/tmp
# mount /mnt/maple
```

Either form will work. If maple:/tmp is mounted automatically (from a listing in /etc/fstab), the directory will be remounted the next time you boot Fedora. If it was a temporary mount (or listed as noauto in /etc/fstab), it will not be remounted at boot time.

> **TIP:** The command is not unmout, it is umount. This is easy to get wrong.

If you get the message "device is busy" when you try to umount a file system, it means the umount fails because the file system is being accessed. Most likely, one of the directories in the NFS file system is the current directory for your shell (or the shell of someone else on your system). The other possibility is that a command is holding a file open in the NFS file system (such as a text editor). Check your Terminal windows and other shells, and cd out of the directory if you are in it, or just close the Terminal windows.

If an NFS file system won't unmount, you can force umount (i.e., umount -f /mnt/maple) or unmount and clean up later (umount -l /mnt/maple). The -l option is usually the better choice, because a force umount can disrupt a file modification that is in progress.

## Other cool things to do with NFS

You can share some directories to make it consistent for a user to work from any of several different Linux computers on your network. Some examples of useful directories to share are:

-   `/var/spool/mail` — By sharing this directory from your mail server, and mounting it on the same directory on other computers on your network, users can access their mail from any of those other computers. This saves users from having to download messages to their current computers or from having to log in to the server just to get mail. There is only one mailbox for each user, no matter from where it is accessed.
-   `/home` — This is a similar concept to sharing mail, except that all users have access to their home directories from any of the NFS clients. Again, you would mount /home on the same mount point on each client computer. When the user logs in, that user has access to all the user’s start-up files and data files contained in the /home/user directory.
    > **TIP:** If your users rely on a shared /home directory, you should make sure that the NFS server that exports the directory is fairly reliable. If /home isn’t available, the user may not have the start-up files to log in correctly, or any of the data files needed to get data done. One workaround is to have a minimal set of start-up files ( .bashrc, .Xdefaults, and so on) available in the user’s home directory when the NFS directory is not mounted. Doing so allows the user to log in properly at those times.
-   `/project` — Although you don’t have to use this name, a common practice among users on a project is to share a directory structure containing files that people on the project need to share. This way everyone can work on original files and keep copies of the latest versions in one place. (Of course, a better way to manage a project is with CVS or some other version control-type software, but this is a simple work-around.)
-   `/var/log` — An administrator can keep track of log files from several different computers by mounting the /var/log file on the administrator’s computer. (Each server may need to export the directory to allow root to be mapped between the computers for this to work.) If there are problems with a computer, the administrator can then easily view the shared log files live.

If you are working exclusively with Fedora, Red Hat Linux, and other UNIX systems, NFS is probably your best choice for sharing file systems. If your network consists primarily of Microsoft Windows computers or a combination of systems, you may want to look into using Samba for file sharing.

# Setting Up a Samba File Server

Samba is a software package that comes with Fedora and Red Hat Linux systems. Samba enables you to share file systems and printers on a network with computers that use the Server Message Block (SMB) protocol. SMB is the protocol that is delivered with Windows operating systems for sharing files and printers. Although you can’t always count on NFS being installed on Windows clients (unless you install it yourself), SMB is always available (with a bit of setup).

On Fedora, the Samba software package contains a variety of daemon processes, administrative tools, user tools, and configuration files. To do basic Samba configuration, you can start with the Samba Server Configuration window. This window provides a graphical interface for configuring the server and setting directories to share.

Most of the Samba configuration you do ends up in the/etc/samba/smb.conf file. If you need to access features that are not available through the Samba Server Configuration window, you can edit /etc/samba/smb.conf by hand or use SWAT, a Web-based interface to configure Samba.

Daemon processes consist of smbd (the SMB daemon) and nmbd (the NetBIOS name server). The smbd daemon makes the file sharing and printing services you add to your Linux system available to Windows client computers. The client computers this package supports include:

-   Windows 9x
-   Windows 2000
-   Windows NT
-   Windows ME
-   Windows XP
-   Windows for Workgroups
-   MS Client 3.0 for DOS
-   OS/2
-   Dave for Macintosh Computers
-   Samba for Linux

As for administrative tools for Samba, you have several shell commands at your disposal. You can check your configuration file using the testparm and testprns commands. The smbstatus command tells you which computers are currently connected to your shared resources. Using the nmblookup command, you can query for NetBIOS names (the names used to identify host computers in Samba).

Although Samba uses the NetBIOS service to share resources with SMB clients, the underlying network must be configured for TCP/IP. Although other SMB hosts can use TCP/IP, NetBEUI, and IPX/SPX to transport data, Samba for Linux supports only TCP/IP. Messages are carried between host computers with TCP/IP and are then handled by NetBIOS.

## Getting and installing Samba

To see if Samba is installed on your Fedora system, type the following:

```
# rpm -qa | grep samba
samba-*
system-config-samba
samba-swat-*
samba-common-*
samba-client-*
```

You should see the name of each of the five packages, followed by the version number (1 represented version numbers with an asterisk). Although not installed with all installation groups in Fedora, the packages that make up Samba are all included on the DVD that comes with this book. To install Samba, insert the DVD. Then run the following (skipping the first step if it mounts automatically):
