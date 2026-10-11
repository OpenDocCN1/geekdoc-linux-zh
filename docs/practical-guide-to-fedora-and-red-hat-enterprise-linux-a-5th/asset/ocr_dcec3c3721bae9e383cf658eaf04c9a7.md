In the preceding output, **MGS** is the name of the workgroup, **PB** is the name of the Windows machine, **mark** and **tmp** are directory shares, and **MainPrinter** is a shared printer. Workgroup and machine names are always shown in capitals. Refer to the `smbtree man page` for more information.

# SMBCLIENT: CONNECTS TO WINDOWS SHARES

The `smbclient` utility functions similarly to `ftp` (page 643) and connects to a Windows share; however, `smbclient` uses Linux-style forward slashes (`/`) as path separators rather than Windows-style backslashes (\). The next example connects to one of the shares displayed in the preceding example:

```
```
$ smbclient //PB/mark
Password:
Domain=[PB] OS=[Unix] Server=[Samba 3.0.10-1.fc2]
smb: > ls

.
D 0 Wed Feb 20 15:10:03 2008
..
D 0 Mon Feb 4 12:40:17 2008
.kde
DH 0 Tue Feb 5 22:24:17 2008
.xemacs
DH 0 Mon Feb 4 10:12:45 2008
.bash_logout
H 24 Tue Oct 23 06:15:04 2007
.bash_profile
H 191 Tue Oct 23 06:15:04 2007
.bashrc
H 124 Tue Oct 23 06:15:04 2007
...
```
```

You can use most `ftp` commands from `smbclient`. Refer to “Tutorial Session” on page 646 for some examples or give the command `help` to display a list of commands.

# BROWSING WINDOWS NETWORKS

Browsing Windows shares using `smbtree` and `smbclient` is quite awkward compared with the ease of browsing a network from Windows; GNOME provides a more user-friendly alternative. From Nautilus (the Gnome file manager), enter `smb:/` in the location bar to browse the Windows shares on the network.

Nautilus uses a virtual filesystem add-on, which is part of the desktop environment and not part of the native Linux system. As a consequence, only native Gnome applications can open files on remote shares; normal Linux programs cannot. For example, `gedit` will be able to open files on remote shares, while OpenOffice, `mplayer`, and `xedit` cannot.

# MOUNTING WINDOWS SHARES

The `mount` utility (page 487) with a `-t cifs` option mounts a Windows share as if it were a Linux directory hierarchy. See page 1075 for more information on the CIFS protocol. When you mount a Windows share, you can write to the files on the share; you cannot write to files on a share using `smbclient`.