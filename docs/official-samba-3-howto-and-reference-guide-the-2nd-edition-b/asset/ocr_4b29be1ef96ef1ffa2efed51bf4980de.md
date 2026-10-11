auth sufficient /lib/security/pam_winbind.so
lines as before, but also added the
required pam_security.so
above it to disallow root logins over the network. I also added a sufficient /lib/security/pam_unix.so use_first_pass line after the winbind.so line to get rid of annoying double prompts for passwords.

# Solaris-Specific Configuration

The /etc/pam.conf needs to be changed. I changed this file so my Domain users can log on both locally as well with telnet. The following are the changes that I made. You can customize the pam.conf file as per your requirements, but be sure of those changes because in the worst case it will leave your system nearly impossible to boot.

```
#ident "#(#)pam conf 1.14 09/09/16 SMI"
#
# Copyright (c) 1996-1999, Sun Microsystems, Inc.
# All Rights Reserved.

# PAM configuration

# Authentication management

# login auth required /usr/lib/security/pam_winbind.so
login auth required /usr/lib/security/$ISA/pam_unix.so.1 try_first_pass
login auth required /usr/lib/security/$ISA/pam_dial_auth.so.1 try_first_pass
#
#rlogin auth sufficient /usr/lib/security/pam_winbind.so
rlogin auth sufficient /usr/lib/security/$ISA/pam_rhosts_auth.so.1
rlogin auth required /usr/lib/security/$ISA/pam_unix.so.1 try_first_pass
#
dtelogin auth sufficient /usr/lib/security/pam_winbind.so
dtelogin auth required /usr/lib/security/$ISA/pam_unix.so.1 try_first_pass
#
rsh auth required /usr/lib/security/$ISA/pam_rhosts_auth.so.1
other auth sufficient /usr/lib/security/pam_winbind.so
other auth required /usr/lib/security/$ISA/pam_unix.so.1 try_first_pass
#
# Account management

#
login account sufficient /usr/lib/security/pam_winbind.so
login account requisite /usr/lib/security/$ISA/pam_roles.so.1
login account required /usr/lib/security/$ISA/pam_unix.so.1
#
```