# # 19.1 Features and Benefits

The distributed file system (DFS) provides a means of separating the logical view of files and directories that users see from the actual physical locations of these resources on the network. It allows for higher availability, smoother storage expansion, load balancing, and so on.

For information about DFS, refer to the Microsoft documentation$^{1}$. This document explains how to host a DFS tree on a UNIX machine (for DFS-aware clients to browse) using Samba. A Samba server can be made a DFS server by setting the global Boolean *host msdfs* parameter in the *smb.conf* file. You designate a share as a DFS root using the share-level Boolean *msdfs root* parameter. A DFS root directory on Samba hosts DFS links in the form of symbolic links that point to other servers. For example, a symbolic link *junction->msdfs:storage1\share1* in the share directory acts as the DFS junction. When DFS-aware clients attempt to access the junction link, they are redirected to the storage location (in this case, *\\storage1\share1*).

DFS trees on Samba work with all DFS-aware clients ranging from Windows 95 to 200X. Example 19.1.1 shows how to setup a DFS tree on a Samba server. In the */export/dfsroot* directory, you set up your DFS links to other servers on the network.

```
root# cd /export/dfsroot
root# chown root /export/dfsroot
root# chmod 755 /export/dfsroot
root# ln -s msdfs:storageA\\shareA linka
```

> $^{1}$<http://www.microsoft.com/NTServer/nt5/downloads/winfeatures/NTSDistriFile/AdminGuide.asp>