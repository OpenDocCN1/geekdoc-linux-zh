```
xfs:x:43:
named:x:25:
ntp:x:38:
gdm:x:42:
htt:x:101:
pvm:x:24:
canna:x:39:
wnn:x:49:
dovecot:x:97:
postdrop:x:90:
postfix:x:89:
mailman:x:41:
netdump:x:34:
quagga:x:102:
quagga:x:92:
radvd:x:75:
radiusd:x:95:
ldap:x:55:
mysql:x:27:
postgres:x:26:
fax:x:78:
nut:x:57:
proxy:x:73:
tomcat:x:53:
exim:x:93:
user1:x:500:
[root@server1 root]# _
```

From the preceding output, the “bin” group has a GID of 1, and three users as members: root, bin, and daemon.

# ### Creating User Accounts

You can create user accounts on the Linux system by using the `useradd` command, specifying the user name as an argument, as shown next:

```
[root@server1 root]# useradd bobg
[root@server1 root]# _
```

In this case, all other information such as the UID, shell, and home directory location are taken from two files that contain user account creation default values.

The first file, `/etc/login.defs`, contains parameters that set the default location for e-mail, password expiration information, minimum password length, range of UIDs and GIDs available for use, as well as specifying whether to create home directories by default.