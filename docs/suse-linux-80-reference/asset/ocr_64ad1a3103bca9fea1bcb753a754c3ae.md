For each directory to export, one line is needed to specify which machines may access that directory with what permissions. All subdirectories of this directory will automatically be exported as well. All authorized machines are usually denoted with their full names (including domain name), but it is possible to use wildcards like ‘*’ or ‘?’. If no machine is specified here, any machine is allowed to import this file system with the given permissions.

Permissions of the file system to export are denoted in brackets after the machine name. The most important options are:

| Option | Description |
|---|---|
| `ro` | File system is exported with read-only permission (default). |
| `rw` | File system is exported with read-write permission. |
| `root_squash` | This makes sure that the user root of the given machine does not have root specific permissions on this file system. This is achieved by assigning user ID 65534 to users with user ID 0 (root). This user ID should be set to nobody. |
| `no_root_squash` | Does not assign user ID 0 to user ID 65534 (default). |
| `link_relative` | Converts absolute links (those beginning with `/`) to a sequence of `../`. This is only useful if the whole file system of a machine is mounted (default). |
| `link_absolute` | Symbolic links remain untouched. |
| `map_identity` | User IDs are exactly the same on both client and server (default). |
| `map-daemon` | Client and server do not have matching user IDs. This tells nfsd to create a conversion table for user IDs. `ugidd` is required for this to work. |

# Table 13.13: Permissions for Exported File Systems

Your exports file might look like File 56.