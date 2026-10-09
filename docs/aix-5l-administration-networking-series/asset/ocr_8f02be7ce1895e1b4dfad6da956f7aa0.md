| Local File System | Non-LFS (Journaled File System) |
| --- | --- |
| rw/ro backup for each filesset | Only rw filessets |
| Multiple filesets per aggregate | One fileset per aggregate (JFS) |
| DCE ACLs |  |

**Table 15-2.** DFS Local File System vs. DFS Non-LFS

# ## VFS Compatibility

Any virtual file system (VFS) that has been enhanced to support DCE VFS+ can be exported by DFS file servers. DFS also provides an NFS/DFS Authenticating Gateway to provide DFS filesystem access to NFS clients. An NFS client may have difficulty working with DFS ACLs in the exported filesystem because it does not have a way to get a DCE context. The following is what you can do to set default ACLs that open this security exposure:

```
# acl_edit /.../[PathName] -m any_other:rxwcid
# acl_edit /.../[PathName] -ic -m any_other:rxwcid
# acl_edit /.../[PathName] -io -m any_other:rxwcid
# acl_edit /.../[PathName]/[EachFile] -m any_other:rxwcid
```

The NFS to DFS Authenticating Gateway maintains DCE credentials on behalf of NFS clients to satisfy ACL permission restrictions. To use this feature, install the `dfs.nfsauth.rte` and `dfs.nfsauth.sm` file sets. AFS and NFS may also be used independently on a DFS file server. Given these capabilities, you should be able to easily integrate DCE DFS into existing NFS and AFS environments.

# ## DFS Components

As already mentioned, DFS requires a number of servers for coordinating filesystem activities in a cell. These servers can be distributed and in some cases replicated across a number of machines, or they can be run on a single computer. I would not recommend the latter unless you are running a very small cell. The cluster of DFS servers includes

+   - The **System Control Machine (SCM)** is responsible for housing and distributing the administration lists. These lists determine which principals (users and machines) can issue requests to the DFS servers. The group of servers managed by the SCM is called its *domain*. The SCM must be configured before any other DFS servers. Administrative lists managed by the SCM are stored in /opt/dfsclocal/var/dfs. The two server processes that run on the SCM are **boss server** and **ups server**. The **boss server** process is the basic overserver server,