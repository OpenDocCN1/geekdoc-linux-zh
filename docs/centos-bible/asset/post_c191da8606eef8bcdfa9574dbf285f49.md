
view the contents of this file and make needed changes. If you selected user security (as recommended), you will also be interested in the smbusers and smbpasswd files (also in the /etc/samba directory). These files, as well as commands such as testparm and smbstatus, are described in the following sections.

## Editing the smb.conf File

Changes you make using the Samba Server Configuration window or SWAT web interface are reflected in your /etc/samba/smb.conf file. Here's an example of an smb.conf file (with comments removed).

```
[global]
workgroup = MONGO
server string = Samba Server on FlashG
hosts allow = 192.168.0.
printcap name = /etc/printcap
load printers = yes
printing = cups
log file = /var/log/samba/%m.log
max log size = 0
smb passwd file = /etc/samba/smbpasswd
security = user
encrypt passwords = Yes
unix password sync = Yes
passwd program = /usr/bin/passwd %u
passwd chat = *New*password* %n\n *Rety pe*new*password* %n\n *passwd:*\*All*authentication*tokens*updated*successfully*
pam password change = yes
obey pam restrictions = yes
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbusers
dns proxy = no

[homes]
comment = Home Directories
browseable = no
writable = yes
valid users = %S
create mode = 0664
directory mode = 0775

[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

In the `[global]` section, the workgroup is set to MONGO, the server is identified as the Samba Server on FlashG, and only computers that are on the local network (192.168.0.*) are allowed access to the Samba service. You must change the `hosts allow = *` parameter to match your network.

Definitions for the local printers that will be shared are taken from the /etc/printcap file, the printers are loaded (yes), and the CUPS printing service (which is the default print service used by CentOS) is used.

Separate log files for each host trying to use the service are created in /var/log/samba/%h.log (with %h automatically replaced with each hostname). There is no limit to log file size (0).

In this case, we are using user-level security (security = user). This allows a user to log in once and then easily access the printers and the user’s home directory on the Linux system. Password encryption is on (encrypt passwords = yes) because most Windows systems have password encryption on by default. Passwords are stored in the /etc/samba/smbpasswd file on your Linux system.

The dns proxy = no option prevents Linux from looking up system names on the DNS server (used for ICMP/IP lookups) when they can’t be found among registered NetBIOS names.

The `[homes]` section allows each user to be able to access his or her Linux home directory from a Windows system on the LAN. The user will be able to write to the home directory. However, other users will not be able see or share this directory. The `[printers]` section allows all users to print to any printer that is configured on the local Linux system.

### Adding Samba Users

Doing user-style Samba security means assigning a Linux user account to each person using the Linux file systems and printers from his or her Windows workstation. You could assign users to a guest account instead, but in this example, all users will have their own accounts. Then you need to add SMB passwords for each user.

1.  Type the following as root user from a Terminal window to add a Linux user account:
    ```
    # useradd -m alexr
    ```
2.  Add a Linux password for the new user as follows:
    ```
    # passwd alexr
    Changing password for user alexr
    New UNIX password: *******
    Retype new UNIX password: *******
    ```
3.  Repeat the previous steps to add user accounts for all users from Windows workstations on your LAN that you want to give access to your Linux system to.
4.  Type the following command to create the Samba password file (smbpasswd):
    ```
    # cat /etc/passwd | /usr/bin/mksmbpasswd.sh > /etc/samba/smbpasswd
    ```
5.  Add an SMB password for the user as follows:
    ```
    # smbpasswd alexr
    New SMB password: ********
    Retype new SMB password: ********
    ```
    (The `smbpasswd -a user` command can be used to create the `smbpasswd` file at the same time you set a user password.) Repeat this step for each user. Later, each user can log in to Linux and run the `passwd` and `smbpasswd` commands to set private passwords.

> **NOTE** In the most recent version of Samba, options are available in the `smb.conf` file that cause SMB and Linux passwords to be synchronized automatically. See Descriptions of the `passwd` program, `passwd` chat, and UNIX password sync options in the SWAT section of this chapter.

## Starting the Samba Service

To start the Samba SMB and NMB daemons, you can run the `/etc/init.d/smb-start-up` script by typing the following as the *root* user:

```
# service smb start
```

This runs the Samba service during the current session. To set up Samba to start automatically when your Linux system starts, type the following:

```
# chkconfig smb on
```

This turns on the Samba service to start automatically in run levels 3, 4, or 5. You can now check SMB clients on the network to see if they can access your Samba server.

## Testing Your Samba Permissions

You can run several commands from a shell to work with Samba. One is the `testparm` command, which you can use to check the access permissions you have set up. It lists global parameters that are set, along with any shared directories or printers.

## Checking the Status of Shared Directories

The `smbstatus` command can view who is currently using Samba shared resources offered from your Linux system. The following is an example of the output from `smbstatus`:

```
# smbstatus

Samba version 3.0.28-1.el5.2.1
PID Username Group Machine ...
25770 timothy timothy tarnak (10.0.0.50)
25833 timothy timothy 10.0.0.50 (10.0.0.50)

Service     pid     machine     Connected at
IPCS        25729   tarnak      Tue Jan 20 12:06:29 2009
mytmp       25770   tarnak      Tue Jan 20 12:16:03 2009
mytmp       25833   10.0.0.50   Tue Jan 20 12:25:52 2009
IPCS        25730   tarnak      Tue Jan 20 12:06:29 2009

Locked files:
Pid Uid Deny_Mode Access R/W Oplock SharePath Name Time
25833 501 DENY_NONE 0x12019f RDWR NONE /home/timothy/files/
.b.txt.swp Tue Jan 20 12:26:18 2009
```

This output shows that, from your Linux Samba server, the myhome service (which is a share of the /home/timothy/files directory) is currently open by the computer named tarnak. PID 25833 is the process number of the smbd daemon on the Linux server that is handling the service. The file that is open is the /home/timothy/files/b.swap file, which happens to be opened by a vi command. It has Read/Write access.

## Setting Up Samba Clients

Once you have configured your Samba server, you can try using the shared directories from a client computer on your network. The following sections describe how to use your Samba server from another Linux system or from various Windows systems.

### Using Samba Shared Directories from Linux

There are several methods of connecting to shared directories from a Linux client. The following sections address these methods.

### Using Samba from Nautilus

To connect to a Samba share from Nautilus, use the "Open Location" box by clicking File ➤ Open Location. Then type **smb:** in your Nautilus File Manager "Open Location" box.

A list of SMB workgroups on your network appears in the window. You can select a workgroup, choose a server, and then select a resource to use. This should work for shares requiring no password.

The Nautilus interface requires you to either send clear-text passwords or type the user and password into your location box. For example, to get to my home directory (/home/timothy) through Nautilus, I can type my username, password, server name, and share name as follows: **smb://timothy:my72mb@roka/timothy**

Instead of just typing this information into the Location box, you can use the "Connect to Server" feature of Nautilus. Select File ➤ Connect to Server. From the Connect to Server window
