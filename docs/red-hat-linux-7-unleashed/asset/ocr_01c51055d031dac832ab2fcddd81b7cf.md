root
udp     0     0 localhost:domain    .:*
udp     0     0 svr01.mk.net:domain .:*
udp     0     0 poto.mk.net:domain .:*
udp     0     0 stats.mk.net:domain .:*
udp     0     0 home.mk.net:domain .:*
udp     0     0 www.mk.net:domain .:*
udp     0     0 www.cmf.net:domain .:*

Active UNIX domain sockets
Proto ReCtTn Flags Type State Path
unix 2  [  ]  SOCK_STREAM UNCONNECTED 1605182
unix 2  [  ]  SOCK_STREAM UNCONNECTED 1627039
unix 2  [  ]  SOCK_STREAM CONNECTED 1652605

# newgrp

newgrp is used to enter a new group. You can use this command to temporarily become a member of a different group so you can access or work on different files or directories.

# passwd

For the normal user (non-superuser), no arguments are used with the passwd command. The command asks the user for the old password. Following this, the command asks for the new password twice, to make sure it was typed correctly. The new password must be at least six characters long and must contain at least one character that is either upper-case or not a letter. Also, the new password cannot be the same password as the one being replaced, nor can it match the user's ID (account name).

If the command is run by the superuser, it can be followed by either one or two arguments. If the command is followed by a single user's ID, the superuser can change that user's password. The superuser is not bound by any of the restrictions imposed on the user. If there is an argument after the single user's ID, that argument becomes that user's new password.

# pdksh

This public domain Korn shell is a workalike shell with features nearly compatible to the commercial Korn shell, and is found on your Linux system with the name ksh.

# pico

The pico command is a handy, virtually crash-proof text editor that is part of the pine mail program's software distribution. One handy command-line option is -w, which disables line wrapping. (This is useful when you are manually configuring system files.) pico performs spell-checking of text files, but does not print.