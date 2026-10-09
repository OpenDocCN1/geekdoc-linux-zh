# ## Auditing Configuration

All configuration files for the auditing subsystem are located in the `/etc/security/audit` directory.

```
```
# ls -l /etc/security/audit
total 56
-rw-r----- 1 root audit     37 Sep 30 1997 bincmds
-rw-rw---- 1 root audit   2116 Nov 06 16:37 config
-rw-rw---- 1 root audit  12236 Nov 06 22:00 events
-rw-rw---- 1 root audit    340 Sep 30 1997 objects
-rw-r----- 1 root audit     54 Sep 30 1997 streamcmds
```
```

The `/etc/security/audit/config` file is arranged into stanzas, each defining an aspect of the auditing subsystem’s behavior. The start stanza sets the mode that auditing will run in when started—BIN, STREAM, or both:

```
```
start:
  binmode = on
  streammode = off
```
```

The next two stanzas define locations and other behaviors of each of the two modes. For the BIN mode, the names and locations of the two bins and the output file may be defined. The STREAM stanza contains only the location of the file containing the audit stream processing command.

```
```
bin:
  trail = /audit/trail
  bin1 = /audit/bin1
  bin2 = /audit/bin2
  binnsize = 10240
  cmds = /etc/security/audit/bincmds

stream:
  cmds = /etc/security/audit/streamcmds
```
```

The various classes are detailed in the next stanza. By default, ten classes are defined in the following format; you are free to modify these existing classes or add your own.

```
```
classes:
  general = USER_SU, PASSWORD_Change, FILE_Unlink, FILE_Link, FILE_Rename, FS_Chdir, FS_Chroot, PORT_Locked, PORT_Change, FS_Mkdir, FS_Rmdir
```
```

The final stanza, `users`, contains the names of users that are to be audited, with the specific classes to audit for those users.

```
```
users:
  root = general
```
```