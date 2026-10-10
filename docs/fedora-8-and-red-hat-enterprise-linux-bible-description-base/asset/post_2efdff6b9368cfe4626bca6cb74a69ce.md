
May 14 17:45:03 toys afpd[2074]: ASIP started on 10.0.0.100:548(1.5.5)
May 14 17:45:03 toys afpd[2074]: uam: uams_clrtxt.so loaded
May 14 17:45:03 toys afpd[2074]: uam: uams_dhx.so loaded
May 14 17:45:03 toys afpd[2074]: uam: *D82Qst28* available
May 14 17:45:03 toys afpd[2074]: uam: "Cleartext Password" available

In the previous example, you can see that the atalkd start-up script successfully started up the atalkd, papd, and afpd daemons. The atalkd daemon looks for AppleTalk network information on the first Ethernet interface (eth0). The papd daemon started, but had no printers to register. The afpd daemon started an AppleTalk file server on the server (toys:APPServer). It then identified the user authentication methods (uams) that are available (both clear-text and encrypted passwords are available here).

## Accessing NFS Servers from the Mac

For many years, Network File System (NFS) was the preferred method for sharing files among Linux and other UNIX-like computer systems. Although Mac OS X does support NFS connections from its Connect to Server window, you need to perform a little trick on the Linux server for that server to accept connections from the Mac OS X computer.

The following procedure describes how to use the Connect to Server window from a Mac OS X client to access files and directories from a shared Linux NFS server. You can then use the files and directories (also called folders) that reside on the Linux NFS server as though they existed on your Mac OS X computer.

As I’ve mentioned, the procedure relies on being able to make a small change to how the Linux NFS server offers the shared directory. If you don’t have access to the Linux server, you either need to ask the administrator of the Linux server to make the change or connect your Mac to the Linux NFS server manually. (I describe the manual procedure at the end of this section.)

### Connecting to NFS from the Connect to Server window

To create an NFS shared directory in Linux and connect to it from a Mac client, do the following:

1. On the Linux server, export a shared directory using the NFS facility as described in Chapter 18. To be able to use the shared directory from Mac OS X, however, you must be sure to add the `insecure` option. For example, to share the `/var/music` directory from the Linux server named juicebox.linuxtoys.net, you can add the following line to the `/etc/exports` file on that server:

   ```
   /var/music        *(rw,insecure)
   ```

   This example allows the `/var/music` directory to be shared with all computers (`*`) and provides read and write permission (`rw`). The `insecure` option lets clients that request the exported directory make the request from an insecure port (ports above 1024). This is important because the Mac OS X Connect to Server window makes its request to mount the shared directory from a port above 1024, and fails without the option.

2. On the Linux server, verify that the NFS service is running and re-export the shared directory by typing the following (as root user):

   ```
   # exportfs -a -v
   ```

3. On the Mac OS X client, select Go in the Finder bar at the top of the screen, and then select Connect to Server. The Connect to Server window appears.

4. On the Mac OS X client, type the address of the share directory into the Address box. For example, to connect to the shared NFS (`nfs://`) directory called `/var/music` from the computer named jukebox.linuxtoys.net, you can type the address `nfs://jukebox.linuxtoys.net/var/music` (see Figure 26-5).

If everything is working properly, an icon representing the server should appear on your Mac OS X desktop. Depending on which version of Mac OS X you are using, a window might just pop open, displaying the contents of the directory or you may need to open that icon to see the contents of the shared directory. You can use the shared files and directories as though they were on your Mac (if permissions on the server permit you to do so). Drop the icon in the trash when you are done.

> **NOTE:** If you are unable to connect to the shared directory, go through the NFS procedures in Chapter 18 more carefully. In particular, make sure that firewall ports are open on the server and that the user and host permissions are set to allow the level of access that you require.

![](img/fb202c163797a743c3c6cf236316bc96_1033_0.png)

Figure 26-5: Connect to an NFS server from the Connect to Server window.

### Connecting to NFS from the command line

You might very well not have any control over how the Linux NFS server is configured. So if the `insecure` option isn't set, you will fail to mount an NFS directory from the Mac's Connect to Server window. A possible workaround is to manually mount the NFS directory from Mac OS X and use a secure port. Here's how:

