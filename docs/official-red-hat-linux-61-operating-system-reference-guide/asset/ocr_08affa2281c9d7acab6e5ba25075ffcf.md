Writers’ Manual, an Application Developers’ Manual, and the PAM standard, DCE-RFC 86.0.

# # 2.7 Shadow Utilities

Shadow passwords are a method of improving system security by moving the en-crypted passwords (normally found in /etc/passwd) to /etc/shadow which is readable only by root. During the installation of Red Hat Linux, you were given the option of setting up shadow password protection on your system.

The shadow-utils package contains a number of utilities that support:

+   - Conversion from normal to shadowed passwords and back (pwconv, pwn-conv)
+   - Verification of the password, group, and associated shadow files (pwck, grpck)
+   - Industry-standard methods of adding, deleting and modifying user accounts (useradd, usermod, and userdel)
+   - Industry-standard methods of adding, deleting, and modifying user groups (groupadd, groupmod, and groupdel)
+   - Industry-standard method of administering the /etc/group file (gpasswd)