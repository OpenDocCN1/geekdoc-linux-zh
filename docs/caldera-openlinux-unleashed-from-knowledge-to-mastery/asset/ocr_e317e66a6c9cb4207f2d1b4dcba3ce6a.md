- **b**  With the number of 4KB blocks that this directory can use.

To limit the size of the home directory for user `silenzu` to about 50MB of disk space, use `nwdssetspace` as follows:

```
```
nwdssetspace -d /NetWare/NDS/Macmillan/Publishing/sys/home
/silenzu -m 50
```
```

# ## File System Trustees on NDS Servers

A file system trustee on a NetWare NDS server is an object (usually a user object) that has been granted a set of access rights to a file or directory on a NetWare volume.

As you view file system trustee assignments, remember that the effective rights for a user can be a combination of the trustee assignments the user has to a file or directory, to parent directories, to parent NDS objects (as limited by any inherited rights filters that might exist), and to security equivalence or group trustee assignment. Because all the possible rights a file or directory can hold are the same in NDS as they are for bindery servers, refer to the section entitled “NetWare Administration for Bindery Servers” earlier in the chapter.

To view an object’s rights to files and or directories on the server, use:

```
```
nwdsshowtrust -o path_to_object
```
```

To add or change an object as a trustee to another file or directory, use:

```
```
nwdsaddtrust -o path to object
```
```

Suppose you want to grant an object called `silenzu` in the `Publishing` organization of the authenticated NDS tree `Macmillan` all rights to the directory `/users/hsimpson` on `workserver`’s old volume. You use `nwdsaddtrust` as follows:

```
```
nwdsaddtrust -o /NetWare/NDS/Macmillan/Publishing/silenzu -r ff
-p /NetWare/NDS/Macmillan/workserver_old/users/hsimpson
```
```

Notice that this example uses the hexadecimal value `ff` to assign full rights, but it could have used the mnemonic value `[RWCEMF]`.

# ## Summary

The NetWare client brings practical NetWare integration and administrative capabilities to the Linux platform. You can use the utilities to simply log in and access your personal work files on any NDS or bindery server, as well as perform many important administrative functions. If you want to stay up to date with the developments Caldera makes to