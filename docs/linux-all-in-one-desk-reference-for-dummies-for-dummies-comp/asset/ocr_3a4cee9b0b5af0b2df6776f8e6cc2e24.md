are to be mapped to the `anonymous user` (by default this is the user named nobody) — then the options look like this:

(`rw,all_squash`)

Table 6-1 shows the options you can use in the `/etc/exports` file. You find two types of options — general options and user ID mapping options.

**Table 6-1** **Options in `/etc/exports`**
| **This Option** | **Does the Following** |
| --- | --- |
| **General Options** |  |
| `secure` | Allows connections only from ports 1024 or lower (default) |
| `insecure` | Allows connections from ports 1024 or higher |
| `ro` | Allows read-only access (default) |
| `rw` | Allows both read and write access |
| `sync` | Performs write operations (writing information to the disk) when requested (by default) |
| `async` | Performs write operations when the server is ready |
| `no_wdelay` | Performs write operations immediately |
| `wdelay` | Waits a bit to see whether related write requests arrive and then performs them together (by default) |
| `hide` | Hides an exported directory that’s a subdirectory of another exported directory (by default) |
| `no_hide` | Behaves exactly the opposite of `hide` |
| `subtree_check` | Performs subtree checking, which involves checking parent directories of an exported subdirectory whenever a file is accessed (by default) |
| `no_subtree_check` | Turns off subtree checking (opposite of `subtree_check`) |
| `insecure_locks` | Allows insecure file locking |
| **User ID Mapping Options** |  |
| `all_squash` | Maps all user IDs and group IDs to the `anonymous user` on the client |
| `no_all_squash` | Maps remote user and group IDs to similar IDs on the client (by default) |
| `root_squash` | Maps remote `root user` to the `anonymous user` on the client (by default) |
| `no_root_squash` | Maps remote `root user` to the local `root user` |
| `anounid=UID` | Sets the user ID of `anonymous user` to be used for the `all_squash` and `root_squash` options |
| `anongid=GID` | Sets the group ID of `anonymous user` to be used for the `all_squash` and `root_squash` options |

![](bbox=[0.86, 0.5, 0.99, 0.7])