however, you’ll find that you make more and more use of it. Diskless systems are a convenient solution to many problems.

A booting FreeBSD system uses the `vfs.nfs.diskless_valid` to see whether it’s running diskless. If the sysctl equals 0, it’s running off a hard drive; otherwise, it’s running diskless. On diskless systems, FreeBSD runs the `/etc/rc.initdiskless` script to parse and deploy the hierarchical diskless configuration.

# ## Configuration Hierarchy

Configure your diskless farm in the diskless host’s `/conf`. The `/conf` directory can have a whole bunch of directories in it. The two critical ones are `/conf/base` and `/conf/default`, but you might also have separate directories for subnets and/or individual IP addresses. Diskless systems use the contents of these directories to build tmpfs filesystems on top of the mounted root partition so individual hosts can have unique settings and read-write filesystems. You can make any directory a tmpfs filesystem and populate it from this hierarchy, but every host needs a read-write `/etc` directory, so we’ll use that as our example.

The `/conf/base` directory contains base system files that need to be mounted read-write on the diskless client. Create `/conf/base/etc` and populate it with a set of `/etc` files, and the diskless host can use them as the base of its tmpfs `/etc`. (It can also recycle the diskless root’s `/etc`, as we’ll see later.)

The `/conf/default` directory contains defaults for your environment. Perhaps every host in your environment needs an `/etc/fstab` that directs it to mount a shared data store. You’d create `/conf/defaults/etc/fstab`, and the diskless system would copy that to every host on top of the base system from `/conf/base/etc`. I’d also distribute your environment’s generic `rc.conf` in the default directory.

You can also have per-subnet directories. Name that directory after the subnet’s broadcast address, the top address in the network. My diskless farm runs on the subnet 198.51.100.0/24, with a broadcast address of 198.51.100.255. If I created `/conf/198.51.100.255/etc/rc.conf`, every host in that subnet would get that `rc.conf`. If I had a special