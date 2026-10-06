# $ cat /etc/pam.d/su

```
%PAM-1.0
auth sufficient /lib/security/pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth sufficient /lib/security/pam_wheel.so use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
#auth required /lib/security/pam_wheel.so use_id
auth required /lib/security/pam_stack.so service=system-auth
account required /lib/security/pam_stack.so service=system-auth
password required /lib/security/pam_stack.so service=system-auth
session required /lib/security/pam_stack.so service=system-auth
session optional /lib/security/pam_xauth.so
```

The third through sixth lines of the su module contain comments that include the lines necessary to permit members of the wheel group to run su without supplying a password (sufficient) and to permit only users who are in the wheel group to use su (required). Uncomment one of these lines when you want your system to follow one of these rules.

# Do Not Create /etc/pam.conf

You may have encountered PAM on other systems where all configuration is arranged in a single file (/etc/pam.conf). This file does not exist on Red Hat. Instead the /etc/pam.d directories contain individual configuration files, one per application that uses PAM. This makes it easy to install and uninstall applications that use PAM without having to modify the /etc/pam.conf file each time. If you create a /etc/pam.conf file on a system that does not use it, your PAM configuration may become confused. Do not use PAM documentation from a different system. Also, the requisite control flag is unavailable on some systems that support PAM.

# Administration Utilities

This section briefly describes a few of the many utilities that can help you perform system administration tasks. You will learn about other utilities from Red Hat documents (including the Red Hat Documentation CD-ROM), from the Red Hat Web site, from other Internet resources (including newsgroups), and from GNU/Linux users. Read the man/info pages for the utilities described in this section to learn more about using them. Some of these utilities are incorporated as part of the K or GN menu, and some are useful to users other than the system administrator.