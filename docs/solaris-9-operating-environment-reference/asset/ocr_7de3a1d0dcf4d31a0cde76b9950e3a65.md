# export — Shell Built-in Environment Variable Function

# Synopsis

```
sh
export [name...]
```

```
ksh
export [name=value]
```

# Description

set(1).

# exportfs — Translate exportfs Options to share/unshare Commands

# Synopsis

```
/usr/sbin/exportfs [-aiuv] [-o options] [pathname]
```

# Description

exportfs translates SunOS 4.x exportfs options to the corresponding share/unshare options and invokes share/unshare with the translated options.

With no options or arguments, exportfs invokes share to print out the list of currently shared NFS file systems.

> Note — exportfs is the BSD/Compatibility Package command of share(1M) and unshare(1M). Use share(1M) whenever possible.

# Options

+   -a
Invoke shareall(1M), or if -u is specified, invoke unshareall(1M).

+   -i
Ignore options in /etc/dfs/dfstab.

+   -o options
Specify a comma-separated list of optional characteristics for the systems being exported. exportfs translates options to share-equivalent options. (See share(1M) for information about individual options.)

+   -u
Invoke unshare(1M) on path name.

+   -v
Verbose.