# Chapter 27 ♦ Running a File Servers 743

```
[printers]
comment = All Printers
path = /var/pool/samba
browable = no
guest ok = no
writable = no
printable = yes
```

I won't go through every line of this example, but here are some observations. In the [global], the group is set to ESTREE, the server is identified as the Samba Server on Map, and only computers that are on the local network (192.168.0.) are allowed access to the Samba service. You must change the local network to match your network.

Definitions for the local printers that will be shared are taken from the /etc/print file, the printers are loaded (yes), and the CUPS printing service is used.

Separate logs for each host trying to use the service are created in /var/log/samba/$m.log automatically replaced with each host name. There is no limit to log file size (0).

This example uses the user-security (security = user), which allows a user to log in once and then easily access the printers and the user's home directory on the Linux system. Password encryption is on (encrypt passwords = yes) because most Windows systems have password encryption by default. Passwords are stored in the /etc/samba/smbpasswdd file on your Linux system.

The dns proxy = no option prevents Linux from looking up system names on the DNS server (used for TCP/IP lookups).

The [homes] section enables each user to access his or her home directory from a Windows system on the LAN. The user will be able to write to the home directory. However, other users will not be able to see or share this directory. The [printers] section enables all users to print to any configured printer on the local Linux system.

# Adding Samba Users

Performing user-style Samba security means assigning a user account to each using the Linux file systems and printers from his or her Windows workstation.(You could assign users to a guest account instead, but in this example, all users have their own accounts.) Then you need to add SMB passwords for each user. For example, here is how you would add a user whose Windows workstation login is chuckp:

+   1. Type the following as root user from a Terminal window to add a Linux user account:

```
# useradd -m chuckp
```