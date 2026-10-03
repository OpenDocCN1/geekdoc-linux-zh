The master map, which is in the /etc/auto_master file, associates a directory with a map. The master map is a list that specifies all the maps that Autofs should check. The following example shows what an auto_master file could contain:

```
# Master map for automounter
#
+auto_master
/net  -hosts  -nosuid,nobrowse
/home  auto_home -nobrowse
/xfn  -xfn
```

This example shows the default auto_master file. The lines beginning with # are comments. The line that contains +auto_master specifies the Autofs NIS table map, which is explained in Chapter 18, “Name Services.” Each line thereafter in the master map, /etc/auto_master, has the following syntax:

```
<mount-point> <map-name> <mount-options>
```

Each field is described in Table 17.8.

# TABLE 17.8

# /ETC/AUTO_MASTER FIELDS

| Field | Description |
|-------|-------------|
| mount-point | This is the full (absolute) pathname of a directory that is used as the mount point. If the directory does not exist, Autofs creates it if possible. If the directory does exist and is not empty, mounting on it hides its contents. In this case, Autofs issues a warning. Using the notation /- as a mount point indicates that a direct map with no particular mount point is associated with the map. |
| map-name | This is the map that Autofs uses to find directions to locations or mount information. If the name is preceded by a slash (/), Autofs interprets the name as a local file. Otherwise, it searches for the mount information using the search specified in the name-service switch configuration file (/etc/nsswitch.conf). Name service switches are described in Chapter 18. |
| mount-options | This is an optional comma-separated list of options that applys to the mounting of the entries specified in map-name, unless the entries list other options. Options for each specific type of file system are listed in Table 17.3 under the mount command syntax. For NFS-specific mount points, the bg (background) and fg (foreground) options do not apply. |