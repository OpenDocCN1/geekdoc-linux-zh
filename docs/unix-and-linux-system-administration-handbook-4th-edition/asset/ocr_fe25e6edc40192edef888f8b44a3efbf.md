in share syntax means to export the directory read-write with access only by the listed hosts. Under AIX, this option allows the entire world to mount the directory read-only. Gotcha! Under AIX, you must use the access clause to restrict mounting to a specified list of clients:

```
rw,access=leopard.atrust.com,ross.atrust.com
```

Read-write exporting is the default, so the rw clause could actually be eliminated. It doesn't hurt to include it explicitly, however.

Each line in an AIX exports file should consist of a directory path, whitespace, and then a dash followed by a comma-separated list of options. For instance, the following example shares the /home directory to the host leopard.atrust.com with AUTH_SYS security and version 4 of the protocol:

```
/home -vers=4,sec=sys,rw,access=leopard.atrust.com
```

Remember to run exportfs -a after changing the /etc/exports file.

# Exports in Linux

As in AIX, the Linux /etc/exports file enumerates the filesystems exported through NFS and the clients that may access each of them. Whitespace separates the filesystem from the list of clients, and each client is followed by a parenthesized list of comma-separated options. Lines can be continued with a backslash.

Here's what the format looks like:

```
/home      harp(rw,no_root_squash) monk(rw)
/usr/share/man  *.atrust.com(ro)
```

There is no way to list multiple client specifications for a single set of options, although some client specifications refer to multiple hosts. Table 18.6 lists the four types of specifications that can appear in the exports file.

# Table 18.6 Client specifications in the Linux /etc/exports file

| Type | Syntax | Meaning |
|---|---|---|
| Hostname | hostname | Individual hosts |
| Netgroup | @groupname | NIS netgroups (not frequently used) |
| Wild cards | * and ? | FQDNs* with wild cards; "**" will not match a dot |
| IP networks | ipaddr/mask | CIDR-style specifications (e.g., 128.138.92.128/25) |

a. Fully qualified domain names

Table 18.7 on the next page shows the most commonly used export options understood by Linux.

Linux's NFS server has the unusual feature of allowing subdirectories of exported directories to be exported with different options. Use the noaccess option to unexport subdirectories that you would rather not share.