Linux, following Unix, is a multiuser system. Unlike most operating systems for personal computers, 1 in which there is only one user and whoever is physically in front of the computer has complete control, Linux and Unix separate files and processes by the owners and groups to which they belong. In this chapter, we examine permission checking and look at the APIs for retrieving and setting the owner and group identifiers.

# 11.1 Checking Permissions

As we saw in Section 5.4.2, “Retrieving File Information,” page 141, the filesystem stores a file’s user identifier and group identifier as numeric values; these are the types uid_t and gid_t, respectively. For brevity, we use the abbreviations UID and GID for “user identifier” and “group identifier.”

Every process has several user and group identifiers associated with it. As a simplification, one particular UID and GID are used for permission checking: when the UID of a process matches the UID of a file, the file’s user permission bits dictate what the process can do with the file. If they don’t match, the system checks the GID of the process against the GID of the file; if they match, the group permissions apply; otherwise the “other” permissions apply.

Besides files, the UID controls how one process can affect another by sending it a signal. Signals are described in Chapter 10, “Signals,” page 347.

Finally, the superuser, root, is a special case. root is identified by a UID of 0. When a process has UID 0, the kernel lets it do whatever it wants to: read, write, or remove files, send signals to arbitrary processes, and so on. (POSIX is more obscure about this, referring to processes with “appropriate privilege.”) This language in turn has filtered down into the GNU/Linux manpages and the GLIBC online Info manual. Some operating systems do separate privilege by user, and Linux is moving in this direction as well. Nevertheless, in current practice, “appropriate privilege” just means processes with UID 0.

+   1. MacOS X and Windows XP are both multiuser systems, but this is a rather recent development.