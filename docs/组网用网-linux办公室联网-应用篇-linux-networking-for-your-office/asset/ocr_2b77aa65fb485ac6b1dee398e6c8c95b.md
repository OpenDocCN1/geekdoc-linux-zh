# Note

The smbmount syntax changed between Samba versions 2.0.3 and 2.0.5a. If you're using 2.0.3, you should type

```
smbmount //nessus/shared-c 'mount /mnt/nessus'
```

to mount a remote Samba share. Also, Red Hat moved the Samba client programs into a separate RPM file with version 2.0.5a, so if you can set up a Samba server, but can't access the client programs, check to see that the samba-client package is installed. If it's not, install it (you can find a link to it in the updates directory on the CD-ROM that accompanies this book).

After you type this command, smbmount asks for a password. (You can instead type a password on the command line, immediately after the share name, but then it is visible for all who walk past the see.) If you type a valid password, you gain access to the remote share.

If you're using pre-2.0.5a versions of smbmount, you can provide additional parameters within the single quotes, to modify the permissions and ownership of files in the mounted share:

+   - u—Specifies the user ID to be used by all files in the share.
+   - g—Specifies the group ID to be used by all files in the share.
+   - f—Specifies the permissions, in octal form, to be assigned to files on the share. These permissions can't exceed those given by the server, though—if a file is marked read-only on the server, you can't override that through this option. You can, however, change permissions with the Linux chmod command after the share has been mounted.
+   - d—Specifies the permissions, in octal form, to be assigned to directories on the share.

These options do not work with smbmount from the 2.0.5a release, unfortunately. This more recent version gives file ownership to the person who mounts the share, and uses permissions of 755 for all files and directories.

As installed on a Red Hat 6.0 system, smbmount requires that you be root to operate. If you want to give ordinary Linux users the ability to mount remote shares, you can do so; just type the following commands:

```
chmod a+s /usr/bin/smbmnt
chmod a+s /usr/bin/smbumount
```

Note that in the first line, the filename is smbmnt, not smbmount—the former is a helper application to the latter. These commands set the suid bit on the applications, which means that they run with the authority of the superuser even when an ordinary user runs them.