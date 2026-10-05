# Chapter 18 The Network File System

# The exportfs command and the exports file (Linux, AIX)

The **exports** files consist of a list of exported directories in the leftmost column followed by lists of associated options. For example, the AIX exports line
`/home -vers=4,sec=sys,access=harp.astrust.com`

permits/**home** to be mounted by the machine harp.astrust.com using version 4 of the NFS protocol and UNIX authentication (`sec=sys`).

Filesystems that are listed in the **exports** file without a specific set of hosts are usually mountable by *all* machines. This is a sizable security hole.

The exact options and syntax used in the **exports** file vary somewhat among systems, though there is a certain thematic similarity. The following sections describe the general formats for Linux and AIX. As always, be sure to check the man page for your system.

# Exports in AIX

AIX has the most "classic" **exports** format of our example systems. The permission options are shown in Table 18.5.

Table 18.5 Common export options for AIX
| Option | Description |
| --- | --- |
| access=list | Lists the hosts that can mount the filesystem. |
| ro | Exports read-only to everyone; no clients may write on the filesystem. |
| rw | Exports for reading and writing to everyone (the default). |
| rw=list | Exports read-mostly. The list enumerates the hosts allowed to mount for writing; all others must read-only. |
| root=list | Lists hosts that can access the filesystem as root. Without this option, root access from a client is equivalent to access by the user nobody. |
| vers=n | Exports the directory to clients using version n. Valid values are 2, 3, and 4. Specifying 2 or 3 includes both and 3. |
| sec=flavor | Specifies a list of security methods for the export directory. Values include sys (UNIX authentication), dh (DES), kip5 (Kerberos authentication), kipbs5 (Kerberos authentication and integrity), kip5 (Kerberos authentication, integrity, and privacy), and none (anonymous access, not recommended). |
| anon=n | Specifies the UID to which root maps are mapped. Defaults to -2 (nobody). Setting this to -1 denies access entirely. |

In Table 18.5, a list consists of a colon-separated series of hosts and longterm names. The options in Table 18.5 are similar to those understood by the **share** command. However, there are some subtle differences. For example, the option