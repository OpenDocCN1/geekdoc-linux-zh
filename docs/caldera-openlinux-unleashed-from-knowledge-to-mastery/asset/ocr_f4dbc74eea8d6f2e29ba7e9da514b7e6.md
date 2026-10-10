You can disable encrypted passwords on Windows clients. The mechanism for doing this varies depending on which version of Windows you are using. For details, see the files `NT4_PlainPassword.reg`, `Win95_PlainPassword.reg`, and `Win98_PlainPassword.reg` in `/usr/doc/samba-2.0.3/docs`. You should also look at the documentation files in `/usr/doc/samba-2.0.3/docs/textdocs`, especially the `ENCRYPTION.txt` file.

# # File Shares

After the global configuration options come share configurations. Each share section specifies a resource to be shared with Windows clients. Continuing with the sample configuration file, here is a section which that shares the CD-ROM volume:

```
```# Make the CD-ROM available to anyone read-only
[cdrom]
    path = /mnt/cdrom
    public = yes
    writable = no```
```

The [cdrom] section creates a share called cdrom. The path specifies which directory is to be shared. Any Windows client accessing the share will see the directory tree rooted at /mnt/cdrom.

The `public = yes` option specifies that anyone may access the share without a password. The Samba daemon changes its user ID to nobody when a public connection is made. The `writable = no` option provides read-only access, which is certainly to be expected for a CD-ROM device.

I have set up the cdrom share on `shishi`. From the test Windows machine, the resource is known as `\\shishi\cdrom`. Windows names network resources as two backslashes followed by the server name, another backslash, and the share name.

Samba supports a special kind of share called [homes]. Here is an example:

```
```[homes]
    valid users = %$S
    only user = yes
    user = %$S
    writable = yes
    create mask = 0750```
```

The share is special because it creates artificial shares based on the user name. If, for example, user `dfs` connects to a share called `dfs`, Samba first looks for a share named `dfs` in the `smb.conf` file. Not finding one, it checks for the presence of a homes share. If this exists, and if `dfs` has an entry in the UNIX password file, the homes share is cloned with a default path equal to the user's home directory. In essence, this makes `\\servername\default` map to `username`'s home directory (as long as `username` has an entry in the UNIX password file).