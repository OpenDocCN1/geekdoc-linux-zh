# Doing the Samba



3.13.1.4 LDAP is another way of centrally storing user data. There are several LDAP servers available, one of which is OpenLDAP (www.openldap.org). Samba can use an LDAP server to store the user account information that is normally stored in the smpasswd file. When combined with some software from padl.com and changes in the nsswitch file, a Linux box can share both UNIX UIDs and Windows SIDs across the enterprise. This works by extending the standard Posix LDAP schema to include the Windows encrypted passwords and SIDs.

When using LDAP, you will want to use the following options:

```
[global]
security = user
ldap admin dn = ldapadmin # or whatever you choose
ldap server = ldap.yourdomain # or localhost or ...
password server = # no password server
```

As of version 2.2.3, the LDAP interface is considered to be stable and safe to use. One of the great things about using an LDAP server is that little unbound, the Linux UIDs will be consistent from machine to machine, making it possible to use Samba and NFS on the same group servers and enforce a common security model across all the servers. When you outgrow your current Samba server, you can simply add another and reuse all of the user accounts, UIDs, and Windows information (SIDs, passwords, etc.).

3.13.2 Logon Services. Samba has the ability to store user profiles and logon scripts. These are DOS formatted scripts and information that could be corrupted if allowed to be accessed by untrusted users. Imagine a rogue user adding a command to the logon script to connect to his local box and install a malicious program. Keep these secured and accessible only by the people who need to modify them. At least set them as read-only to users other than root.

# 3.8.14 Samba Management Security

Swat is a lovely tool that I have never found a reason for. Once a Samba server is set up, it does not normally require constant system-administrator attention. Therefore, it is not necessary to have the super server listen on a given port (901 usually) for the system administrator or a cracker to try and break in.

If you decide to use swat, restrict how instances of it can be started and where it can be accessed from. And, if someone is trying to access it, keep track of who it is by logging them. A typical secured xinetetd file will look something like this:

```
service swat {
port = 901
socket_type = stream
wait = no
only_from = 192.168.1.100
```