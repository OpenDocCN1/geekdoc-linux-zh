
The following sections describe how to install Samba from the companion CD-ROMs. They also discuss the process of setting up a printer on the Red Hat Linux PC to print through Windows.

## Checking if Samba is installed, and installing Samba

Before installing Samba, first check whether Samba is already installed by typing the following command in a terminal window:

```
rpm -qa | grep samba
samba-common-2.0.7-36
samba-client-2.0.7-36
samba-2.0.7-36
samba-swat-2.0.7-36
```

If the rpm command displays a package name that begins with samba, then Samba is already installed on your system and you should skip the rest of this section. Otherwise, follow these steps to install Samba from this book's companion CD-ROMs:

- Log in as root and make sure that the companion CD-ROM is in the drive and mounted. If not, use the umount /mnt/cdrom command to dismount the current CD-ROM, replace it with the companion CD-ROM, and then mount it with the mount /mnt/cdrom command.
- Use the following command to change the directory to the CD-ROM where the Red Hat Package Manager (RPM) packages are located:
  ```
  cd /mnt/cdrom/Redhat/RPMS
  ```
- Use the following rpm command to install Samba:
  ```
  rpm -ivh samba*
  ```

If Samba is already installed, this command gives an error message. Otherwise, the rpm command installs Samba on your system by copying various files to their appropriate locations.

These steps complete the unpacking and installation of the Samba software. Now, to use Samba, you simply configure it.

## Configuring Samba

To set up the Windows file- and print-sharing services, you have to provide a configuration file named /etc/samba/smb.conf. The configuration file is a text file that looks like a Microsoft Windows 3.1 INI file.

Like the Windows INI files, the /etc/samba/smb.conf file consists of sections with a list of parameters in each section. Each section of the smb.conf file begins with the name of the section in brackets ([]). The section continues until the next one begins or the file ends.

Each line in a section specifies the value of a parameter using this syntax:

```
name = value
```

As in Windows INI files, comment lines begin with a semicolon (;). In the /etc/samba/smb.conf file, comments may also begin with a hash mark (also known as the number sign), #.

> Text editors are covered in Session 9.

The Samba software comes with a configuration file that you can edit to get started. To prepare the configuration file, log in as root and use your favorite text editor to edit the file /etc/samba/smb.conf. Here’s a sample configuration file without any comments:

```
[global]
workgroup = KurtWerks
server string = Samba Server
hosts allow = 192.168.127.
guest account = kwail
log file = /var/log/samba/%m.log
max log size = 0
security = user
smb passwd file = /etc/samba/smbpasswd
encrypt passwords = yes
unix password sync = no
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
remote browse sync = 192.168.0.255
remote announce = 192.168.0.255
local master = yes
os level = 33
name resolve order = 1mhosts bcast
dns proxy = no
ssl CA certFile = /usr/share/ssl/certs/ca-bundle.crt

[printers]
comment = All Printers
path = /var/spool/samba
browseable = yes
guest ok = yes
writable = no

[homes]
comment = Home Directories
browseable = yes
writable = yes
printable = yes

[tmp]
comment = Temporary file space
path = /tmp
read only = no
public = yes

[public]
comment = Public Stuff
path = /home/samba
browseable = yes
public = yes
guest ok = yes
writable = yes
printable = no
available = yes
guest only = no
user = kwall
only user = yes
```

Change the workgroup name to one of your choosing. Change the user and guest account entries from kwall to your user name. Also make sure that all directories mentioned in the configuration file actually exist. For example, create the /home/samba directory with the command mkdir /home/samba.

After editing the Samba configuration file, add two users to the Samba password file. First add your user name. Here’s how one user adds himself:

```
smbadduser kwall:kwall

---------------------------------------------------
ENTER password for kwall
New SMB password:       type the password
Retype new SMB password:       type password again
Added user kwall.
```

Next add the root user with the command smbadduser root:root and then provide a password. (This does not change the password of your Red Hat Linux system’s root user.)

After making the changes to the /etc/samba/smb.conf file, type testparm to verify that the file is OK. The testparm command checks the /etc/samba/smb.conf file and reports if the file is OK or not. After that, restart the SMB services with the following command:

```
/etc/rc.d/init.d/smb restart
Shutting down SMB services: [ OK ]
Shutting down NMB services: [ OK ]
Starting SMB services: [ OK ]
Starting NMB services: [ OK ]
```

The first two lines may show [FAIL] if SMB services were not already running. You can ignore this error message.

## Accessing the Samba server

You can now try to access the Samba server on the Red Hat Linux system from one of the Windows systems on the LAN. Perform these steps to do so:

- Double-click the Network Neighborhood icon on the Windows desktop. This should open up the Network Neighborhood window (see Figure 15-5) with all the other Windows systems on the LAN.

![](img/5fe8f856723cde0b366f73584b9e64b8_178_0.png)

- Click the Red Hat Linux Samba server's icon to see its server string. Notice from the comment in the lower-left corner of Figure 15-5 that luther is actually a Linux system, as specified in the Samba configuration file.
- If you do not see the Red Hat Linux Samba server in the Network Neighborhood screen in Windows, select Start-> Find-> Computer. Then type in the Linux system's host name (see Figure 15-6) and click the Find Now button. The Red Hat Linux Samba server should then show up on the screen.

![](img/5fe8f856723cde0b366f73584b9e64b8_178_1.png)

Once you see the Linux Samba server, you can open it by double-clicking the icon. This should show folders for each shared directory in the Linux Samba server. You can then open those folders to further explore the contents of the directories. When you finish browsing the Samba server, you can close the Network Neighborhood.

## Accessing Windows resources with smbclient

You can use the smbclient program to access shared directories and printers on Windows systems on the LAN as well as to check that your Linux Samba server is working. One quick way to check is to use the smbclient -L command to view the list of services on the Linux Samba server itself.

If you have other Windows servers on the LAN, you can look at their services with the smbclient program. Here is the smbclient command that one user types to view the services on a Pentium II PC running Windows 98:

```
smbclient -L phillip
```

You can also use smbclient to access a disk on a Windows server, as well as send a file to a Windows printer. The smbclient program is similar to ftp, in that you connect to a Windows server and then use commands to exchange files and send files to the printer.

The following example shows how one user implements smbclient to access a disk on his Windows 98 PC and view its directory (he types the command in a terminal window):

```
smbclient //phillip/c kwall
added interface ip-192.168.0.1 bcast-192.168.0.255 mask-255.255.255.0
Got a positive name query response from 192.168.0.2 ( 192.168.0.2 )smb: \> dir *.txt
BOOTLOG.TXT AH 13754 Wed Jul 18 01:14:06 2001
FRUNLOG.TXT A 1012 Wed Jul 18 00:59:32 2001
SETUPLOG.TXT AH 14646 Wed Jul 18 01:07:06 2001
NETLOG.TXT A 16076 Wed Jul 18 01:07:06 2001
DELOG.TXT ARS 69973 Wed Jul 18 01:01:58 2001

34728 blocks of size 131072. 26814 blocks available
smb: \> quit
```

To see a list of smbclient commands, type help at the smb: \> prompt. To familiarize yourself with smbclient, you may want to try out some of these commands. Note that the smbclient commands are similar to MS-DOS commands.

## REVIEW

This session showed you how to use NFS to share files among a Red Hat Linux system and other Linux or UNIX systems. Then you learned how to configure your Red Hat Linux system as a Windows server using the Samba software package.
