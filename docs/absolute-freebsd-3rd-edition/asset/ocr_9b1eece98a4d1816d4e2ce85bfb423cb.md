Here, I create a pool named \textit{db}, using a mirror VDEV and two GPT-labeled partitions:

```
# zpool create db mirror gpt/zfs3 gpt/zfs4
```

The structure we assign gets reflected in the pool status.

```
# zpool status db
--snip--
config:

NAME STATE READ WRITE CKSUM
\textbf{db} ONLINE 0 0 0
\textbf{\small\textcircled{1}} mirror-0 ONLINE 0 0 0
\textbf{\small\textcircled{2}} gpt/zfs3 ONLINE 0 0 0
\textbf{\small\textcircled{3}} gpt/zfs4 ONLINE 0 0 0
--snip--
```

The pool \textit{db} contains a single VDEV, named \textit{mirror-0} \textbf{\small\textcircled{1}}. It includes two partitions with GPT labels, /dev/gpt/zfs3 \textbf{\small\textcircled{2}} and /dev/gpt/zfs \textbf{\small\textcircled{3}}. All of those partitions are online.

If you don’t include a VDEV name, zpool(8) creates a striped pool with no redundancy. Here, I create a striped pool called \textit{scratch}:

```
# zpool create scratch gpt/zfs3 gpt/zfs4
```

The pool status shows each VDEV, named after the underlying disk.

```
--snip--
NAME STATE READ WRITE CKSUM
garbage ONLINE 0 0 0
gpt/zfs3 ONLINE 0 0 0
gpt/zfs4 ONLINE 0 0 0
--snip--
```

Creating any type of RAID-Z looks much like creating a mirror. Just use the correct VDEV type.

```
# zpool create db raidz gpt/zfs3 gpt/zfs4 gpt/zfs5
```

The pool status closely resembles that of a mirror, but with more disks in the VDEV.