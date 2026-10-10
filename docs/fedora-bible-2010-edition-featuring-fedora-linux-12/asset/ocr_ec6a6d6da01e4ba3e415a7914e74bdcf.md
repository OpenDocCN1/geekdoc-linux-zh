craft in the `handsonhistory.com` domain. The final example matches any three-letter hostnames in the domain.

> **NOTE:** You can also separate multiple hostnames with spaces, but if you add options after each hostname, leave no spaces between the hostname and the parentheses. For example:
> `*.handsonhistory.com(rw)` `*.example.net(ro)`

+   * **NIS groups** — You can allow access to hosts contained in an NIS group. To indicate an NIS group, precede the group name with an at (@) sign (for example, @group).

# ### Access options in /etc/exports

You don’t have to just give away your files and directories when you export a directory with NFS. In the options part of each entry in `/etc/exports`, you can add options that allow or limit access by setting read/write permission. These options, which are passed to NFS, are as follows:

+   * `ro` — Only allow the client to mount this exported file system read-only. The default is to mount the file system read/write.
+   * `rw` — Explicitly ask that a shared directory be shared with read/write permissions. (If the client chooses, it can still mount the directory read-only.)

# ### User mapping options in /etc/exports

Besides options that define how permissions are handled generally, you can also use options to set the permissions that specific users have to NFS shared file systems.

One method that simplifies this process is to have each user with multiple user accounts have the same user name and UID on each machine. This makes it easier to map users so that they have the same permission on a mounted file system as they do on files stored on their local hard disk. If that method is not convenient, user IDs can be mapped in many other ways. Here are some methods of setting user permissions and the `/etc/exports` option that you use for each method:

+   * **root user** — Normally, the client’s root user is mapped into the `nfsnobody` user name (UID 65534). This prevents the root user from a client computer from being able to change all files and directories in the shared file system. If you want the client’s root user to have root permission on the server, use the `no_root_squash` option.
+   
+   * **nfsnobody user/group** — By using the `nfsnobody` user name and group name, you essentially create a user/group whose permissions will not allow access to files that belong to any real users on the server (unless those users open permission to everyone). However, files created by the `nfsnobody` user or group will be available to anyone assigned as the `nfsnobody` user or group. To set all remote users to the `nfsnobody` user/group, use the `all_squash` option.

The `nfsnobody` user is assigned to UIDs and GIDs of 65534. This prevents the ID from running into a valid user or group ID. Using `anolid` or `anogid` options, you