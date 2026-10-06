
# Part IV: Fedora RHEL Network and Server Setup

- guest ok — Select Yes to enable any access to this directory without requiring a password.
- hosts allow — Add the names of the computers that will be allowed to access this file system. You can separate hostnames with commas, spaces, or tabs. There are some valid ways of entering hostnames:
  - localhost — Allow access to the local host.
  - 192.168.74.18 — IP address. Enter an individual IP address.
  - 192.168.74.— Enter a network address to include all hosts on a network. (Be sure to put a dot at the end of the network number or it won't work!)
  - maple, pine — Enable access to individual hosts by name.
  - EXCEPT — If you are allowing access to a group of hosts (such as by entering a network address), use EXCEPT to specifically deny access from one host from that group.
- hosts deny — Deny access to specific computers by placing their names. By default, no particular computers are excluded. Enter hostnames in the same format you used for hosts.
- browseable — Indicates whether you can view this directory on the list of shared directories. This is on (Yes) by default.
- available — Enables you to leave this entry intact, but turns off the service. This is useful if you want to close access to a directory temporarily. This is on (Yes) by default. Select No to turn it off.

5. Select Commit Changes.

At this point, the shared file systems should be available to the Samba client computers (Windows 9x, Windows NT, Windows 2000, Windows Vista, Mac OS X, OS/2, Linux, and so on) that have access to your Linux Samba server. Before you try, however, you can check a few things about your Samba configuration.

# Checking your Samba setup with SWAT

From the SWAT window, select the STATUS button.

From this window, you can restart the smbd and nmbd processes. Likewise, you can see lists of active connections, active shares, and open files. The preferred way is to set the smbd and nmbd daemons to set up the samba service to start automatically. Type chkconfig smb in a Terminal window to set the service to start at boot time.

# Working with Samba files and commands

Although you can set up Samba through the Server Configuration window or SWAT, many administrators prefer to edit the /etc/samba/smb.conf directly. As root user, you can view the contents of this file and make needed changes. If you selected user security (as recommended, you will also be interested in the smbusers and smbpasswd file (also in the /etc/samba directory). These files, as well as commands such as testpar and smbstatus, are described in the following sections.

# Editing the smb.conf file

Changes you make using the Samba Server Configuration window or SWAT Web interface are reflected in your /etc/samba/smb.conf file. Here's an example of an smb.conf file (with comments removed):

```
[global]
workgroup = ESTREET
server string = Samba Server on Maple
hosts allow = 192.168.0.
printcap name = /etc/printcap
loader printers = cups
log file = /var/log/samba/%m.log
max log size = 0
smb passwd file = /etc/samba/smbpasswd
security = user
encrypt passwords = Yes
unix password sync = Yes
passwd program = /usr/bin/passwd %u
passwd chat = *New*password* %n\n *Retype*new*password* %n\n *passwd:\n*all*authentication*tokens*updated*successfully*
p password change = yes
obey socket options = TCP_NODELAY SO_RCBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbusers
dns proxy = no
```

```
[homes]
comment = Home Directories
browseable = yes
writable = yes
valid users = %S
create mode = 0664
directory mode = 0775
```

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = no
```

In [global] section, the workgroup is set to STREET, the Samba Server on Maple, and only computers that are on the local network (192.168.0. ) are allowed access to the Samba service. You must change the 'hosts allow =' parameter to match your network.

Definitions for the local printers that will be shared from the /etc/printcap file, the printers are loaded (yes), and the cups printing service (which is the default print service used by Fedora and RHEL).

Separate log for each host trying to use the service are created in /var/log/samba/%m.log (with %m automatically replaced with each host). There is no limit to log for file size (0).

In this case, we use user-level security (security = user). This allows a user to log in once and easily access the printers and the user's home directory on the Linux system. Password encryption is on (encrypt passwords = yes) because most Windows systems have password encryption by default. Passwords are stored in the /etc/samba/smbpasswd file on your system.

The dns proxy = no options prevents Linux from looking up system names on the DNS server (for TCP/IP lookups) when they can't be found on registered NetBIOS names.

The [homes] section allows each user to be able to access his her home directory from a Windows system on the LAN. The user will be able to write to the home directory. However, other users will not be able to share this directory. The [printers] section allows all users to print any printer that is configured on the local Linux system.

# Adding Samba users

Doing user-style Samba means assigning a user account to each person using the Linux file system and printers from his or her Windows workstation. (You could assign users to a guest account instead, but in this example, all users have their own accounts.) Then you need to add SMB passwords for each user. For example, here is how you would add a user whose workstation location is chuckp:

1. Type the following as root user from a Terminal window to add a Linux user account:

```
# useradd -m chuckp
```

2. Add a password for the user as follows:

```
# passwd chuckp
Changing password for user: chuckp
New password: ********
Retype new password: ********
```

3. Repeat the previous steps to add user accounts for all users on your LAN you want to give access.

4. Type the following command to create the Samba password file (smbpasswd):
```
# cat /etc/passwd | /usr/bin/smbpasswd.sh > /etc/samba/smbpasswd
```

5. Add an SMB password for the user as follows:
```
# smbpassword chuckp ********
New SMB password: ********
Retype SMB password: ********
```

(The smbpassword -a user command can be used to create the smbpassword file at the same time you set user password.) Repeat this step for each user. Later, each user can log in Linux and run the passwd and smbpassword commands to set private passwords.

> NOTE: In the most recent version of Samba, options are available in the smb.conf file that cause SMB and Linux passwords to be synchronized. Descriptions of the passwd program, passwd chat, and UNIX password sync options are in the SWAT section of this chapter.

# Starting the Samba service

To start the Samba and NMB daemons, you can run the /etc/init.d/smb start-up script by typing it as the root:

```
# service smb start
```

This runs the Samba service during the current session. To set up Samba to start automatically on your Linux system starts, type the following:

```
# chkconfig sm on
```

This turns on the Samba service to start automatically in run levels 3, 4, or 5. You can now check SMB clients on the network to see if they can access your Samba server.

# Testing your Samba permissions

You can run several commands from a shell to work with Samba. One is the testpar command, which you can use to check the access permissions you have set up. It lists global parameters that are set, along with shared directories and printers.

 Checking the status of shared directories

The mbstatus command can view who is currently using Samba shared resources offered from your Linux system. The following is an example of the output from smbstatus:

```
# smbstatus
```

Samba version 3.2.4-0.22.fc10
