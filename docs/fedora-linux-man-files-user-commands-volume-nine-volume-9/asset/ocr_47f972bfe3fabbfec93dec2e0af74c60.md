preserve the directory structure of the files being copied instead of flattening the directory structure. For example, rdist ing a list of files such as /path/dir1/f1 and /path/dir2/f2 to /tmp/dir would create files /tmp/dir/path/dir1/f1 and /tmp/dir/path/dir2/f2 instead of /tmp/dir/dir1/f1 and /tmp/dir/dir2/f2.

**noexec**  
Automatically exclude executable files that are in (5) format from being checked or updated.

**younger**  
Younger mode. Files are normally updated if their *mti* and *size* (see (2)) disagree. This option causes *rdist* not to update files that are younger than the master copy. This can be used to prevent newer copies on other hosts from being replaced. A warning s sage is printed for files which are newer than the master copy.

**compare**  
Binary comparison. Perform a binary comparison and update files if they differ rather than comparing dates and sizes.

**follow**  
Follow syolic links. Copy the file that the link points to rather than the link itself.

**ignlnks**  
Ignore unresolved links. *Rdist* will normally try to maintain the link structure of files being transferred and warn the user if all the links cannot be found.

**chk nfs**  
Do not check or update files on target host that reside on NFS filesystems.

**chk readonly**  
Enable check on target host to see if a file resides on a read-only filesystem. If a file does, then no checking or updating of the file is attempted.

**chksym**  
If the target on the remote host is a syolic link, but is not on the master host, the remote target will be left a syolic link. This behavior is generally considered a bug in the original version of *rdist*, but is present to allow compatibility with older versions.

**quiet**  
Quiet mode. Files that are being modified are normally printed on standard output. This option suppresses this.

**remove**  
Remove extraneous files. If a directory is being updated, any files that exist on the remote host that do not exist in the master directory are removed. This is useful for maintaining truly identical copies of directories.

**nochk owner**  
Do not check user ownership of files that already exist. The file ownership is only set when the file is updated.

**nochk group**  
Do not check group ownership of files that already exist. The file ownership is only set when the file is updated.

**nochk mode**  
Do not check file and directory permission modes. The permission mode is only set