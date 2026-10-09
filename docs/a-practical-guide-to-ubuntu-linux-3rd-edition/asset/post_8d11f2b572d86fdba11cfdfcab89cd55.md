
/tmp directory from dog as j (tmp) on the Windows machine. If you cannot map the drive, refer to “Troubleshooting” on page 817.

## WORKING WITH WINDOWS SHARES FROM LINUX

Samba enables you to view and work with files on a Windows system (client) from a Linux system (server). This section discusses several ways of accessing Windows files from Linux.

### smbtree: Displays Windows Shares

The **smbtree** utility displays a hierarchical diagram of available shares. When you run **smbtree**, it prompts you for a password; do not enter a password if you want to browse shares that are visible to the *guest* user. The password allows you to view restricted shares, such as a user's home directory in the **[homes]** share. Following is sample output from **smbtree**:

```
$ smbtree
Password: RETURN (do not enter a password)
MGS
    \\JAM
            \\JAM\CS        Default share
            \\JAM\ADMIN$    Remote Admin
            \\JAM\F
            \\JAM\E
            ...
    \\DOG       Samba 3.0.22
            \\DOG\dogprinter HP LaserJet 1320
            \\DOG\print$     Printer Drivers
            \\DOG\home
            \\DOG\p81        common backed-up directory
            \\DOG\p82        common backed-up directory
```

In the preceding output, **MGS** is the name of the workgroup, **JAM** is the name of the Windows machine, and **DOG** is the name of the Samba server the **smbtree** utility is run from. Workgroup and machine names are always shown in uppercase letters. If **smbtree** does not display output, set the **workgroup** (page 808) and **wins server** (page 813) parameters in **smb.conf**. Refer to the **smbtree** man page for more information.

### smbclient: Connects to Windows Shares

The **smbclient** utility functions similarly to ftp (page 687) and connects to a Windows share. However, **smbclient** uses Linux-style forward slashes (/) as path separators rather than Windows-style backslashes (\). The next example connects to one of the shares displayed in the preceding example:

```
$ smbclient //JAM/D
Enter sam's password: RETURN (do not enter a password)
Anonymous login successful
Domain=[JAM] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: > ls
audit            D     0 Tue May 4 18:46:33 2010
Data             D     0 Tue May 4 18:47:09 2010
laptop.data      D     0 Tue May 4 19:12:16 2010
Linux            D     0 Tue May 4 18:57:49 2010
oldfonts         D     0 Wed May 5 00:02:17 2010
PSFONTS          D     0 Tue May 4 18:45:36 2010
RECycler         DH  0 Thu May 6 20:05:21 2010
System Volume Information  DH   0 Tue May 4 18:45:32 2010
                       46547 blocks of size 1048576. 42316 blocks available
smb: >
```

You can use most ftp commands from smbclient. Refer to "Tutorial Session" on page 690 for some examples. Alternatively, give the command **help** to display a list of commands or **help** followed by a command for information on a specific command:

```
smb: \> help history
HELP history:
    displays the command history
```

## BROWING WINDOWS NETWORKS

Browsing Windows shares using `smbtree` and `smbclient` is quite awkward compared with the ease of browsing a network from Windows; GNOME provides a more user-friendly alternative. From Nautilus, enter `smb:///` in the location bar to browse the Windows shares on the network.

Nautilus uses virtual filesystem add-ons, which are part of the desktop environment and not part of the native Linux system. As a consequence, only native GNOME applications can open files on remote shares; normal Linux programs cannot. For example, gedit can open files on remote shares, while OpenOffice, mplayer, and xedit cannot.

## MOUNTING WINDOWS SHARES

The mount utility (page 506) with a `-t cifs` option mounts a Windows share as if it were a Linux directory hierarchy. See page 1141 for more information on the CIFS protocol. When you mount a Windows share, you can write to the files on the share; you cannot write to files on a share using `smbclient`.

