# INTERACTIVE COMMANDS

Once in interactive mode, **sftp** understands a set of commands similar to those of (1). Commands are case insensitive. Pathnas that contain spaces st be enclosed in quotes. Any special characters contained within pathnas that are recognized by (3) st be escaped with backslashes ( ' ' )

+   bye
+       Quit **sftp**

+   cd *path*
+       Change remote directory to *path*

+   chgrp *grp path*
+       Change group of file *path* to *grp* *path* may contain (3) characters and may match multiple files. *grp* st be a nuric GID.

+   chmod *mode path*
+       Change permissions of file *path* to *mode* *path* may contain (3) characters and may match multiple files.

+   chown *own path*
+       Change owner of file *path* to *own* *path* may contain (3) characters and may match multiple files. *own* st be a nuric UID.

+   df [ -hi ] [ *path* ]
+       Display usage information for the filesystem holding the current directory (*or path* if specified). If the *-h* flag is specified, the capacity information will be displayed using “human-readable” suffixes. The *-i* flag requests display of inode information in addition to capacity information. This command is only supported on servers that implement the “” extension.

+   exit
+       Quit **sftp**

+   get [ -afPpr ] *remote-path* [ *local-path* ]
+       Retrieve the *remote-path* and store it on the local machine. If the local *path* na is not specified, it is given the *sa na* it has on the remote machine. *remote-path* may contain (3) characters and may match multiple files. If it does and *local-path* is specified, then *local-path* st specify a directory.
+   
+   If the *-a* flag is specified, then atemptt to resu partial transfers of existing files. Note that resumption assus that any partial copy of the local file matches the remote copy. If the remote file contents differ from the partial local copy then the resultant file is likely to be corrupt.
+   
+   If the *-f* flag is specified, then (2) will be called after the file transfer has completed to flush the file to disk.
+   
+   If either the *-P* or *-p* flag is specified, then full file permissions and access tis are copied too.
+   
+   If the *-r* flag is specified then directories will be copied recursively. Note that **sftp**