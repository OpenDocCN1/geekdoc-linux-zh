| Type | Effect |
| --- | --- |
| user_obj | The user who owns the object |
| user | The user "username" from the local cell |
| foreign_user | The user "username" from the foreign cell "cell_name" |
| group_obj | Members of the group who own the object |
| group | The group "group_name" from the local cell |
| foreign_group | The group "group_name" from the foreign cell "cell_name" |
| other_obj | Users from the local cell who do not match any preceding entries |
| foreign_other | Users from the foreign cell "cell_name" who do not match any of the preceding entries |
| any_other | Users from any foreign cell who do not match any of the preceding entries |
| mask_obj | Mask for maximum permissions that can be set, except for group_obj and other_obj |

# Table 15-5. ACL Object Types and Effects

# # FILESET REPLICATION

DFS replication is a handy tool for managing common filesystem trees across a number of machines when availability requirements will not allow network mounting. A replicated fileset should be a group of files that are not modified often. Good candidates for replication include operating system commands and application binaries. Replicas are created from a RW master copy. Each replica fileset is RO. Replicas are updated either at scheduled intervals or at manually called releases. To create a replica, begin by setting the replication information and site list on the machine with the master copy of the fileset.

```
# fts ssetrepinfo [-release | -scheduled] ← Source replica type
# fts addsite ←—Source sitelist update
```

On the target machine(s), first create an aggregate large enough to hold the replica and update the site list.

```
# fts addsite ←——Client sitelist update
```

If you chose scheduled replication, then the fileset will be replicated at the interval you indicated. For release replicas, you can manually start replication using the fts release option.

```
# fts release ←—Manual replication
```

Note that replication improves availability by making multiple copies of a fileset available to clients. The client cache manager will select RO replicas when acquiring a mount point unless RW is specified.