And:

session optional pam_mount.so

The auth line should go before the pam_unix and pam_winbind lines. The session line should go in the session section. Remember to append a use_first_auth argument to each auth line; otherwise, a second password prompt will be triggered by the pam_mount line.

The pam_mount module has its own configuration file /etc/security/pam_mount.conf. This file contains settings such as where the mount um commands are found, debug settings, which mount points should be created, and which file systems should be mounted for which users.
nA minimum pam_mount.conf file for mounting SMB shares looks like Example 9-23 on page 217.

# 9.7 How to use network printers in the domain

Being able to use existing printers is one of the most important preconditions for a new type of client in any environment. We do not want to keep separate printing environments for every type of client.
This means that the Linux client has to use the (network) printers available in the domain. We can achieve this in two ways:

+   - Print directly to the printer using its network interface.
- Print to the printer using the Windows print server and its SMB interface.

Both options are available using CUPS from the Linux client. We suggest using the second option, however, since all printing in the domain (and user's environment) is equal. This means there are just prints and not Windows prints and Linux prints.
You need to be running CUPS on the Linux client. Check this by:

```
/etc/init.d/cups status
```

This should return that CUPS is running and give its PID. If not, start it using:
/etc/init.d/cups start