A mount command that mounts a Windows share has the following syntax (you must run this command with root privileges):

```
mount -t cifs //host/share dir
```

where *host* is the name of the system the share is on, *share* is the name of the Windows share that you want to mount, and *dir* is the absolute pathname of the Linux directory that you are mounting the share on (the mount point).

The following command, when run with **root** privileges, mounts on the /share directory the share used in the preceding example:

```
$ sudo mount -t cifs //jam/d/share -o username=sam
Password:
$ ls /share
Linux RECYCLER audit laptop.data
PSFONTS System Volume Information data oldfonts
```

You can omit the **username** argument and provide a blank password to mount shares that are visible to the **guest** user. Use the **uid**, **file_mode**, and **dir_mode** mount options with type **cifs** filesystems to establish ownership and permissions of mounted files.

```
$ sudo mount -t cifs //jam/d/share -o username=sam,uid=sam,file_mode=0644,dir_mode=0755
```

Permissions must be expressed as octal numbers preceded by a zero. For more information refer to the *mount.cifs* man page.

## TROUBLESHOOTING

Samba provides two utilities that can help troubleshoot a connection: **testparm** checks the syntax of /etc/samba/smb.conf and displays its contents; **smbstatus** displays a report on open Samba connections.

The following steps can help you narrow down the problem when you cannot get Samba to work.

- 1. Restart the Samba daemons. Make sure **smbd** is running.

```
$ sudo service smbd restart
smbd start/running, process 4420
```

- 2. Run **testparm** to confirm that the *smb.conf* file is syntactically correct:

```
$ testparm
Load smb config files from /etc/samba/smb.conf
Processing section "[printers]"
Processing section "[print$]"
Processing section "[p12]"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions
...
```

You can ignore an error message about **rlimit_max**. If you misspell a keyword in *smb.conf*, you get an error such as the following:

```
$ testparm
Load smb config files from /etc/samba/smb.conf
Unknown parameter encountered: "workgruop"
Ignoring unknown parameter "workgruop"
...
```

- 3. Use ping (page 393) from both sides of the connection to make sure the network is up.

- 4. Confirm the firewall on the server is not blocking the Samba connection (page 799).

- 5. Make sure you have set up a password for the Samba user you are trying to log in as.

- 6. From a *Windows* command prompt, use **net view** to display a list of shares available from the server (**dog** in this example):

```
C:\> **net view \\dog**
Shared resources at \\dog

Samba 3.0.24
```

| Share name | Type | Used as | Comment |
|---|---|---|---|
| backup | Disk | | The backup partition |
| dogprinter | Print | | HP LaserJet 1320 |
| homes | Disk | | Home Directories |
| p04 | Disk | 0: | common backed-up directory |
| ... | | | |

The command completed successfully.

- 7. Try to map (mount) the drive from a *Windows* command prompt. The following command attempts to mount the share named **p04** on **dog** as drive **X**:

```
C:\> **net use x: \\dog\\p04**
The command completed successfully.
```

- 8. From the Samba server, query the **nmbd** server, using the special name **__SAMBA__** for the server’s NetBIOS name. The **-d 2** option turns the debugger on at level 2, which generates a moderate amount of output. The **-B** option specifies the server you are querying.

```
$ **nmblookup -d 2 -B localhost __SAMBA__**
added interface ip=192.168.0.10 bcast=192.168.0.127
  nmask=255.255.255.128
querying __SAMBA__ on 127.0.0.1
Got a positive name query response from 127.0.0.1 ( 192.168.0.10 )
192.168.0.10 __SAMBA__<00>
```

The next example uses **nmblookup**, without setting the debug level, to query the local system for all NetBIOS names.

```
$ **nmblookup -B localhost \***
querying \* on 127.0.0.1
192.168.0.10 \*<00>
```

To query for the master browser from the local server, run **nmblookup** with the **-A** option followed **localhost** or the name of the server:
