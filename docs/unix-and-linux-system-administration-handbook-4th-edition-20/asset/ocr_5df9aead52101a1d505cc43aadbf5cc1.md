For example, consider the following list of directories, with the directories to be exported in boldface.

```
/www/domain1
/www/domain2
/www/domain3
/var/logs/httpd
/var/spool
```

In NFS version 3, each exported directory must be separately configured. Client systems must execute three different mount requests to obtain access to all the server's exports.

In NFS version 4, however, the pseudo-filesystem bridges the disconnected portions of the directory structure to create a single view for NFS clients. Rather than requesting a separate mount for /www/domain1, /www/domain2, and /var/logs/httpd, the client can simply view the server's pseudo-root directory and browse the hierarchy.

The directories that are not exported, /www/domain3 and /var/spool, do not appear during browsing. In addition, individual files contained in /,var, /www, and /var/logs are not visible to the client because the pseudo-filesystem portion of the hierarchy includes only directories. Thus, the client view of the NFS4-exported file system is

```
/
/www
/www/domain1
/www/domain2
/var
/var/logs
/var/logs/httpd
```

The server specifies the root of the exported filesystems in a configuration file known as the exports file.

# File locking

File locking (implemented by the flock, lockf, and fcntl systems calls) has been a sore point on UNIX systems for a long time. In the context of NFS, the ground is shakier than still. By design, early versions of NFS servers are stateless: they have no idea what machines are using any given file. However, state information is needed to implement locking. What to do?

The traditional answer is to implement file locking separately from NFS. In most systems, the two daemons lockd and stat try to make a go of it. Unfortunately, the task is difficult for variety of subtle reasons, and NFS file locking generally tended to be flaky.