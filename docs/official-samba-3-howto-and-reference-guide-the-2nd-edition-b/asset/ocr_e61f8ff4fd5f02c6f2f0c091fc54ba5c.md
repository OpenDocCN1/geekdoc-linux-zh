+   - 2 - user default quotas (uid = -1)
+   - 3 - group quotas
+   - 4 - group default quotas (gid = -1)
+   *   2 - id (uid for user, gid for group, -1 if N/A)
+   *   3 - quota state (0 = disable, 1 = enable, 2 = enable and enforce)
+   *   4 - block softlimit
+   *   5 - block hardlimit
+   *   6 - inode softlimit
+   *   7 - inode hardlimit
+   *   8 (optional) - block size, defaults to 1024

The script should output at least one line of data on success. And nothing on failure.

# share modes (S)  Default: *share modes = yes*

This enables or disables the honoring of the *share modes* during a file open. These modes are used by clients to gain exclusive read or write access to a file.

These open modes are not directly supported by UNIX, so they are simulated using shared memory, or lock files if your UNIX doesn't support shared memory (almost all do).

The share modes that are enabled by this option are DENY_DOS, DENY_ALL, DENY_READ, DENY_WRITE, DENY_NONE and DENY_FC6.

This option gives full share compatibility and enabled by default.

You should *NEVER* turn this parameter off as many Windows applications will break if you do so.

# short preserve case (S)  Default: *short preserve case = yes*

This boolean parameter controls if new files which conform to 8.3 syntax, that is all in upper case and of suitable length, are created upper case, or if they are forced to be the *default case* . This option can be use with *preserve case = yes* to permit long filenames to retain their case, while short names are lowered.

See the section on the section called §220:NAME MANGLING§221: .

# show add printer wizard (G)  Default: *show add printer wizard = yes*

With the introduction of MS-RPC based printing support for Windows NT/2000 client in Samba 2.2, a "Printers..." folder will appear on Samba hosts in the share listing. Normally this folder will contain an icon for the MS Add Printer Wizard (APW).