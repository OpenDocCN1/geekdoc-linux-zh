to the service request. If the service is not found, Samba checks whether there is a [homes] section. If the [homes] section exists, the password file is searched to find the home directory for the user making the request. Once this directory is found, the system shares it with the network:

```
[homes]
browseable = no
writable = yes
```

The preceding is the simplest usable [homes] share. The browseable=no entry instructs the SMB client not to list the share in a browser (such as Windows Explorer). However, [homes] is a special case. The user share it represents will be visible in the client browse list even if [homes] contains browseable=no. If [homes] were to contain browseable=yes, a share called homes would actually appear in the client browse list. The writable=yes entry enables the user to write to the directory, which is typically the desired situation in home directories.

# Note

The writable= parameter has two synonyms, writeable= and write ok=, and one inverse synonym, read only=. Thus, these four lines perform identically:

```
writable=yes
writeable=yes
write ok=yes
read only=no
```

In general, Samba has excellent defaults, making the preceding [homes] configuration practical. The following [homes] share contains additional parameters:

```
[homes]
comment = Home Directories
browseable = no
read only = no
path = %H/smbtree
create mode = 0750
```

The comment entry is a human-readable share identification string to be displayed by the client user interface. Note that comment= is similar to server string=, but the latter is only valid in the [global] section. The read only= parameter is an inverse synonym of writable=, and was explained previously. Also explained previously was the browseable= parameter.