the UNIX filesystem, associated with the file or directory. For this to operate correctly, the parameters map hidden, map system, map archive must be set to off. This parameter writes the DOS attributes as a string into the extended attribute named “user.DOSATTRIB”. This extended attribute is explicitly hidden from smbD clients requesting an EA list. On Linux the filesystem must have been mounted with the mount option user.xattr in order for extended attributes to work, also extended attributes must be compiled into the Linux kernel

# strict allocate (S) Default: strict allocate = no

This is a boolean that controls the handling of disk space allocation in the server. When this is set to yes the server will change from UNIX behaviour of not committing real disk storage blocks when a file is extended to the Windows behaviour of actually forcing the disk system to allocate real storage blocks when a file is created or extended to be a given size. In UNIX terminology this means that Samba will stop creating sparse files. This can be slow on some systems.

When strict allocate is no the server does sparse disk block allocation when a file is extended.

Setting this to yes can help Samba return out of quota messages on systems that are restricting the disk quota of users.

# strict locking (S) Default: strict locking = yes

This is a boolean that controls the handling of file locking in the server. When this is set to yes, the server will check every read and write access for file locks, and deny access if locks exist. This can be slow on some systems.

When strict locking is disabled, the server performs file lock checks only when the client explicitly asks for them.

Well-behaved clients always ask for lock checks when it is important. So in the vast majority of cases, strict locking = no is acceptable.

# strict sync (S) Default: strict sync = no

Many Windows applications (including the Windows 98 explorer shell) seem to confuse flushing buffer contents to disk with doing a sync to disk. Under UNIX, a sync call forces the process to be suspended until the kernel has ensured that all outstanding data in kernel disk buffers has been safely stored onto stable storage. This is very slow and should only be done rarely. Setting this parameter to no (the default) means that smb(8) ignores the Windows applications requests for a sync call. This is only a possibility of losing data if the operating system itself that Samba is running on crashes, so there is little danger in this default setting. In addition, this fixes many performance problems that people have reported with the new Windows98 explorer shell file copies.