```
browseable = no
writable = yes
```

Here is how you can change these parameters.

+   - **comment.** Exactly what its name suggests. Set this to whatever you wish.
+   - **browseable.** Controls whether or not home directories are visible in a browser list (such as the Network Neighborhood) or when the NET VIEW command is used from the Windows command prompt. Set this to yes or no depending on your needs.
+   - **writable.** Controls whether or not a user can write to her own home directory. For most practical purposes, this needs to be set to yes. If you set this to no, a user will have read-only access to her own home directory.

# Setting the [printers] paramters

The [printers] section is useful only if you have one or more printers attached to your Red Hat Linux system. The default [printers] configuration is as follows:

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

Here is how you can change these parameters.

+   - **comment.** Exactly what its name suggests. Set this to whatever you wish.
+   - **path.** Set this to the directory where printer data files will be spooled. If you have a lot of users, make sure you have plenty of disk space for this directory.