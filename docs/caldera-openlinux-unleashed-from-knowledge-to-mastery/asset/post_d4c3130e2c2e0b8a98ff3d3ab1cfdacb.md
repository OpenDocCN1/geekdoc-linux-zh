
## Running Samba

A Samba server consists of two daemons: The **nmbd** daemon provides NetBIOS name service, and the **smbd** daemon provides actual resource sharing.

To have Samba start automatically when you boot, open the COAS System::Daemons dialog box and enable SMB Server Processes (Samba).

To manually start Samba, run this command as root:

```
# sh /etc/rc.d/init.d/samba start
```

To stop Samba, use:

```
# sh /etc/rc.d/init.d/samba stop
```

If you have changed the configuration file and need to restart Samba, use:

```
# sh /etc/rc.d/init.d/samba restart
```

The script `/etc/rc.d/init.d/samba` starts or stops the **nmbd** and **smbd** programs. These programs have a number of command-line options; see the manual pages **nmbd(8)** and **smbd(8)**, respectively.

## Debugging a Samba Setup

Samba includes a couple of utility programs for debugging your Samba setup. They verify that your configuration file is sane and allow you to connect to SMB servers from the Linux command line.

### Verifying the Samba Configuration File

The program **smbtestparm** parses the Samba configuration file and reports any errors. Here is an example:

```
$ smbtestparm
Load smb config files from /etc/samba.d/smb.conf
Processing section "[homes]"
Processing section "[cdrom]"
Processing section "[printers]"
Processing section "[public]"
Processing section "[pdwrite]"
Loaded services file OK.
Press enter to see a dump of your service definitions
```

After verifying that all services are correct, **smbtestparm** prompts you to press Enter. When you do so, it dumps a complete list of global parameters. This includes both the parameters in the configuration file and default values for those not in the configuration file. It then prints a complete list of shares.

The prompt to press Enter is rather annoying because it makes it hard to pipe smbtestparm’s output to a file or through more. If you wish to put smbtestparm’s output in a file, invoke it with the -s option:

```
$ smbtestparm -s > tempfile
```

## Command-Line SMB Client

smbclient is a command-line SMB client program. This lets you connect to SMB shares from a Linux machine, eliminating the need to test your setup from a Windows machine.

The simplest way to connect to a share is as follows:

```
$ smbclient //server/share
```

Here’s an example:

```
$ smbclient //shishi/dfs
Added interface ...
Password: k3w1d00d
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 2.0.3]
smb: \>
```

