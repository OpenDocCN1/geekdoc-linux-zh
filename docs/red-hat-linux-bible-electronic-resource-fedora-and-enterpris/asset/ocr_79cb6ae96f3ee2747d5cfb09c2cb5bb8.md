```
``` 
10.0.0.0/255.0.0.0 
172.16.0.0/255.255.0.0 
192.168.18.0/255.255.255.0
```
```

+   - **TCP/IP domain** — Using wildcards, you can include all or some host computers from a particular domain level. Here are some valid uses of the asterisk and question mark wildcards:

```
```
*.handsonhistory.com
*craft.handsonhistory.com
???.handsonhistory.com
```
```

The first example matches all hosts in the handsonhistory.com domain. The second example matches woodcraft, basketcraft, or any other host names ending in craft in the handsonhistory.com domain. The final example matches any three-letter host names in the domain.

> **NOTE:** Using an asterisk doesn't match subdomains. For example, * .handsonhistory.com would *not* cause the host name mallard.duck.handsonhistory.com to be included in the access list. Also, separate multiple host names with spaces, but if you add options after each host name, leave no spaces between the host name and the parens. For example:
> * .handsonhistory.com (rw) * .example.net (ro)

+   - **NIS groups** — You can allow access to hosts contained in an NIS group. To indicate a NIS group, precede the group name with an at (@) sign (for example, @group).

# ### Access options in /etc/exports

You don't have to just give away your files and directories when you export a directory with NFS. In the options part of each entry in /etc/exports, you can add options that allow or limit access by setting read/write permission. These options, which are passed to NFS, are as follows:

+   - **ro** — Only allow the client to mount this exported file system read-only. The default is to mount the file system read/write.
+   - **rw** — Explicitly ask that a shared directory be shared with read/write permissions. (If the client chooses, it can still mount the directory read-only.)

# ### User mapping options in /etc/exports

Besides options that define how permissions are handled generally, you can also use options to set the permissions that specific users have to NFS shared file systems.

One method that simplifies this process is to have each user with multiple user accounts have the same user name and UID on each machine. This makes it easier to map users so that they have the same permission on a mounted file system as they do on files stored on their local hard disk. If that method is not convenient, user IDs can be mapped in many other ways. Here