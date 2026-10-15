
**chown** can change both the owner and group of a file at once with the syntax

`chown user:group file ...`

For example,

`$ sudo chown -R matt:staff ~matt/restore`

Linux and Solaris take this syntax to its logical end and let you omit either **user** or **group**, thus making the **chgrp** command superfluous. If you include the colon but no **group**, **chown** uses the user’s default group.

## umask: assign default permissions

You can use the built-in shell command **umask** to influence the default permissions given to the files you create. Every process has its own **umask** attribute; the shell’s built-in **umask** command sets the shell’s own umask, which is then inherited by commands that you run.

The **umask** is specified as a three-digit octal value that represents the permissions to take away. When a file is created, its permissions are set to whatever the creating program requests minus whatever the **umask** forbids. Thus, the individual digits of the **umask** allow the permissions shown in Table 6.6.

**Table 6.6 Permission encoding for umask**

| Octal | Binary | Perms | Octal | Binary | Perms |
|---:|:---:|:---:|---:|:---:|:---:|
| 0 | 000 | rwx | 4 | 100 | -wx |
| 1 | 001 | rw- | 5 | 101 | -w- |
| 2 | 010 | r-x | 6 | 110 | --x |
| 3 | 011 | r-- | 7 | 111 | --- |

For example, **umask 027** allows all permissions for the owner but forbids write permission to the group and allows no permissions for anyone else. The default **umask** value is often 022, which denies write permission to the group and world but allows read permission.

You cannot force users to have a particular umask value because they can always reset it to whatever they want. However, you can put a suitable default in the same `.profile` file that you give to new users.

## Linux bonus flags

Linux’s ext2, ext3, and ext4 filesystems define some supplemental attributes you can turn on to request special semantics—“request” being the operative word, since many of the flags haven’t actually been implemented. For example, one flag makes a file append-only and another makes it immutable and undeletable.

Since these flags don’t apply to filesystems other than the ext* series, Linux uses special commands, lsattr and chattr, to view and change them. Table 6.7 lists the flags that currently work (about 50% of those mentioned in the man page).

### Table 6.7 Ext2 and ext3 bonus flags

| Flag | Meaning |
|------|---------|
| A | Never update access time (st_atime; for performance) |
| a | Allow writing only in append mode (only root can set) |
| D | Force directory updates to be written synchronously |
| d | No backup—make dump ignore this file |
| i | Make file immutable and undeletable (only root can set) |
| j | Keep a journal for data changes as well as metadata |
| S | Force changes to be written synchronously (no buffering) |

With the possible exception of the “no backup” flag, it’s not clear that any of these features offer much day-to-day value. The immutable and append-only flags were largely conceived as ways to make the system more resistant to tampering by hackers or hostile code. Unfortunately, they can confuse software and protect only against hackers that don’t know enough to use chattr -ia. Real-world experience has shown that these flags are more often used by hackers than against them.

The S and D options for synchronous writes also merit a special caution. Since they force all filesystem pages associated with a file or directory to be written out immediately on changes, they might seem to offer additional protection against data loss in the event of a crash. However, the order of operations for synchronous updates is unusual and has been known to confuse fsck; recovery of a damaged filesystem might therefore be made more difficult rather than more reliable. Filesystem journaling, as supported by ext3 and ext4, is usually a better option. The j option can force data journaling for specific files, albeit at some performance cost.

## 6.6 ACCESS CONTROL LISTS

The traditional 9-bit owner/group/other access control system is powerful enough to accommodate most administrative needs. Although the system has clear limitations, it’s very much in keeping with the UNIX traditions (some might say, “former traditions”) of simplicity and predictability.

Virtually all non-UNIX operating systems use a more complicated way of regulating access to files: access control lists, aka ACLs. Each file or directory can have an associated ACL that lists the permission rules to be applied to it. Each of the rules within an ACL is called an access control entry, or ACE.
