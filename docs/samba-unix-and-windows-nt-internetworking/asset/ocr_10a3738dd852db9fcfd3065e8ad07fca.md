```
# A publicly accessible directory, read/write to all users. Note
that all files
# created in the directory by users will be owned by the default
user, so
# any user with access can delete any other user's files.
Obviously this
# directory must be writable by the default user. Another user
could of course
# be specified, in which case all files would be owned by that
user instead.
;[public]
; path = /usr/somewhere/else/public
; public = yes
; only guest = yes
; writable = yes
; printable = no

# The following two entries demonstrate how to share a directory
# so that two
# users can place files there that will be owned by the specific
users. In this
# setup, the directory should be writable by both users and
should have the
# sticky bit set on it to prevent abuse. Obviously this could be
extended to
# as many users as required.
;[myshare]
; comment = Mary's and Fred's stuff
; path = /usr/somewhere/shared
; valid users = mary fred
; public = no
; writable = yes
; printable = no
; create mask = 0765
```

# Bibliography

# Overview

Jeremy Alison, "Doing the NIS/NT Samba," Linux World, October 1998.

John D. Blair, "Samba: Integrating UNIX and Windows," Specialized Systems Consultants, Inc., 1998.

Jim Boyce Christa Anderson, Axel Larson, et al., "Windows NT Workstation 4.0 Advanced Technical Reference," Indianapolis, IN: Que Corporation, 1996.

Eric Car, "The New King of the Hill," Sm@rt Reseller Online, ZDNet, Ziff-Davis, Inc., April 5, 1999.