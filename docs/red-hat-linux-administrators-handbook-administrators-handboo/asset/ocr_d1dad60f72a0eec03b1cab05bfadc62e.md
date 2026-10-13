After you mount the NFS server-exported files on your NFS client system, your users can start using the mounted file systems or directories immediately. Before you allow users access to your NFS exports, consider the following security issues.

# Securing Your NFS Server

The portmap program, in combination with rpc.nfsd, can be fooled, making it possible for unauthorized persons to get to files on NFS servers without having any privileges. Fortunately, the portmap program that Linux uses is relatively secure against attack and can be made more secure by adding the following line in the /etc/hosts.deny file:

```
portmap: ALL
```

The system will deny portmap access for everyone. Next, the /etc/hosts.allow file needs to be modified as follows:

```
portmap: 192.168.1.0/255.255.255.0
```

This allows all hosts from the 192.168.1.0 network to have access to portmap-administered programs, such as nfsd and mountd.

> **Caution**
> 
> Never use host names in the portmap line in /etc/hosts.allow, because use of host name lookups can indirectly cause portmap activity, which will trigger host name lookups in a loop.

One other security issue on the server side is whether to allow the root account on a client to be treated as root on the server. By default, Linux prohibits root on the client side of the NFS to be treated as root on the server side. In other words, an exported file owned by root on the server cannot be modified by the client root user. To explicitly enforce this rule, the /etc/exports file can be modified as follows:

```
/www www1.nitec.com(rw, root_squash)
```

Now, if a user with UID 0 (the root user) on the client attempts to access (read, write, or delete) the file system, the server substitutes the UID of the server's nobody account. This means the root user on the client can't