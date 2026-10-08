# Chapter 16: Creating Basic Linux Network Services 221

![](bbox=[0.13, 0.14, 0.21, 0.2])

Samba was originally designed and coded by Andrew Tridgell, of Australia. Samba instantly became popular worldwide and became too much for a few people to handle. Thus, the Samba project was started in order to take care of the phenomenon. You can find more information about Samba at www.samba.org.

Follow these steps to dance the— er, install, configure, and use— Samba:

+   1. **Log in as root and insert this book’s companion DVD-ROM.**

+   2. **Open a terminal emulator window and enter this command:**

```
```
rpm -ivh /mnt/cdrom/RedHat/PPMS/samba-client*
```
```

The Samba server consists of two daemons: smbd and nmbd. You must start both daemons before anyone can access your Samba server.

+   3. **Enter this command to start the daemons:**

```
```
/etc/init.d/smb start
```
```

You can stop the daemons by substituting the stop option for the start option. You can restart the Samba server by using the restart option:

```
```
/etc/init.d/smb restart
```
```

+   4. **Automate the startup of the Samba daemons by creating these soft links with the chkconfig utility:**

The following command tells Linux to automatically start Samba for Level 3 (nongraphical) and Level 5 (running the graphical X server); Samba is started whether your Linux computer starts in graphical or nongraphical mode:

```
```
chkconfig --level 35 smb on
```
```

Samba is configured by default to use its own password file. You must create the password file by using the mksmbpasswd.sh script.

+   5. **Use the smbpasswd program to create the Samba user account and password.**

The -a option tells the script to add the user account to the smbpaswd file:

```
```
smbpasswd -a paul
```
```

You’re prompted to enter a password twice.