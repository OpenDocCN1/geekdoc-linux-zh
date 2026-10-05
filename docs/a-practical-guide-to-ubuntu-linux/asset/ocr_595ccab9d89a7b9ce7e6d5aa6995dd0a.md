# INTRODUCTION TO SAMBA

# MORE INFORMATION

Local Samba/swat home page has links to local Samba documentation (page 804)
Documentation: /usr/share/samba-doc-*

Web Samba: www.samba.org (mailing lists, documentation, downloads, and more)
CIFS: www.samba.org/cifs

HOWTO Unofficial Samba HOWTO: hr.uregon.edu/davidrl/samba.html
Samba Documentation Collection: Point a browser at /usr/share/doc/samba-doc/
htmldocs/index.html; if you have installed the samba-doc-pdf package, look in
/usr/share/doc/samba-doc-pdf.

# NOTES

Firewall The server normally uses UDP ports 137 and 138 and TCP ports 139 and
445. If the Samba system is running a firewall, you need to open these ports.
Using gufw (page 876), open these ports by setting a policy that allows service for
amba.

Share Under Samba, an exported directory hierarchy is called a share.

Mapping a share The term mapping a share is equivalent to the Linux term mounting a direc-
tory hierarchy.

Samba The name is derived from SMB (page 1172), the protocol that is the native
method of file and printer sharing for Windows.

swat You must use a root password to use swat to change the Samba configuration; see
page 431 for instructions.

# SAMBA USERS, USER MAPS, AND PASSWORDS

For a Windows user to access Samba services on a Linux system, the user must prov-\ide a Windows username and a Samba password. In some cases, Windows supplies
the username and password for you. It is also possible to authenticate using other
methods. For example, Samba can use LDAP (page 1156) or PAM (page 478)
stead of the default password file. Refer to the Samba documentation for
information on authentication methods.

names The username supplied by Windows must be the same as a Linux username or must
map to a Linux username.

User maps You can create a file, typically named /etc/samba/susers, to map user-
names to Linux usernames. For more information see username map on page 811.

Passwords By default, Samba uses Linux passwords to authenticate users. However, Ubuntu
sets passdb backend (page 809) to tdsams, causing Samba to use tribal database
passwords. Change this parameter to smbpasswd in smb.conf (page 807) to cause
samba to use Linux passwords.