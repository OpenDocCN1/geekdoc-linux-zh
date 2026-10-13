# SELF TEST ANSWERS

# User Account Management

+   1. The minimum user ID number for regular users on Red Hat distributions is 500. It's 100 on many other Linux distributions.
+   2. The command in a GUI-based text console that starts the Red Hat User Manager is system-config-users.

# Administrative Control

+   3. The file that regulates the local consoles where the root user can log in is /etc/securetty.
+   4. The file that supports the configuration of custom administrators is /etc/sudoers.
+   5. When a regular user uses the sudo command to run an administrative command, the regular password of that user is required.

# User and Shell Configuration

+   6. To automatically add files to every new user account, you should use the /etc/skel directory.
+   7. The system-wide configuration file associated with the bash shell is /etc/bashrc.

# Users and Network Authentication

+   8. If the LDAP domain is example.org, what is the LDAP Search Base DN is dc=example,dc=org.
+   9. The full path to the file that points to an LDAP database for authentication is /etc/nsswitch.conf.

# Special Groups

+   10. The command that would set the SGID bit on the /home/developer directory is chmod g+s /home/developer. Numeric options such as chmod 2770 /home/developer are not correct, as they go beyond just setting the SGID bit.
+   11. The command would set up ownership of the developer group on the /home/developer directory is chgrp developer /home/developer.
+   12. The command that adds user alpha to the developer group is usermod -G developer alpha.