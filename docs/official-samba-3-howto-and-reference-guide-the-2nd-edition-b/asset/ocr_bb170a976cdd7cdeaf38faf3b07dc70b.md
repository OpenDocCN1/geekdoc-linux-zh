A boolean variable that controls whether all printers in the printcap will be loaded for browsing by default. See the `printers` section for more details.

**local master** (G) Default: `local master = yes`

This option allows smbd(8) to try and become a local master browser on a subnet. If set to no then **nmbd** will not attempt to become a local master browser on a subnet and will also lose in all browsing elections. By default this value is set to yes. Setting this value to yes doesn't mean that Samba will become the local master browser on a subnet, just that **nmbd** will participate in elections for local master browser. Setting this value to no will cause **nmbd** never to become a local master browser.

**lock dir** This parameter is a synonym for *lock directory*.

**lock directory** (G) Default: `lock directory = ${prefix}/var/locks/var/run/samba/locks`

Example: `lock directory = /var/run/samba/locks`

This option specifies the directory where lock files will be placed. The lock files are used to implement the `max connections` option.

**locking** (S) Default: No default

This controls whether or not locking will be performed by the server in response to lock requests from the client.

If locking = no, all lock and unlock requests will appear to succeed and all lock queries will report that the file in question is available for locking.

If locking = yes, real locking will be performed by the server.

This option *may* be useful for read-only filesystems which *may* not need locking (such as CDROM drives), although setting this parameter of no is not really recommended even in this case.

Be careful about disabling locking either globally or in a specific service, as lack of locking may result in data corruption. You should never need to set this parameter.

**lock spin count** (G) Default: `lock spin count = 3`

This parameter controls the number of times that smbd should attempt to gain a byte range lock on the behalf of a client request. Experiments have shown that Windows 2k servers do not reply with a failure if the lock could not be immediatly granted. but try a few more times in case the lock could later be acquired. This behavior is used to support PC database formats such as MS Access and FoxPro.

**lock spin time** (G) Default: `lock spin time = 10`