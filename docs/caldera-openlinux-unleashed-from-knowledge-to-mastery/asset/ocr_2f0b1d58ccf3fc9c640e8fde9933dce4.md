Each host specification can be followed by one or more options. Options are enclosed in parentheses and separated with commas. Do not put spaces in the option lists. Available options are:

+   * secure   Requires that mount requests originate from a “reserved” Internet port. UNIX machines limit access to ports below 1024 to root; this option adds a small measure of security by ensuring that requests from UNIX machines come from root-privileged sources. This option is on by default.
+   * ro   Allows read-only access to the volume.
+   * noaccess   Disallows access to the volume. This seemingly useless option allows you to export a volume but disable access to certain subdirectories within the volume.

# Background Material

> The noaccess level only works on Linux. Most UNIX NFS servers do not allow the noaccess level of control.

+   * root_squash   Converts access from root on a client to nobody on the server. It actually reduces root’s privileges. This option is on by default. It was intended to provide some extra security—anyone who gains root privileges on a client will still be unable to modify sensitive files on the NFS server. In practice, the option doesn’t provide that much extra security.
+   * no_root_squash   Turns off root_squash.

For more options, see exports(5). Most of the remaining options relate to user- and group-ID mapping.

# Sample /etc/exports File

Here is a sample exports file:

```
/   shishi(ro) trusted(rw,no_root_squash)
   \*,roarngpenguin.com(ro)
/usr/local   (ro,insecure)
/pub   (ro,insecure)
/pub/private   (noaccess)
```

Let’s look at it line-by-line:

+   * shishi is allowed to mount the root directory read-only. trusted can mount it read/write and, in addition, root on trusted retains root privileges on the server.
+   * Any machine in roarngpenguin.com can mount /usr/local read-only.