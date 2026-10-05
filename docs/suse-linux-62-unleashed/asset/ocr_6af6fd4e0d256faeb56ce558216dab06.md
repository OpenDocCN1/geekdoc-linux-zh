# Networking and Internet Services
PART II

the UNIX group database if the name is not found. There are other possible prefixes that are explained in detail in the smb.conf man page.

# invalid users= (S)

This is a list of users who cannot access this share. This list overrides any users in the valid users= option for the share.

```
[ateam]
valid users = myuid,tacket,art
invalid users = myuid,tacket
```

This smb.conf snippet allows only art to access [ateam].

# read list= (S)

The value is a list of users to be given read-only access. This overrides any read-only= writable, and so on, restricting the list to read-only access. If any user on the read list= is also on the write list= option for the share, read list= is overridden and that user can write in the directory.

Does read list= override valid users? That's an interesting question. When a user not appearing in an existing valid users= list for the share appears in the read list= list, that user is prompted for a password. No matter what password is input, the user is kicked out. This behavior is exactly mirrored by Samba's smclient program and Windows Network Neighborhood. The following is an example:

```
[spec_dir]
path = /home/everyone/spec
valid users = valerie,tacket
writeable = yes
read list = valerie,tacket,myuid
write list = tacket
```

In the preceding example, the myuid(/home/everyone/spec directory can be read by Valerie and tacket, but not by myuid (no valid users= entry for myuid). Valerie cannot write the directory because her entry in read list= overrides the writeable= option. Tacket can write it because her write list= entry overrides her read list= entry.

# write list= (S)

Any share can have a list of users who can write to that share, no matter what the writeable= or read list= options say. The following is an example giving write access to [billsdir] for bill, tacket, and myuid, in spite of the fact that the directory is opted to be read-only: