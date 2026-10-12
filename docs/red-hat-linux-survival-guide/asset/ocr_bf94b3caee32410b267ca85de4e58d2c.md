name) cannot be resolved to an IP address. If you set this parameter to yes, the nmbd server treats the NetBIOS name as an Internet domain name and tries to resolve it by using the DNS protocol. Keep the default setting.

# Setting the [homes] parameters

The [homes] section is a special configuration section that allows you to set up home directory access from Windows systems. In other words, a user with a valid username/password on the Red Hat system can access her home directory on the Linux system from a Windows system. The default [homes] configuration is as follows:

```
[homes]
    comment = Home Directories
    browseable = no
    writable = yes
```

Here is how you can change these parameters:

+   - **comment.** Exactly what its name suggests. Set this to whatever you wish.
+   - **browseable.** Controls whether or not home directories are visible in a browser list (such as the Network Neighborhood) or when the NET VIEW command is used from the Windows command prompt. Set this to yes or no depending on your needs.
+   - **writable.** Controls whether or not a user can write to his or her own home directory. For most practical purposes, this should be set to yes. If you set this to no, a user will have only read-only access to her own home directory.

# Setting the [printers] parameters

The [printers] section is of interest only if you have one or more printers attached to your Red Hat Linux system. The default [printers] configuration is as follows:

```
[printers]
    comment = All Printers
    path = /var/spool/samba
```