The share to which you connect (in this case, //shishi/dfs) is referred to as the remote directory, and the current UNIX working directory is the local directory.

The smb: prompt is an FTP-like prompt. To list the available commands, type help:

```
smb: \> help
ls dir du lcd cd
...
```

Some of the more useful smbclient commands are given in Table 16.1.

**TABLE 16.1** smbclient Commands

| Command | Meaning |
| :--- | :--- |
| ls | List the contents of the current remote directory. |
| pwd | Show the current remote directory. |
| rename | Rename a file. |
| rm | Delete a file. |
| get | Transfer a file from the remote directory to the local directory. |
| put | Transfer a file from the local directory to the remote directory. |
| print | Print a local file. Only valid if the share is a printer share. |
| help | List available commands. |
| help *cmd* | Get help about the command *cmd*. |
| quit | Log off from the SMB server. |

As you see, **smbclient** is very similar to the command-line FTP client. For details about other commands, type **help** at the **smbclient** prompt. For details about invoking **smbclient**, see the man page **smbclient(1).**

## Backing Up SMB Shares

**smbclient** has a very useful command called **tar**. This command creates a *tar* file of the remote directory. You can use **smbclient** to back up or restore SMB shares from a Linux machine.

To back up an SMB share, use the **c** option:

```
smb:\> tar c backup.tar

5166 ( 280.3 kb/s) \SUSLOG.DAT
28553 ( 386.0 kb/s) \BOOTLOG.TXT
20553 ( 378.7 kb/s) \BOOTLOG.PR
93812 ( 424.1 kb/s) \COMMAND.COM
...
```

**smbclient** backs up the entire share in **backup.tar**. The **x** option is the opposite; it causes **smbclient** to extract files from local *tar* file and place them on the SMB share.

You can invoke **smbclient** with the **-T** option to automatically invoke the *tar* command. This lets you write shell scripts to back up SMB shares from Linux. See **smbclient(1)** for details.

## Mounting SMB Shares

Not only can Linux act as an SMB server, it can also mount SMB file systems. You can put SMB shares in your Linux directory tree, just as you can put NFS volumes in the tree.

To mount an SMB share, use the **smbmount** command:

```
# smbmount //server/share password -c 'mount mountp'
```

For example, the following command mounts the `\\windows\\c share` under `/mnt/w`:

```
# smbmount //windows/c k3w100ed -o "mount /mnt/w/"
```

You can verify that the mount worked by listing the directory contents:

```
$ ls /mnt/w
```

```
AUTOEXEC.BAT      DETLOG.TXT      SETUPLOG.TXT
Acrobat3          DRVSPACE.BIN    SUIDLOG.DAT
BOOTLOG.PRV       IO.SYS          SYSTEM.1ST
BOOTLOG.TXT       MSDOS.--        WEBSHARE
COMMAND.COM       MSDOS.SYS       WINDOWS
CONFIG.SYS        NETLOG.TXT      dfs
DBLSpace.BIN      Program Files   logo.sys
DETLOG.OLD        RECYCLED
```

Yes, all the ugly Windows files are there.

Because SMB does not have the concept of users or groups, the **smbmount** command lets you specify the user and group for the mounted share (from UNIX's point of view). The `-u` option specifies the numeric user ID, and the `-g` specifies the numeric group-ID. They default to the user ID and group ID of the person who invoked **smbmount**. You can also specify file and directory permissions as octal numbers with the `-f` and `-d` options. See the **smbmount(8)** and **smbnt(8)** manual pages for details.

To unmount an SMB share, use the usual **umount** command:

```
# umount /mnt/w
```

## Checking Samba's Status

The **smbstatus** command displays a short listing of all currently active shares. Here is an example:

```
$ smbstatus

Samba version 2.0.3
Service  uid  gid  pid  machine
--------------------------------------
dfs      dfs  dfs  1056  windoze  Mon Aug 23 09:02:21 1999
cdrom    dfs  dfs  1056  windoze  Mon Aug 23 09:02:21 1999
public   dfs  dfs  1056  windoze  Mon Aug 23 09:02:21 1999

No locked files

Share mode memory usage (bytes):

1848464(99%) free + 56(0%) used + 56(0%) overhead = 1848576(100%) total
```

The -b option provides “brief” output:

```
$ smbstatus -b
Samba version 2.0.3
PID Username Machine Time logged in
--------------------------------------------------
1056 dfs winzoe Mon Aug 23 09:02:21 1999
```

## Web-Based Samba Configuration

If editing the text smb.conf file has depressed you, cheer up: Samba supports web-based configuration file editing via a program called SWAT (Samba Web-based Administration Tool).

To enable SWAT, make sure that the following line appears in /etc/services:

```
swat  901/tcp # Samba Web Administration Tool
```

Next, make sure that the following line appears in /etc/inetd.conf:

```
swat stream tcp nowait.400 root /usr/sbin/tcpd swat
```

Finally, and most importantly, put this line in /etc/hosts.deny:

```
swat:ALL EXCEPT 127.0.0.1
```

> **Warning**
> SWAT requires you to enter the root password in your Web browser. Do not use SWAT over the network; intruders could sniff the root password. The line in /etc/hosts.deny ensures that all SWAT sessions are run on the Samba server itself.

Restart inetd as follows:

```
# kill -HUP `cat /var/run/inetd.pid`
```

On the Samba server, start a Web browser and open the URL http://localhost:901:

```
$ netscape http://localhost:901
```

Enter the root login and password. You will be presented with the wonderful SWAT home page (Figure 16.1).
