configuration options. Still, you should review that file and add your own settings before running a Samba server. A very basic smb.conf file is shown here:

```
[global]
workgroup = MYPLACE
netbios name = sundance
server string = Samba on Linux posing as Windows 2000
hosts allow = 192.168.100.
printcap name = /etc/printcap
load printers = yes
printing = lprng
log file = /var/log/samba.log
max log size = 0
security = user
encrypt passwords = yes
smb passwd file = /etc/samba/smbpasswd
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
dns proxy = no

[homes]
comment = User home directories
browseable = no
writable = yes

[printers]
comment = Linux printers
path = /var/spool/samba
browseable = no
guest ok = no
printable = yes
```

The smb.conf file is divided into sections. The [global] section defines the overall operation of the server. Other sections define how the server handles shared resources: either the printers or specific file system shares (directories that you want to share). The [homes] and [printers] sections are standard names that refer to the home directories of each user who logs in and the Linux printers, respectively. You can create other sections to define other shares.

# Creating Samba Users

Although the sample configuration file settings above are sufficient to start a basic Samba server, the recommended user-based security model requires that each user must log in with a valid user name and password before using a share on the Samba server. It's common to allow everyone with a Linux user account to also log in via Samba. Several utilities included with the Samba suite make this easy to implement. Assuming that you have created all your Linux user accounts, the following command creates a Samba password file for all your Linux users:

```
# cat /etc/passwd | mksmbpasswd.sh > /etc/samba/smbpasswd
```