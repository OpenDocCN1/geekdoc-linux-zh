When you type the umask command, the command returns a four-number output such as 0245. As of this writing, the first number in the umask output is always 0 and is not used. In the future, this first number may be usable to allow for new files that automatically include the SUID or SGID bits.

Also, no matter what the value of umask, new files in Red Hat Enterprise Linux can no longer be automatically created with executable permissions. In other words, a umask value of 0454 leads to identical permissions on new files as a umask value of 0545. You need to use commands such as chmod to set executable permissions on a specific file.

# The Default umask

With that in mind, the default umask is driven by the /etc/bashrc file, specifically the following stanza, which drives a value for umask depending on the value of the UID:

```
if [ $UID -gt 199 ] && [ "`id -gn`" = "`id -un`" ]; then
  umask 002
else
  umask 022
fi
```

In other words, the umask for user accounts with UIDs of 200 and above is 002.

In contrast, the umask for UIDs below 200 is 022. In RHEL 6, service users such as adm, postfix, and apache have lower UIDs; this affects primarily the permissions of the log files created for such services. Of course, the root administrative user has the lowest UID of 0. By default, files created for such users have 644 permissions; directories created for such users have 755 permissions.

In contrast, regular users have a UID of 500 and above. Files created by such users normally have 664 permissions. Directories created by such users normally have 775 permissions.

# Commands to Change Permissions and Ownership

Key commands that can help you manage the permissions and ownership of a file are chmod, chown, and chgrp. In the following subsections, you'll examine how to use those commands to change permissions along with the user and group that owns a specific file, or even a series of files.