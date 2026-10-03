With this entry in the /etc/auto_master file, /etc/auto_share is the name of the indirect map file for the mount point /share. For this entry, you also need to create an indirect map file named /etc/auto_share, which would look like this:

```
# share directory map for automounter
#
ws            neptune:/export/share/ws
```

If the /share directory is accessed, the Autofs service creates a trigger node for /share/ws, and the following entry is made in the /etc/mnt-tab file:

```
-hosts  /share/ws  autofs \
nosuid,nobrowse,ignore,nest,dev=###
```

If the /share/ws directory is accessed, the Autofs service completes the process with these steps:

+   1. It pings the server's mount service to see if it's alive.
2. It mounts the requested file system under /share. Now /etc/mnttab file contains the following entries:

```
-hosts  /share/ws  autofs \
nosuid,nobrowse,ignore,nest,dev=###
neptune:/export/share/ws /share/ws  nfs \
nosuid,dev=####  #####
```

Lines in indirect maps have the following general syntax:

```
<key> <mount-options> <location>
```

The fields in this line are described in Table 17.10.

# TABLE 17.10

# INDIRECT MAP FIELDS

| Field | Description |
|---|---|
| key | key is a simple name (no slashes) in an indirect map. |
| mount-options | The mount-options are the options you want to apply to this particular mount. They are described in Table 18-4. They are required only if they differ from the map default options specified in the /etc/auto_master file. |
| location | location is the remote location of the file system specified as server:pathname. More than one location can be specified. The pathname should not include an auto-mounted mount point; it should be the actual absolute path to the file system. For instance, the location of a directory should be listed as server:/usr/local, not as server:/net/server/usr/local. |