The preceding works only if root creates the user’s subdirectory, mode 0700, and changes group and owner to that of the user. This is not the best way to accomplish this task. It’s merely a demonstration of the `%u` substitution. Note that the directory creation could also be accomplished with a root preexec= script.

# read only= Versus writeable= Versus
writable= Versus write ok= ($)

writeable=, writable=, and write ok= are synonyms, meaning they completely substitute for each other. read only= is an inverted synonym for writeable=, writable=, and write ok=, meaning that a read only=yes substitutes for a writeable=no, and a read only=no substitutes for a writeable=yes, and so on. Only one of these four options needs to specify whether a share is writeable. If this option is specified in the [global] section, it serves as a default for all shares. (This is true of all options that can be put in share definitions.) Note that these options can be overridden by the write list= option.

```
```
read only=no
writeable=yes
writable=yes
write ok=yes
```
```

All four mean the same thing and are interchangeable. The default is read only=yes.

# valid users= ($)

The lack of this option or a blank value following the equal sign in any share makes the share accessible to everyone (probably not what you want). To limit access, place a comma-delimited list of valid users after the equal sign:

```
```
valid users = myuid, tackett, @acct
```
```

This option gives access to users myuid and tackett, and group acct. This option is overridden by the invalid users= option.

# invalid users= ($)

This is a list of users who cannot access this share. This list overrides any users in the valid users= option for the share.

```
```
[team]
valid users = myuid, tackett, art
invalid users = myuid, tackett
```
```

This smb.conf snippet allows only art to access [team].