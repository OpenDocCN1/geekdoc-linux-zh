# The df Command

The df command lists the disk usage of a mounted file system. Run it on the NFS client to verify that NFS mounting has occurred. In many cases, the root_squash mount option prevents the root user from doing this. Therefore, it is best to try it as an unprivileged user.

The syntax to use df command is follows:

```
[root@netx tmp]$ df -F nfs
[root@netx tmp]$
```

# The nfsstat Command

The nfsstat command provides useful error statistics. The -s option provides NFS server stats, while the -c option provides them for clients.

Let's summarize the main points of the Lab.

# Summary

In this chapter, you learned to install and configure NFS protocol server and client.