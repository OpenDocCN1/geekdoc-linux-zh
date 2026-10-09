# **USER ID MAPPING OPTIONS**

Each user has a UID number and a primary GID number on the local system. The local `etc/passwd` and `etc/group` files may map these numbers to names. When a user makes a request of an NFS server, the server uses these numbers to identify the user on the remote system, raising several issues:

+   - The user may not have the same ID numbers on both systems. As a consequence, the user may have owner access to files of another user and not have owner access to his own files (see “NIS and NFS” for a solution).
+   - You may not want a user with **root** privileges on the client system to have owner access to **root**-owned files on the server.
+   - You may not want a remote user to have owner access to some important system files that are not owned by **root** (such as those owned by `bin`).

# **Critical files in NFS-mounted directories should be owned by root**

Despite the mapping done by the **root-squash** option, a user with **root** privileges on a client system can use `sudo` or `su` to assume the identity of any user on the system and then access that user’s files on the server. Thus, without resorting to **all-squash**, you can protect only files owned by **root** on an NFS server. Make sure that **root**—and not `bin` or another user—owns and is the only user who can modify or delete critical files within any NFS-mounted directory hierarchy.

Taking this precaution does not completely protect the system against an attacker with **root** privileges, but it can help thwart an attack from a less experienced malicious user.

*Owner access* to a file means that the remote user can execute or—worse—modify the file. NFS gives you two ways to deal with these cases:

+   - You can use the **root_squash** option to map the ID number of the **root** account on a client to UID 65534 on the server.
+   - You can use the **all-squash** option to map all NFS users on the client to UID 65534 on the server.

Use the `anounid` and `anongid` options to override these values.

When you use NIS (page 741) for user authorization, users automatically have the same UIDs on both systems. If you are using NFS on a large network, it is a good idea to use a directory service such as NIS or LDAP (page 758) for authorization. Without such a service, you must synchronize the `passwd` files on all the systems manually.

# root_squash (no_root_squash)

Maps requests from **root** on a remote system so they appear to come from the UID 65534, a nonprivileged user on the local system, or as specified by `anounid`. This option does not affect other sensitive UIDs such as `bin`. The `no_root_squash` option turns off this mapping so that requests from **root** appear to come from **root**.