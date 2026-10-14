```
sys:x:3:3::/
 adm:x:4:4:Admin:/var/adm:
 lp:x:71:8:Line Printer Admin:/usr/spool/lp:
 smtp:x:0:0:Mail Daemon User:/
 nuucp:x:9:9:uucp
 Admin:/var/spool/uucppublic:/usr/lib/uucp/uucico
 listen:x:37:4:Network Admin:/usr/net/nis:
 nobody:x:6001:60001:Nobody:/
 noaccess:x:60002:60002:No Access User:/:
 nobody4:x:65534:65534:SunOS 4.x Nobody:/:
 +@systems::0:0::
 +@usergroup1::0:0::
 +@usergroup2::0:0::
 +user3::0:0::
 +:0::/bin/false
```

Users whose login names belong to one of the three netgroups: systems, usergroup1, and usergroup2 are authorized to access the host (the @ sign designates an NIS netgroup). A single user, user3, is also given access.

The last line gives access to everyone. The user shell field is overridden by the local entry and replaced by /bin/false. Therefore, this last line acts as a "deny all" statement, as /bin/false is not a valid user shell.

In the future, host access restrictions will be performed using LDAP (as a replacement for NIS) and an equivalent of the netgroup structure. User authentication through LDAP now requires the use of a special PAM module. This module, supported as open source, is called pam_ldap and can be found at http://www.padl.com/pam_ldap.html.

A good practice for UNIX systems is to disable direct remote access by the root administrator account. This limits access to the console of the system to only the root account and to an already authenticated user via the use of su. The general scenario is that the system administrator logs on using their regular login name (corresponding to their personal account) and then becomes root using the su command.

Unfortunately, the root password used by the su command will be transmitted unencrypted, but unless an outsider has both the root password and a user password, they will be unable to compromise the root account on the system. The use of an encryption channel, such as using SSH as described before, decreases this last risk.

+   Under Solaris, root logins are restricted by editing the /etc/default/login file and by uncommenting the following line:
+   CONSOLE=/dev/console

+   Under HPUX, root access restrictions are done by editing the file /etc/securetty and by listing the terminals where direct root