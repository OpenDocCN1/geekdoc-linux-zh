Table 36-1: The /etc/exports Options

| General Options | Description |
|---|---|
| no_wdelay | Performs writes immediately, not checking to see if they are related. |
| wdelay | Checks to see if writes are related, and, if so, waits to perform them together. Can degrade performance. This is the default. |
| hide | Automatically hides an exported directory that is the subdirectory of another exported directory. The subdirectory has to be explicitly mounted to be accessed. Mounting the parent directory does not allow access. This is the default. |
| no_hide | Does not hide an exported directory that is the subdirectory of another exported directory (opposite of hide). Only works for single hosts and can be unreliable. |
| subtree_check | Checks parent directories in a file system to validate an exported subdirectory. This is the default. |
| no_subtree_check | Does not check parent directories in a file system to validate an exported subdirectory. |
| insecure_locks | Does not require authentication of locking requests. Used for older NFS versions. |
| User ID Mapping | Description |
| all_squash | Maps all UIDs and GIDs to the anonymous user. Useful for NFS-exported public FTP directories, news spool directories, and so forth. |
| no_all_squash | The opposite option to all_squash. This is the default setting. |
| root_squash | Maps requests from remote root user to the anonymous UID/GID. This is the default. |
| no_root_squash | Turns off root squashing. Allows the root user to access as the remote root. |
| anonuid anon gid | Sets explicitly the UID and GID of the anonymous account used for all_squash and root_squash options. The defaults are nobody and nogroup. |

# NFS User-Level Access

Along with general options, there are also options that apply to user-level access. As a security measure, the client's root user is treated as an anonymous user by the NFS server. This is known as squashing the user. In the case of the client root user, squashing prevents the client from attempting to appear as the NFS server's root user. Should you want a particular client's root user to have root-level control over the NFS server, you can specify the no_root_squash option. To prevent any client user from attempting to appear as a user on the NFS server, you can classify them as anonymous users (the all_squash option). Such anonymous users would only have access to directories and files that are part of the anonymous group.

Normally, if a user on a client system has a user account on the NFS server, that user can mount and access his or her files on the NFS server. However, NFS requires the User ID for the user be the same on both systems. If this is not the case, he or she is considered two different users. To overcome this problem, you could use an NIS service, maintaining User ID information in just one place, the NIS password file (see the following section for information on NIS).