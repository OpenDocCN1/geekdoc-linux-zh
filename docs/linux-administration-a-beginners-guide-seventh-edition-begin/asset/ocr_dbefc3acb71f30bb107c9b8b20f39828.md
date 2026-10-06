# 632 Linux Administration: A Beginner's Guide

+   5. Save your changes to the /etc/samba/smb.conf file, and exit the editor.
Note that we have accepted all the other default values in the file. You may want to go back and personalize some of the settings to suit your environment.
One setting you might want to change is directly (workgroup) that defines the workgroup. This controls what workgroup your server will appear to be in queried by clients or viewed in Windows My Places.
Also note that the default configuration may contain other share definitions. You should comment out (or delete) these if it is not your intention to include them.

+   6. Use the testpar utility to check the smb.conf file for internal correctness (that is, absence of syntax errors):
```bash
root@server ~]# testpar -s less
..<OUTPUT TRUNCATED>...
[samba-share]
comment = This folder contains shares
path = /tmp/testshare
guest ok = Yes
```

Study the output for any serious errors, and try to fix them by going back to correct them in the smb.conf file.

> NOTE Because you piped the output of testparm to the less command, Samba to make the software acknowledge its changes. You may have to press o on your keyboard to quit the command (that is, to quit viewing the output).

+   7. Now restart (or start) Samba to make the software acknowledge its changes. You can use the systemctl command on systemd-enabled Linux distros Fedora to restart the smb server by typing
```bash
root@fedora-server ~]# systemctl restart smb.service
```

We are creating our test share. In the next section, we will attempt to access the share.

> TIP On older versions (pre-systemd) of Debian-based distributions, or Ubuntu, you can restart the samba daemon by running
```bash
master@ubuntu-server:~$ sudo /etc/init.d/samba restart
```

# Using smbclient

The smbclient program is a command-line tool that allows your Linux-based system to act as a Windows client. You can use this utility to connect to other Samba servers