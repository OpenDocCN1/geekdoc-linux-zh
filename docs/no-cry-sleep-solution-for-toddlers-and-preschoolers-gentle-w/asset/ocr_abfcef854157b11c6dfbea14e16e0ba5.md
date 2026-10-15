# NFS User-Level Access

Along with general options, there are also options that apply to user-level access. As a security measure, the client’s root user is treated as an anonymous user by the NFS server. This is known as squashing the user. In the case of the client root user, squashing prevents the client from attempting to appear as the NFS server’s root user. Should you want a particular client’s root user to have root-level control over the NFS server, you can specify the no_root_squash option. To prevent any client user from attempting to appear as a user on the NFS server, you can classify them as anonymous users (the all_squash option). Such anonymous users would only have access to directories and files that are part of the anonymous group.

Normally, if a user on a client system has a user account on the NFS server, that user can mount and access his or her files on the NFS server. However, NFS requires the User ID for the user be the same on both systems. If this is not the case, he or she is considered two different users. To overcome this problem, you could use an NIS service, maintaining User ID information in just one place, the NIS password file (see the following section for information on NIS).

# NFS /etc/exports Example

Examples of entries in an /etc/exports file are shown here. Read-only access is given to all hosts to the file system mounted on the /pub directory, a common name used for public access. Users, however, are treated as anonymous users (all_squash). Read and write access is given to the lizard.mytrek.com computer for the file system mounted on the /home/foodstuff directory. The next entry would allow access by rabbit.mytrek.com to the NFS server’s CD-ROM, using only read access. The last entry allows anyone secure access to /home/richlp.

```
/etc/exports
/pub			*(ro,insecure,all_squash,sync)
/home/foodstuff	lizard.mytrek.com(rw,sync)
/mnt/cdrom	rabbit.mytrek.com(ro,sync)
/home/richlp	*(secure,sync)
```

# Applying Changes

Each time your system starts up the NFS server (usually when the system starts up), the /etc/exports file will be read and those directories specified will be exported. When a directory is exported, an entry for it is made in the /var/lib/nfs/xtab file. It is this file that NFS reads and used to perform the actual exports. Entries are read from /etc/exports and corresponding entries made in /var/lib/nfs/xtab. The xtab file maintains the list of actual exports.

If you want to export added entries in the /etc/exports file immediately, without rebooting, you can use the exportfs command with the -a option. It is helpful to add the -v option to display the actions that NFS is taking. Use the same options to effect any changes you make to the /etc/exports file.

```
exportfs -a -v
```

If you later make changes to the /etc/exports file, you can use the -r option to re-export its entries. The -r option will resync the /var/lib/nfs/xtab file with the /etc/exports entries, removing any other exports or any with different options.

```
exportfs -r -v
```