# SEE ALSO

dump(8), newfs(8), mount(8), mfs(8), rmt(8)

# BUGS

**Restore** can get confused when doing incremental restores from dump that were made on active file systems.

A level zero dump must be done after a full restore. Because restore runs in user code, it has no control over inode allocation; thus a full dump must be done to get a new set of directories reflecting the new inode numbering, even though the contents of the files is unchanged.

The Linux port of **restore** is not able yet to restore multi-volume backups.

# HISTORY

The **restore** command appeared in 4.2BSD.

# ROUTE(8)

# NAME

**route**  Show / manipulate the IP routing table.

# SYNOPSIS

```
```
route [-n\nec]     route [-v] add [-net|-host] Target [netmask Nm] [gw Gw]
                    [metric N] [mss M] [window W] [irtt I] [reject] [mod] [dyn]
                    [reinstall] [[dev] I]
     route [-v] del [-net|-host] Target [gw Gw] [netmask Nm]
                    [metric N] [[dev] I]
     route [-V] [--version] [-h] [--help]
```
```

# DESCRIPTION

**route** manipulates the kernel's IP routing table. Its primary use is to set up static routes to specific hosts or networks via an interface after it has been configured with the **ifconfig**(8) program.