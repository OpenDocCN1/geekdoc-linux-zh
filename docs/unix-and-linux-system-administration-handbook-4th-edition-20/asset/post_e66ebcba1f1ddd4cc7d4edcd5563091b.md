
## ACL implementation

See Chapter 18 for more information about NFS.

The architects of version 4 of the NFS protocol—the standard file-sharing protocol used by UNIX—wanted to incorporate ACLs as a first-class entity. Because of the UNIX/Windows split and the inconsistencies among UNIX ACL implementations, it was clear that the systems on an NFSv4 connection might often be of different types. Each system must understand NFSv4 ACLs, POSIX ACLs, Windows ACLs, or no ACLs at all. The NFSv4 standard would have to be interoperable with these various worlds without causing too many surprises or security problems.

Given this constraint, it's perhaps not surprising that NFSv4 ACLs are essentially a union of all preexisting systems. A strict superset of POSIX ACLs, so no POSIX ACL can be represented as an NFSv4 ACL without loss of information. At the same time, NFSv4 ACLs accommodate all the permission bits found on Windows, and they have most of Windows' semantic features as.

## ACL implementation

In theory, responsibility for maintaining and enforcing ACLs could be turned over several different components of the operating system. ACLs could be implemented by the kernel on behalf of all the system's files, by individual filesystems, or by higher-level software such as NFS and CIFS servers.

In practice, only filesystems can implement ACLs reliably, and with acceptable performance. Hence, ACL support is both OS dependent and filesystem dependent. A filesystem that supports ACLs on one system may not support them on another, or it may feature a somewhat different implementation managed by different commands.

The standard UNIX system calls that manipulate files (open, read, unlink, and on) make no provision for ACLs. However, they continue to work on systems with ACLs because the underlying systems do their own permission checking. Operations that are not allowed by the relevant ACL simply fail and return a generic "permission denied" error code.

ACL-aware programs use a separate system call or library runtime to read or set files' ACLs. When an operating system first adds support for ACLs, it usually updates utilities such as ls and cp to be at least ACL-aware (for example, by making cp -p preserve ACLs if they are present). In addition, the system must add new commands or command extensions to let users read and set ACLs from the command line. Unfortunately, these commands are not standard among operating systems, either.

Because ACL implementations are filesystem specific and because systems support multiple filesystem implementations, many systems end up supporting multiple types of ACLs. Even a given filesystem may offer several ACL options, as in IBM's JFS2. The commands to manipulate them might be the same or different; it depends on the system.

![](img/579efec8c67772f31ecf34844bbb71a2_209_0.png)

## ACL support by system

In general, ACL support under UNIX and Linux is currently something of ad hoc mess. Here are some particulars:

- As of writing (2010), POSIX-based ACL systems have the lead in implementation and deployment, by NFSv4 ACLs are rapidly gaining ground and will likely become the facto standard. Currently, Sun's ZFS and IBM's JFS2 have native support for NFSv44 ACLs.

- Under Linux, POSIX-style ACLs are supported by ReiserFS, XFS, JFS, Btrfs, and the ext family of filesystems. They are usually disabled by default; use the -acl option to mount them. The getfac and setfac commands manipulate POSIX ACL entries.

![](img/579efec8c67772f31ecf34844bbb71a2_210_0.png)

- Solaris supports POSIX ACLs on the older UFS filesystems and NFSv4 ACLs on ZFS. The Solaris versions of ls have been modified to display and edit all types of ACLs. Solaris has getfac and setfac commands that are vaguely similar to those found on Linux distributions, but they're really just for compatibility and work for POSIX ACLs.

![](img/579efec8c67772f31ecf34844bbb71a2_210_1.png)

- HP-UX designed its own ACL system for its High-performance Filesystem (HFS). When HP adopted Veritas's VxFS as its primary filesystem, it also incorporated support for POSIX-style ACLs. Unfortunately, the two ACL systems are controlled by different sets of commands. HFS is now deprecated, the HFS commands remain for compatibility. We do not discuss the HFS ACLs in this book.

![](img/579efec8c67772f31ecf34844bbb71a2_210_2.png)

- AIX's JFS2 filesystem supports a primary ACL system known as AIX. As of ACL 5.0, JFS2 supports NFSv4-style ACLs. AIX uses the same commands (acget, acput, and acledit) to manipulate both types of ACLs, and it provides an aclconvert to facilitate migration from one format to another. We do not discuss AIX in this book.

![](img/579efec8c67772f31ecf34844bbb71a2_210_3.png)

## POSIX ACLs

POSIX ACLs are supported on many Linux filesystems and on HP-UX's VxFS filesystem (known as JFS). They are also available under Solaris for the deprecated UFS filesystem.

- 1. Make sure that your PATH environment variables /bin /usr/gnu/bin so that you get the Solaris-specific versions of ls and chosen instead of the GNU versions.

- 2. In effort to keep users disoriented and docile

## Interaction between traditional modes and ACLs

POSIX ACLs are a mostly straightforward extension of the standard 9-bit UNIX permission model. Read, write, execute permission are the only capabilities that the ACL system deals with. Embellishments like the setuid and sticky bits are handled exclusively through the traditional modes.

ACLs allow the rwx bits to be set independently for any combination of users and groups. Table 6.8 shows what the individual entries in an ACL can look like.

## Table 6.8 Entries that can appear in an access control list

| Format | Example | Sets permissions for |
| --- | --- | --- |
| user::perms | user:rw-- | The file owner |
| user:username:perms | user:trent:rw- | A specific user |
| group::perms | group:rx | The group that owns the file |
| group:name:perms | group:staff | A specific group |
| other::perms | other:: | All others |
| mask::perms | mask:rwx | The mask |

## Interaction between traditional modes and ACLs

POSIX ACLs are a mostly straightforward extension of the standard 9-bit UNIX permission model. Read, write, execute permission are the only capabilities that the ACL system deals with. Embellishments like the setuid and sticky bits are handled exclusively through the traditional modes.

ACLs allow the rwx bits to be set independently for any combination of users and groups. Table 6.8 shows what the individual entries in an ACL can look like.

## Table 6.8 Entries that can appear in an access control list

| Format | Example | Sets permissions for |
| --- | --- | --- |
| user::perms | user:rw-- | The file owner |
| user:username:perms | user:trent:rw- | A specific user |
| group::perms | group:rx | The group that owns the file |
| group:name:perms | group:staff | A specific group |
| other::perms | other:: | All others |
| mask::perms | mask:rwx | The mask |

In words, the mask specifies an upper bound on the access that the ACL can assign to individual groups and users. It is conceptually similar to the umask, except that the ACL is always in effect and specifies the allowed permissions rather than the permissions to be denied.

As a result, the traditional mode bits can never understand the access allowed by the ACL as a whole. Furthermore, clearing a bit from the group portion of the traditional mode clears the corresponding bit in the ACL mask and thereby forbids this permission to everyone but the file's owner and those who fall in the category of "other".
