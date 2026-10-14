+   - RPM (see also Section *RPM — the Distribution Package Manager* on page 69) is available in Version 3.0. The format of the RPM database has changed. The database must be converted as soon as rpm is installed. In the course of a normal update of the (Base) system with YaST, this conversion will take place at the right time in the background.

+   - According to the FHS (Filesystem Hierarchy Standard) (see Section *File System Hierarchy Standard (FHS)* on page 272), the architecture-independent documentation is now found under `/usr/share/doc` (formerly `/usr/doc`).

+   - The manual pages are stored in `/usr/share/man` and the info pages in `/usr/share/info`, according to the FHS. See Section *File System Hierarchy Standard (FHS)* on page 272.

+   - `makewhatis` (package `makewhatis`) now uses the tool `manpath` to search for *manual pages*. The environment variable `MANPATH` should no longer be set in rc files.

+   - package `aaa_base`: For reasons of clarity, daily system maintenance has been divided into a number of scripts. In `/etc/cron.daily` there are now, apart from `aaa_base`, the components `backup_rpmdb`, `clean_catman`, `clean_core`, `clean_instlog`, `clean_tmp`, `do_manbd`, `rotate_logs`, and `updatedb`. In addition `aaa_base` reads `cron.daily.local`, where your own extensions can be entered. For more information on the cron system, refer to Section *Package cron* on page 273.

+   - A newer version of tar has been included. The overwrite behavior when unpacking existing files has changed. If you rely on the old mode, use the `--overwrite` option.

+   - In X, the Compose button ("multikey") can be accessed using the key combination (`Shift`) + (`Ctrl`) (right). See Section *Keyboard Layout* on page 291.

+   - For reasons of security, *anonymous* FTP is no longer allowed automatically. To allow anonymous FTP with the ftp daemon, in `ftpd` the comment sign `#` in `/etc/pam.d/ftpd` must be removed at the beginning of the line:

```
auth    sufficient    /lib/security/pam_ftp.so
```

+   - Changing password with *PAM Pluggable Authentication Modules*. `pam_unix` can also change NIS passwords and understands md5 hashes as passwords. Caution: see Section *PAM: Pluggable Authentication Modules* on page 25.