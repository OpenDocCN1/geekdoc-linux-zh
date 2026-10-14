As a general rule, a normal user should only have write access in the following directories:

+   - The home directory of the user
+   - The /tmp directory (to store temporary files)

Depending on the purpose of a computer, other directories can be writable by users. For example, if you install a Samba file server, a writable share needs a directory that is also writable for the Linux user or technician is mapped to.

Some device files (like those for sound cards) might also be writable for users because applications need to send data to the corresponding devices.

# The Basic Rules for User Read Access

Some files in the system should be protected from user read access. This is important for files that store passwords.

No normal user account should be able to read the content of such files. Even when the passwords in a file are encrypted, the files must be protected from any unauthorized access.

Some of the files containing passwords on a Linux system are listed next:

+   - */etc/shadow*—This file contains user passwords in an encrypted form. Even when LDAP is used for user authentication, this file contains at least the root password.

+   - */etc/samba/smbpasswd*—This file contains the passwords for Samba users.
+     By default, the file permissions are set to 600.

+   - *Files with Apache passwords*—The location of these files depend on your configuration. They contain passwords for the authorized access to the Web server.

+   - */etc/openldap/slapd.conf*—This file contains the root password for the openLDAP server.

![](bbox=[0.107, 0.546, 0.295, 0.619])

After installing the openldap2 package, the permissions for this file are set to 644.

+   - */boot/grub/menu.lst*—This file can contain the password for the GRUB boot loader.
+     By default, the file permissions are set to 600.

![](bbox=[0.107, 0.699, 0.295, 0.773])

This list is not complete. More password files may be on your system, depending on your system configuration and your software selection.

Some password files can be readable for a nonroot account. This is normally the account under whose user ID a service daemon is running.

For example, the Apache Web server runs under the user ID of the user wwwrun. For this reason, the password files must be readable for the user wwwrun.

In this case, you have to make sure that only this daemon account and no other user is allowed to read the file.