1. On the Mac OS X computer, gain access to the root user account as follows:
   - a. With the Folder icon selected, select Go → Applications. The *Applications* folder appears.
   - b. Open the *Utilities* folder, then the *NetInfo* Manager utility.
   - c. Click the lock icon on the NetInfo Manager window so that it unlocks.
   - d. Select Security → *Enable Root User*. (If you see a NetInfo error, click OK.)
   - e. Type in and verify the new root user password, and then click *Verify*. (Remember that `password!`)
   - f. Click the open lock icon to close it and prevent further changes.

2. On the Mac OS X computer, click the Terminal icon to open a shell and log in as root:

   ```
   $ su -
   Password: ********
   ```

3. Create a directory that is accessible to the user account of the person who wants to use the shared NFS directory on the Mac. For example, for the user `chris` you might type:

   ```
   # mkdir /Users/chris/music
   # chown chris /Users/chris/music
   ```

4. Mount the NFS shared directory on the directory you just created. For example:

   ```
   # mount -o "-P" jukebox.linuxtoys.net:/var/music /Users/chris/music
   ```

   The `-P` says to use a privileged port. Replace `jukebox.linuxtoys.net` and `/var/music` with the server's name and the shared directory, respectively. The user can now access `/var/music` from the `/Users/chris/music` directory on the Mac OS X client.

## Installing Fedora on an Intel-based Mac

The latest Apple computers feature Intel-based computer architecture. The Fedora Project has enhanced Fedora so that it can be installed (either by itself or dual booting with Mac OS X) on this new Apple hardware. Reasons you might want to install Fedora on one of these "Maclet" computers include:

- **Dual booting** — You might like the Mac OS X desktop (Aqua) and proprietary applications (such as iPhoto or iTunes) for yourself or family members some of the time. However, you might sometimes want access to server applications, administration tools, development environment, or thousands of free applications you can get with Fedora.
- **Fedora only** — Although you pay a bit of a premium for Apple hardware (though not as much as you used to), you might like the form and features of those cute Apple Mac computers enough to pay a bit extra to have it as your primary desktop Fedora computer.

This section describes how to start with an Intel-based Apple Mac computer (I used a Mac Mini for this example) and configure it to either dual boot with Mac OS X or run Fedora alone.

> **CAUTION:** Installing Fedora on Intel-based hardware is still a technology that is experimental in the Fedora community. Some hardware components still require extra tweaking or won’t work at all. I recommend that you don’t do this procedure if you can’t afford the possibility that your disk may be blown away and have to be reinstalled from scratch.

### Before installing Fedora on your Mac

Let’s start with a reminder that this procedure is only for Apple Mac computers that are based on Intel architecture. I ran this procedure on a new Mac Mini 1.1 (Intel Core Duo CPU, 512MB RAM). However, the same procedure should work for Intel-based iMac, MacBook, MacBook Pro, or Mac Pro computers.

This procedure is not for Macs with PowerPC architectures. Fedora does support that configuration, but you need to download the ppc installation media from Fedora instead of using the DVD that comes with this book. (Get the media for installing on PowerPCs from http://fedoraproject.org/wiki/Distribution/Download.)

When you purchase your Mac, the entire hard disk is devoted to Mac OS X. To keep your Mac OS X installation on the computer (so you can boot either Mac OS X or Fedora), you need to reduce the amount of space devoted to Mac OS X. Then you need to use that space to create one or more partitions for installing Fedora.

Although the procedure for resizing and repartitioning your disk is fairly safe, there is some risk that you could corrupt your Mac OS X partition or make the machine (temporarily) unbootable. For that reason, before starting the procedure that follows, please . . .

. . . BACK UP ANY IMPORTANT DATA!

### Installing Fedora

Mac OS X Leopard offers software called Boot Camp that can be used to resize Mac hard disks (using the default HFS+ file system type). Until Leopard was released, the beta version of Boot Camp was available as a free download from Apple. The following procedure describes how to update your firmware, resize your disk, and install Fedora.

1. **Check for firmware updates** — Update your Mac OS X system to the latest firmware. Refer to the Mac OS X Firmware Updates page for information on how to do that
