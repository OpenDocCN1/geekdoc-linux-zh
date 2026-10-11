medfield. The automountd daemon will automatically unmount the file system after it has been inactive for five minutes.

The "/net" and "/home" maps are included in several other default automount maps. Use the "/net" mountpoint to access other hosts. If you know there are NFS servers with specific names, you can view all the file systems that are exported by each one. Use `ls` to display `/net medfield`, `net medford`, and so on. Once the file systems are mounted, browse through them.

> NOTE You can use the AdminSuite to view and modify your shares and mounted file systems as well as to set up automounts.

Solaris has produced a very powerful automount facility. It is more powerful than that contained in other commercial versions of Unix. If you want to use a remote file system on your local machine, it needs to be mounted. The following example command will mount the file system by hand:

```
% mkdir /perhome /docs
% mount barric:/export/home /perhome
% mount -o ro, nosuid barric:/export/docs
% mount -o ro barric:/export/docs/access /docs/access
```

If you use `mkdir` to make directories on which to mount the file systems, then you use `mount` to mount the file systems. The file systems will be read-only by default if the NFS server is exporting with read-write permissions. In the first line, the `/export/home` directory is mounted from the machine named `barrie` on the local directory `/perhome`. The second and third lines use the `-o ro` option to force a read-only mount. The second mount line also uses the `-ro` option to force a read-only mount, and in addition, it adds the `-o nosuid` option by using the multiple-option form of the `-o` option.

The `nosuid` option forces mounted `setuid` executables to run with regular Solaris permissions. Use the entries in `/etc/vfstab` to mount the `/var/mail` directory from the server whenever the machine is booted. This entry will mount the `/var/mail` directory from the server named `mailhost` whenever the machine is booted:

```
mailhost:/var/mail 	 - 	 /var/mail 	 nfs 	 - 	 yes \
	 intr,hard,bg,noac
```

Here there is no raw device to check. The file system type is NFS and the command `fsck` is not run at boot. This example is designed for mounting a mail spool directory from a mail server. Table 9.6 describes the various NFS options and what they do.