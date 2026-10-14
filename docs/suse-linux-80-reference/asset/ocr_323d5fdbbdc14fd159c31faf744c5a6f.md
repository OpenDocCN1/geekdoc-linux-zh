There is now a new pam_pwcheck module which takes over the verification of new passwords. The old entry:

```
password required    /lib/security/pam_unix.so    #strict=false
```

must be changed (written in one line, or with \\ at the end of the line):

```
password required    /lib/security/pam_pwcheck.so \
                     nullok #use_cracklib
password required    /lib/security/pam_unix.so    \
                     nullok use_first_pass use_authtok
```

This manual intrusion is only necessary if rpm is not able to change the configuration files itself because the system administrator has made changes. This is the case for all PAM configuration files located in /etc/pam.d.

+   - `ldconfig` is only run if there is a `/lib` directory newer than `/etc/ld.so.cache`. This may be run in the background. Force ldconfig to run by setting the environment variable `run_ldconfig` to true. You can also set this at the boot prompt with `"run_ldconfig=true"`.
+   
+   - The package `apache` package has been divided. If you need special enhancements, also install the `mod_*` subpackages. Documentation on PHP can be found in the package `phpdoc`. For a good overview, take a glance at `/var/log/httpd`.
+   
+   - `package openssh`: For heightened security, “X11 forwarding” is disabled in the default setting. The parameter `-X` allows the activation of this feature. Forwarding can be globally or locally (only for certain machines) activated by entering the line `ForwardX11 yes` in `/etc/ssh/ssh_config`. Users can also specify this option in `~/.ssh/config`.
+   
+   - `ypserv` from the package `ypserv` is no longer linked to the “tcp-wrapper” library, but instead uses `/var/rpc/securenets`. After an update, the settings from `/etc/hosts.allow` or from `/etc/hosts.deny` should be transferred to `/var/yp/securenets`.
+   
+   - The portmapper is started via `/etc/init.d/portmap` (since SuSE Linux 7.1) or with the command `rcportmap`. `/sbin/init.d/rpc` is now obsolete.
+   
+   - On the package cron: in accordance with the FHS, the cron tables are located in `/var/spool/cron/tabs`. See section Package cron on page 273.