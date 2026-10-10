calculator system, and you can write a module to support it (documentation on writing modules is included with the system). PAM-aware programs can use the new module and work with the new one-time-password calculators without being recompiled or otherwise modified in any way.

# ### 10.4.2 Services

Each program which uses PAM defines its own “service” name. The login program defines the service type `login`, ftpd defines the service type `ftp`, etc. In general, the service type is the name of the program used to **provide** the service, not (if there is a difference) the program used to **access** the service.

# ### 10.4.3 The Configuration Files

The directory `/etc/pam.d` is used to configure all PAM applications. (This used to be `/etc/pam.conf` in earlier PAM versions; while the pam.conf file is still read if no /etc/pam.d/ entry is found, its use is deprecated.) Each application (really, each **service**) has its own file. A file looks like this:

```
#%PAM-1.0

auth required /lib/security/pam_securtty.so
auth required /lib/security/pam_pwd.b.so shadow nullok
auth required /lib/security/pam_nologin.so
account required /lib/security/pam_pwd.b.so
password required /lib/security/pam_cracklib.so
password required /lib/security/pam_pwb.b.so shadow nullok use_authok
session required /lib/security/pam_pwd.b.so
```

The first line is a comment. Any line that starts with a `#` character is a comment. The next three lines stack up three modules to use for login authorization. The first line makes sure that if the user is trying to log in as root, the tty on which they are logging in is listed in the `/etc/securtty` file *if* that file exists. The second line causes the user to be asked for a password and the password checked. The third line checks to see if the file `/etc/nologin` exists, and if it does, displays the contents of the file, and if the user is not root, does not let him or her log in.