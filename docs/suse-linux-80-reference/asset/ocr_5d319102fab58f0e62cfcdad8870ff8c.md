+   - All kernel modules (“drivers”) are components of the kernel you have installed (single, multiprocessor, etc.). This ensures that the properly compiled module are installed. package `kernelmod` and package `kern`-mods are no longer required. The configuration files of the installed kernel are stored in `/boot` as `vmlinuz.config-pentium`, e.g., `vmlinuz.autoconf.h` and `vmlinuz.version.h`.

+   - The configuration file for the kernel modules has a similar file name pattern as other configuration files: `/etc/modules.conf` (formerly `/etc/conf.modules`).

+   - The nscd (name service cache daemon) is also included in the glibc. It is configured in the `/etc/nscd.conf` file. See the man page for nscd (man 8 nscd) for more information.

+   - The current glibc has ushered in the final migration to “Unix98 PTY” devices, which requires the mounting of the `devpts` file system. This is defined by the following line in `/etc/fstab`:

```
none    /dev/pts    devpts    gid=5,mode=620    0 0
```

Refer to the documentation in `/usr/src/linux/Documentation/` Changes under the kernel sources (package `kernel-source`, series d).

+   - PAM (Pluggable Authentication Modules): In addition to `/etc/login.defs`, there are now `/etc/security`, `/etc/security/limits.conf`, and `/etc/security/pam_env.conf`. See on page 25.

+   - Valid login shells are specified in `/etc/shells`. See the man page for `shells` (man 5 shells). If a user is designated `/bin/true`, this user can only log in over the X Window System—this user does not have a shell. If `/bin/false` defines the “login shell” for a given user, that user cannot log in at all.

+   - The X Window System 4.0 no longer supports some older graphics cards. It also does not support some newer cards yet. See Section *Version 4.x of XFree86* on page 128. The setup application will recognize this situation, in which case, it will automatically fall back to the previous package version 3.3.x.

+   - To heighten security, the XDM is now preconfigured to *not* accept XDMCP or Chooser requests. To access from X terminals, for example, comment out the option line `DisplayManager.requestPort` in `/etc/X11/xdm/xdm-config` (formerly `/var/X11R6/lib/xdm/xdm-config`) with an exclamation mark. See the man page for xdm (man xdm).