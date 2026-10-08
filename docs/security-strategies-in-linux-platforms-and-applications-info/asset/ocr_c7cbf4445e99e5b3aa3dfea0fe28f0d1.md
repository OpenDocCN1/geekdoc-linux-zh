# 134 PART 2 | Layered Security and Linux

```
nfsnbody:x:4294967294:4294967294:
→ Anonymous NFS User:/var/lib/nfs:/bin/sh
```

Additional problems relate to different user-authentication databases. For example, the first user on an Ubuntu system has a UID of 1000, the first user on a Red Hat system has a UID of 500. Even if those users have identical names and passwords, the user on one client won't be able to access his or files on a shared directory from a second client.

# NFS Permissions and Authentication

All versions of NFS share shares with read-only or read-write access. Whatever access is allowed in the NFS /etc/exports configuration file supersedes any access of actual files. In fact, when you run the ls -l command on an NFS-mounted directory, the permissions don't have to match the permissions configured in the /etc/exports file.

NFS version 4 (NFSv4) systems, when properly configured, are somewhat secure. They can be used with a Kerberos ticket server to authenticate users.

NFSv4 allows ACLs. With regular ACLs on Linux, NFS-based ACLs override standard read, write, and executable permissions for shared directories.

# Samba/CIFS Network Permissions

Samba is the Linux implementation of Microsoft networking. As Microsoft has added to its systems with the Common Internet File System (CIFS), Samba has kept pace. As a result, current Linux systems can share directories and printers on a Microsoft-based network. It's even possible to have a Samba-based network of nothing but Linux computers. The focus of this section is the main Samba configuration file, smb.conf in the /etc/samba/ directory. That configuration file is split into two sections, "Global Settings" and "Share Definitions." This chapter is focused on the shared files; the first section is discussed in Chapter 8.

As NFS, the configured options in the Samba configuration supersede any any local permissions for the shared files and directories.

The standard share in Samba is of home directory owners. It's associated with the [homes] stanza. In general, default options allow an authenticated user to access his or her home directory on the local system. However, directory is not shared—and should not even be visible to other users, courtesy of the following:

```
browseable = no
```

Some directives are functionally identical. For example, you may see one of the following defaults in the [homes] stanza:

```
read only = yes
writeable = no
```

> NOTE Some Samba directives appear to be misspelled. Sometimes, multiple spellings are allowed; for example, browseable and browseable have the same meaning in a Samba configuration file.