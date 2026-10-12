and *anongid* in the following line are specified to allow root squashing to UID 500 and GID 666:

```
```
/proj       *.nitec.com (anousuid=500 anongid=666)
```
```

If you prefer to squash all the UID/GID pairs to an anonymous UID/GID pair, use the *all_squash* option. For example:

```
```
/proj       *.nitec.com (anousuid=500 anongid=666 all_squash)
```
```

Here, the */proj* directory is exported to all hosts in the *nitec.com* domain, but all accesses are made as UID 500 and GID 666.

If you want to specify a list of UIDs and GIDs that needs to be squashed using the anonymous UID/GID pair, use the *squash_uids* and *squash_gids* options. For example, the following squashes all the UIDs and GIDs in the range 0~100 using the anonymous UID 500 and GID 666:

```
```
/proj       *.nitec.com (anousuid=500 anongid=666 \
                squash_uids=0~100 squash_gids=0~100)
```
```

You can also specify an external map file to map NFS client-supplied UIDs and GIDs to whatever you want. The map is specified using the *map_static* option. For example:

```
```
/proj       *.nitec.com (map_static=/etc/nfs.map)
```
```

Here, the */proj* directory is exported to all the *nitec.com* hosts, but all NFS client-supplied UIDs and GIDs are mapped using the */etc/nfs.map* file. An example of this map file is as follows:

```
```
uid 0~100 -       # squash all remote uids in the 0~100 range
gid 0~100 -       # squash all remote gids in the 0~100 range
uid 500 666   # map remote uid 500 to local uid 666
gid 500 777   # map remote gid 500 to local gid 777
```
```

That covers all the commonly used options for creating the */etc/export* file. Whenever a change is made to the */etc/export* file, however, the NFS daemons need to be told about this change. A script called *exportfs* can be used to restart these daemons, as follows:

```
```
/usr/sbin/exportfs
```
```