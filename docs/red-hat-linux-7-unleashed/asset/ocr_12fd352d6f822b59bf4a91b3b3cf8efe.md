# autogroup

The autogroup command provides tighter controls of anonymous users by automatically assigning them a certain group permission when they log in. The format of the autogroup line follows:

```
autogroup groupname class [class ...]
```

groupname is the name of the group to which you want the anonymous users set and class is the name of a class that is defined by using the class command. You can have multiple class entries for an autogroup. Only the anonymous users referenced in class will be affected by autogroup.

Remember, the group to which you are providing user permission must be in the /etc/group file.

# deny

The deny command enables you to explicitly deny service to certain hosts based on their names, their IP addresses, or whether their hostnames can be reverse-resolved via DNS. The format of the deny command is as follows:

```
deny addrglob message_file
```

addrglob is a regular expression containing the addresses that are to be denied and message_file is the filename containing a message that should be displayed to the hosts when they connect.

The following is a sample deny line:

```
deny evilhacker.domain.com /home/ftp/.message.no.evil.hackers
```

This line displays the contents of the file /home/ftp/.message.no.evil.hackers to anyone trying to connect via FTP from evilhacker.domain.com. To deny users access based on whether their IP addresses can be reverse-resolved to their hostnames, use the string 1nreserved for the addrglob entry.

# guestgroup

The guestgroup command is useful when you want to provide your real users with restrictive FTP privileges. The format of the command is as follows:

```
guestgroup groupname [groupname ...]
```

groupname is the name of the restricted group (as taken from /etc/group).

When a user's group is restricted, the user is treated much like an anonymous visitor; thus, the user's account requires the same setup as for anonymous visitors. Also, the user's password entry is a little different in the directory field.