
## Part II: Ubuntu for Desktop Users

- USERNAME: This is the name of the user that you want to use to mount the Windows share on the remote host, and PASSWORD is that user's password.
- uid=0: Use User ID 0 when mounting the filesystem.
- gid-users: All files on the Windows share will be assigned to the group users. This enables users of your systems that belong to this group (with their Windows login name) to write files that they can access on the remote system.

## Caution

Some versions of the kernel support for CIFS filesystems have some issues. If you are unable to mount CIFS shares from remote systems or cannot see these shares after mounting them, you must add the noiserverino to the list of mount options in the /etc/fstab entry for those shares.

Mounting a Windows share via the /etc/fstab file will make that share available to all users of your system, enforcing file access security through the users entry in the /etc/group file and permission settings on files and directories in the share, which is fine for multiuser systems. For personal desktop Linux systems, you may prefer to require that each system manually mount the Windows shares that they themselves need, which will enable you to leverage your personal security settings more precisely on the Windows server. The next sections discuss how users mount Windows shares themselves on their Ubuntu desktop systems.

## Connecting to Windows Shares from the GNOME Desktop

Ubuntu's Places menu provides the "Connect to Server" command, which makes it easy to create an icon on your desktop for a Windows share and connect to that share using the Nautilus File Manager. Selecting Places Connect to Server displays the dialog shown earlier in Figure 26-2. To specify that you want to connect to an FTP server that requires authentication, click the "Service type" menu at the top of this dialog and select the Windows share entry to display the dialog in Figure 26-8.

FIGURE 26-8
Identifying a Windows share to connect to

![](img/1a233c34336fbf5a85d6eb785e401709_979_0.png)

You must least enter the name or IP address of the Windows server that hosts the share you want to connect to. If you are going to access this directory frequently, you can create a permanent entry for it in the Places menu by checking “Add Bookmark” and entering a name for the bookmark on the Places menu. You can also identify the name of the user that you want to connect as, the name of the Windows domain or workgroup you want to connect as, and the share you want to connect to, but all of this is optional—you will be prompted for anything that you do not specify here when you attempt to connect. Click Connect to create a desktop icon for the Windows share that you have defined.

Simply creating a desktop icon for a Windows share doesn't actually establish the connection. To do that, double-click on the appropriate desktop icon to open it. You will see a dialog that prompts you for any required information that you have not specified yet, as shown in Figure 26-9.

## Figure 26-9

Completing authentication information for a Windows share

![](img/1a233c34336fbf5a85d6eb785e401709_980_0.png)

Once you enter any remaining information about the share that you want to connect to and the server upon which it resides, a Nautilus File Manager window appears that displays the contents of the default directory associated with the user that you are logged in as, as shown in Figure 26-10.

Once the Nautilus File Manager displays, copying files in either direction you use the standard Nautilus and GNOME desktop conventions, as discussed in Chapter 5.

Once you are accessing the Windows share, close the Nautilus File Manager window. To discard the desktop icon, right-click on the icon for the Windows share and select “Unmount Volume” from the pop-up menu to sever the connection and discard the icon. Desktop icons for SMB shares will be automatically removed when you log out. If you want to create a permanent desktop icon, see the sidebar entitled “Creating Permanent Desktop Icons for Services and Locations,” earlier in this chapter, for more information.

## Part II: Ubuntu for Desktop Users

A connection to a Windows share in the Nautilus File Manager

![](img/1a233c34336fbf5a85d6eb785e401709_981_0.png)

## Connecting to Windows Shares from the Command Line

While many people find using the command line to be a throwback to the 1980s and serial terminals, command-line commands are eminently portable, working fine from your Terminal emulator of choice (a GNOME Terminal, xterm, etc.) on Ubuntu and non-Ubuntu distributions.

To mount a Windows share from the command line on any Ubuntu system, execute a command like the following:

```
sudo mount -t cifs //192.168.6.64/vwh /mnt/vwh \
  -o username=vwh,password=yeahright,rw
```

(This command would ordinarily be typed on a single line—the backslash in this command is only present for formatting purposes.).

This command mounts the Windows or Samba share vwh from the host 192.168.6.64 on the directory /mnt/vwh read-write mode (rw), authenticating as the user vwh with the password yeahright. The mounted share will be available on this directory until it is unmounted, you can do via the following command:

```
sudo umount /mnt/vwh
```

Note that this command isn't unmount, ummount. Why type that extra n if you don't have to?

## Caution

Some versions of the kernel support for CIFS filesystems still have some issues. If you are unable to mount CIFS shares from remote systems or cannot see files in these shares after mounting them, you must add the noserverino keyword to the mount command that you use to mount those shares.

## Accessing NFS Directories from Linux Systems

Long before Microsoft Windows, UNIX systems were sharing files over networks using Network File System (NFS), which was originally developed by Sun Microsystems, Inc. in the early 1980s. Sun smart enough to release the specifications for NFS to the known universe, and every other UNIX system manufacturer with common sense since has also implemented support for NFS on UNIX and UNIX-like systems. Most of those vendors are gone and Sun's long-term future is cloudy, but NFS lives as the default filesystem and file sharing mechanism that you can find on any UNIX or UNIX-like system, such as Linux and Mac OS.

Unfortunately, a whimsical mechanism for mounting NFS filesystems isn't currently supported by the GNOME desktop's "Connect to Server" tool you'll have to mount remote filesystems manually, using the command line. And you might have thought you could get away with not reading Chapter 11, "Using-Line Tools! Luckily, mounting filesystems from the command line is extremely easy to do. (The mechanism by you export a filesystem from your local system via NFS is similarly easy, and is explained in Chapter 4)

NFS filesystems are identified by the name or IP address of the NFS server where they live, a colon, and the name of the directory that is exporting. For example, 192.228.6.64:/home/whm is the directory /home/whm that is exported by the NFS server whose IP address is 192.228.6.64. NFS filesystems are mounted on directories of your local system just like any other filesystem (explained in Chapter 4)

To mount the remote filesystem that I just mentioned, you therefore need to create a mountpoint for it. I create these in the directory /mnt so they are easily identified as temporary mounted devices. For example, the following command creates a mountpoint called /mnt/nfs:

```
$ mkdir /mnt/nfs
Password:
```

After providing your password, the mountpoint exists, so you can now mount the NFS directory using the standard Linux mount command, as in the following example:

```
$ mount -t nfs 192.228.6.64:/home/whm /mnt/nfs
```

At this point, you can verify that the directory is successfully mounted either by listing the directory or by simply using the df command, in the following example:

| Filesystem | 1K-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | 77299808 | 40359644 | | 56% | / |
| varrun | 257968 | 136 | 257832 | 1% | /var/run |
| varlock | 257968 | 4 | 257964 | 1% | /var/lock |
