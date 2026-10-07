```
$ smbclient //server/share
```

After you type this command, smbclient prompts you for a password, which should match the password associated with your username on the server. (If your username on the server is not the same as on the client, you can use the `-U username` parameter to specify your username on the server.) The commands available in smbclient are similar to those in the text-mode ftp program, or from a Linux shell—to see the available files; put and get to transfer files to and from the share, respectively; cd to move to a new directory; and so on. You can type ? or help to see a summary of commands.

Although smbclient can be a good way to quickly transfer a few files, smbmount is more flexible if you want to be able to directly modify files on the server. You might use this tool to use a Linux program to edit a file that's stored on a server, for instance. To use smbmount, issue the command in the following form:

```
$ smbmount //server/share mountpoint
```

**Note** If you don't issue the smbmount command as root, two programs must be set user ID (suid) root for this to work: smbmnt (a helper program to smbmount) and smbmount (used to umount SMB/CIFS shares). You can issue the command `chmod a+s /usr/bin/smbmnt /usr/bin/smbmount` to accomplish this task.

Like smbclient, smbmount asks you for a password before it mounts the share. Once a share is mounted, you can access the files on it as if they were on a local disk, with certain caveats. Some filesystems may be shared read-only, so you may not be able to write files to these shares. SMB/CIFS doesn't support Linux-style ownership and permissions, so by default, all files are owned by the individual who issues the smbmount command. When you're done with a share, you can unmount it with the smbmount command; enter it as

```
$ smbmount mountpoint
```

As mentioned earlier, you can use mount instead of smbmount with Samba 2.0.6 and later. To do so, you call mount with a filesystem type of smbfs, thus:

```
# mount -t smbfs //server/share mountpoint
```

This procedure works best when the caller is root, unless you create an /etc/fstab entry that allows ordinary users to issue the mount command, as described in Chapter 6. When this is the case, you should omit the filesystem type, server, and share names when issuing the mount command (as in mount mountpoint).

Several GUI front-ends to smbmount are available. Details of operation differ from one program to another, but as a general rule, these utilities present a GUI view of the local network, as demonstrated by LinNeighborhood (http://www.bnr.o.de/~schmidjo/), shown in Figure 12.4. When you double-click a share to open it, a dialog box asks for your username and password, and the program then opens a window on the share using the file manager you specify when you configure the program. GUI front-ends don't really add fundamentally new functionality to Linux's SMB/CIFS capabilities, but they do make these networks more accessible to those who aren't familiar with Samba's text-mode tools. You may therefore want to install LinNeighborhood, or a similar package, such as Kruiser (http://devel-home.kde.org/~kruiser/) or xSMBrowser (http://www.public.iastate.edu/~chadspen/).