```
# by the default user. Another user could of course be specified,
# in which case all files would be owned by that user instead.
;[public]
; path = /usr/somewhere/else/public
; public = yes
; only guest = yes
; writable = yes
; printable = no
```

Finally, this is another variation on the User Private Group scheme, which creates a group directory. Unlike the [public] stanza, this share is private.

```
# The following two entries demonstrate how to share a directory so
# that two users can place files there that will be owned by the
# specific users. In this setup, the directory should be writable
# by both users and should have the sticky bit set on it to prevent
# abuse. Obviously this could be extended to as many users as required.
;[myshare]
; comment = Mary's and Fred's stuff
; path = /usr/somewhere/shared
; valid users = mary fred
; public = no
; writable = yes
; printable = no
; create mask = 0765
```

# Let Samba Join a Domain

If you've configured a Samba server, and it's not the DC for the network, you may need to configure as a member of the domain. To do so, you can configure an account on the DC for the network. As long as there's one domain on this network, it's easy to do with the following command:

```
# net rpc join -U root
```

If there is more than one domain available, substitute the name of the controller for DC in the net rpc join -S DC -U root command. This assumes that the user named root is the administrative user on the DC. However, the administrative user on a domain governed by a Microsoft Windows computer is administrator. If the command successful, it prompts for that user's password on the remote DC. The result adds an account for the local computer to the DC's user database in /etc/passwd.